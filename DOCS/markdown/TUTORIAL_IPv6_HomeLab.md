# IPv6 в хоумлабе: ULA → Hurricane Electric 6in4 → dual-stack + home.arpa

Пошаговый туториал «по вечерам» по плану, принятому 2026-05-19: провайдер
нативного IPv6 не даёт и ждать его не будем; сначала внутренний IPv6 на
ULA-адресах, затем глобальный через бесплатный 6in4-туннель Hurricane
Electric; dual-stack на одном RB5009, локальные имена — в зоне `home.arpa`.
Выигрыша в скорости не будет и не обещается — ценность образовательная и
функциональная.

Каждый этап — один вечер, со своей проверкой и откатом. Не начинай
следующий, пока проверка текущего не зелёная.

> **Железо в тексте:** RB5009 (роутер, RouterOS v7), CRS304/CRS305 (свитчи),
> hAP ax² (Wi-Fi), UGreen NAS, клиенты macOS/iOS/Linux. Команды — CLI
> RouterOS v7; детали любой команды — в полке: Chapter 2 (IPv4/IPv6
> Fundamentals), Chapter 6 (Firewall), SUBINDEX'ы в INDEX.md.

---

## Этап 0 (вечер 0): инвентарь и страховка

1. **Бэкап конфига** — обязателен, это точка отката всего туториала:

   ```routeros
   /system backup save name=pre-ipv6
   /export file=pre-ipv6-export
   ```

   Скачай оба файла с роутера (Files → download) на NAS/ноутбук.

2. **Проверь пакет IPv6.** В RouterOS v7 IPv6 входит в основной пакет, но
   может быть выключен:

   ```routeros
   /ipv6 settings print
   ```

   Если `disable-ipv6=yes` — включи: `/ipv6 settings set disable-ipv6=no`.

3. **Карта адресации.** Заполни таблицу до того, как трогать конфиг, и
   держи её в этом же файле (или рядом) — это единственный источник правды
   на все этапы:

   | Сегмент | VLAN/бридж | IPv4 | ULA /64 (этап 1) | GUA /64 (этап 4) |
   |---|---|---|---|---|
   | LAN (основной) | `bridge` | 192.168.88.0/24 | `<ULA>:0088::/64` | `<GUA>:0088::/64` |
   | Lab (Proxmox) | VLAN 30 | 192.168.30.0/24 | `<ULA>:0030::/64` | — (решить позже) |
   | Полигон | VLAN 40 | 192.168.40.0/24 | `<ULA>:0040::/64` | — |

   Соглашение: hex-группа ULA/GUA-подсети повторяет номер VLAN — адрес
   читается глазами без таблицы. Ряды подгони под фактическую разбивку
   (актуальная — в homenet-iac).

**Проверка этапа:** бэкап скачан и открывается; `disable-ipv6=no`; таблица
заполнена.

---

## Этап 1 (вечер 1): внутренний IPv6 на ULA

ULA (RFC 4193, `fd00::/8`) — приватные адреса: работают без провайдера и
туннеля, наружу не маршрутизируются, при появлении GUA продолжают жить
рядом (в IPv6 несколько адресов на интерфейсе — норма).

1. **Сгенерируй свой /48-префикс.** 40 бит после `fd` обязаны быть
   случайными — не выдумывай «красивый» и не бери из примеров:

   ```bash
   python3 -c "import secrets; print('fd' + secrets.token_hex(5))" \
     | sed -E 's/(..)(....)(....)/\1\2:\3/;s/$/::\/48/'
   ```

   Результат вида `fdab:cdef:1234::/48` запиши в карту адресации как `<ULA>`.

2. **Назначь /64 на LAN-бридж** (адрес роутера в этой сети — `::1`):

   ```routeros
   /ipv6 address add address=<ULA>:0088::1/64 interface=bridge advertise=yes
   ```

   `advertise=yes` включает SLAAC: RA-анонс префикса, клиенты соберут себе
   адреса сами. Повтори для VLAN-интерфейсов из карты (interface —
   соответствующий vlan-интерфейс на RB5009).

3. **Router Advertisement и DNS в RA.** Чтобы клиенты узнали и DNS:

   ```routeros
   /ipv6 nd set [find default=yes] ra-interval=20s-60s dns=<ULA>:0088::1
   ```

4. **Проверка с клиентов:**
   - macOS: `ifconfig en0 | grep inet6` — должен появиться адрес из
     `<ULA>:0088::/64` (плюс link-local `fe80::`);
   - Linux: `ip -6 addr show dev eth0`; `ping <ULA>:0088::1` — роутер
     отвечает;
   - iPhone: Настройки → Wi-Fi → (i) — адрес IPv6 из ULA-диапазона.

   NAS и серверам, к которым будешь ходить по имени, лучше задать
   **статические** ULA (например `<ULA>:0088::20` для NAS) — SLAAC-адреса
   с privacy extensions меняются, DNS-записи к ним не привяжешь.

**Проверка этапа:** клиенты в LAN пингуют друг друга и роутер по ULA.
**Откат:** удалить `/ipv6 address` и вернуть `/ipv6 nd` к дефолту — IPv4
не затронут вообще.

---

## Этап 2 (вечер 2): локальные имена в home.arpa

`home.arpa` — стандартная зона для домашних сетей (RFC 8375): регистрация
не нужна, наружу не утекает. DNS-сервер — сам RB5009.

1. **Статические записи** для всего, у чего есть постоянный адрес — парами
   A (IPv4) + AAAA (ULA):

   ```routeros
   /ip dns static add name=router.home.arpa address=192.168.88.1
   /ip dns static add name=router.home.arpa address=<ULA>:0088::1 type=AAAA
   /ip dns static add name=nas.home.arpa address=192.168.88.20
   /ip dns static add name=nas.home.arpa address=<ULA>:0088::20 type=AAAA
   ```

   (Плюс proxmox, VM 106/107/108 и прочие постоянные жильцы — по карте.)

2. **Убедись, что клиенты используют роутер как DNS** (обычно уже так через
   DHCP option 6 / RA dns). `allow-remote-requests=yes` в `/ip dns` должен
   быть включён — но тогда обязательно проверь, что на WAN вход в 53-й порт
   закрыт firewall'ом (в дефолтном конфиге закрыт).

3. **Поисковый домен**, чтобы работало короткое `ssh nas`:

   ```routeros
   /ip dhcp-server network set [find] domain=home.arpa
   ```

4. **Проверка:** `ping nas.home.arpa` с ноутбука резолвится и идёт (по
   IPv4); `ping6 nas.home.arpa` — по ULA. `dig nas.home.arpa AAAA` отдаёт
   ULA-адрес.

**Проверка этапа:** имена работают с обоих стеков.
**Откат:** удалить статические записи — ничего больше не менялось.

---

## Этап 3 (вечер 3): туннель Hurricane Electric — сначала гейт

> **Гейт перед этапом.** 6in4 — это protocol 41 поверх IPv4, и он требует
> **публичный** IPv4 на WAN RB5009. Известно (решение от 2026-07-27 по
> доменному проекту): постоянного белого IPv4 у провайдера нет, адрес
> динамический. Динамический — не приговор (HE умеет update-URL), а вот
> CGNAT — приговор. Проверь:
>
> ```routeros
> /ip address print where interface=<WAN-интерфейс>
> ```
>
> и сравни с `curl -4 ifconfig.me` с любой машины за роутером.
> - **Совпали и адрес не из 100.64.0.0/10** → публичный динамический IPv4,
>   продолжаем.
> - **Не совпали / 100.64.x.x** → CGNAT: 6in4 не пройдёт. Честные варианты:
>   остаться на ULA (этапы 1–2 самодостаточны), попросить у провайдера
>   белый IP, или строить IPv6 поверх WireGuard/VPS — это отдельный дизайн,
>   не этот туториал. **Дальше не идти.**

1. **Аккаунт** на tunnelbroker.net → Create Regular Tunnel → endpoint —
   твой текущий WAN IPv4, сервер — ближайший (Франкфурт/Прага — по плану).
   HE выдаст: Server IPv4, Server IPv6, Client IPv6, Routed /64 (и /48 по
   кнопке — возьми сразу, пригодится на VLAN'ы).

2. **Интерфейс туннеля** (HE в примерах для MikroTik использует тип 6to4 —
   это generic sit/protocol-41 туннель):

   ```routeros
   /interface 6to4 add name=sit-he local-address=<WAN-IPv4> \
     remote-address=<HE-Server-IPv4> comment="HE tunnelbroker"
   /ipv6 address add address=<Client-IPv6>/64 interface=sit-he advertise=no
   /ipv6 route add dst-address=::/0 gateway=<Server-IPv6>
   ```

3. **Firewall IPv4:** разрешить protocol 41 только с сервера HE:

   ```routeros
   /ip firewall filter add chain=input protocol=ipv6-encap \
     src-address=<HE-Server-IPv4> action=accept place-before=0 \
     comment="HE 6in4"
   ```

4. **Динамический IP:** в HE включи update-URL (формат в кабинете HE) и
   повесь на RB5009 scheduler, дёргающий его при смене WAN-адреса; иначе
   туннель молча умрёт при первой смене IP. Плюс: смена WAN-IP требует
   обновить `local-address` туннеля — тем же скриптом.

5. **Проверка с роутера:** `/ping <Server-IPv6>` — туннель жив;
   `/ping 2606:4700:4700::1111` — мир достижим.

**Проверка этапа:** с роутера пингуется IPv6-мир.
**Откат:** disable `sit-he` + удалить дефолтный маршрут — сеть как раньше.

---

## Этап 4 (вечер 4): dual-stack для клиентов + firewall

Раздаём routed-префикс HE в LAN. **Firewall — до раздачи**, не после:
с GUA-адресами клиенты становятся достижимы из интернета напрямую, NAT'а,
который «случайно защищал», в IPv6 нет.

1. **Baseline IPv6 firewall** (сверь с дефолтным набором v7 — Chapter 6):

   ```routeros
   /ipv6 firewall filter
   add chain=input action=accept connection-state=established,related,untracked
   add chain=input action=drop connection-state=invalid
   add chain=input action=accept protocol=icmpv6
   add chain=input action=accept in-interface=!sit-he comment="LAN to router"
   add chain=input action=drop comment="drop all else"
   add chain=forward action=accept connection-state=established,related,untracked
   add chain=forward action=drop connection-state=invalid
   add chain=forward action=accept protocol=icmpv6
   add chain=forward action=accept out-interface=sit-he comment="LAN out"
   add chain=forward action=drop comment="no unsolicited inbound"
   ```

   ICMPv6 резать нельзя — на нём стоит ND/PMTUD, «запрещу ping» здесь
   ломает сеть.

2. **Раздай routed /64** на LAN-бридж рядом с ULA:

   ```routeros
   /ipv6 address add address=<Routed-64>::1/64 interface=bridge advertise=yes
   ```

   Клиенты соберут GUA по SLAAC. ULA при этом остаётся — для внутреннего
   трафика и home.arpa.

3. **Проверка:** с ноутбука <https://test-ipv6.com> — 10/10 (или близко);
   `curl -6 ifconfig.co` показывает адрес из Routed /64; **встречная
   проверка firewall'а**: с внешнего IPv6-хоста (телефон в LTE) попытка
   зайти на GUA-адрес ноутбука по 22/80 — таймаут.

4. **MTU.** 6in4 съедает 20 байт: MTU туннеля 1480. Если какие-то сайты
   по IPv6 «висят» — это почти всегда PMTUD, проверь, что ICMPv6
   packet-too-big не режется по пути (п. 1 выше).

**Проверка этапа:** dual-stack на клиентах, входящие снаружи закрыты.
**Откат:** убрать GUA-адрес с бриджа — клиенты возвращаются на IPv4+ULA.

---

## Этап 5 (вечер 5): хвосты и эксплуатация

- **hAP ax² и свитчи** — если они в режиме bridge/switch, им ничего не
  нужно: IPv6 для них прозрачен. Управляющим интерфейсам можно дать
  статический ULA и записи в home.arpa.
- **Proxmox / VM (VLAN 30)** — решить, нужен ли лабе GUA вообще; ULA для
  внутренних нужд часто достаточно, а полигон (VLAN 40) по дизайну
  deny-by-default — GUA туда не раздавать без явной причины.
- **Мониторинг туннеля**: netwatch на `<Server-IPv6>` с логом — иначе о
  смерти туннеля узнаёшь по «почему картинки не грузятся».
- **Свежий бэкап**: `/system backup save name=post-ipv6` + `/export` — и
  экспорт правил в homenet-iac, чтобы IaC-слепок не разъехался с рукой.

---

## Куда смотреть, когда что-то не так

| Симптом | Первый подозреваемый |
|---|---|
| Клиент не получил ULA/GUA | `advertise=yes` на адресе; `/ipv6 nd` на интерфейсе |
| `ping6` роутера работает, мир — нет | дефолтный маршрут через `<Server-IPv6>`; жив ли туннель |
| Туннель умер «сам» | сменился WAN IP: update-URL + `local-address` |
| Сайты по IPv6 висят | MTU/PMTUD: ICMPv6 packet-too-big режется |
| Имена `home.arpa` не резолвятся | клиент ходит не в роутер за DNS; search-домен |

Разделы полки по теме: Chapter 2 «IPv4 and IPv6 Fundamentals» (адресация,
ND, RA), Chapter 6 «Firewall» (ipv6 firewall filter), Chapter 13
«Scripting» (update-скрипт для динамического IP).
