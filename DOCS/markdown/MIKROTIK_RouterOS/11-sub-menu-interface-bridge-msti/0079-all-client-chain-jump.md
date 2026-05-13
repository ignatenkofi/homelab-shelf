## `# All client chain jump` 

```
/ip firewall nat add chain=srcnat action=jump jump-target=clients \
    src-address="$StartingAddress-$($StartingAddress + ($ClientCount * $AddressesPerClient) - 1)"
:local currentPort $StartingPort
:for c from=1 to=$ClientCount do={
    # Specific client chain jumps
    :if ($AddressesPerClient > 1) do={
      /ip firewall nat add chain=clients action=jump jump-target="client-$c" \
      src-address="$($StartingAddress + ($AddressesPerClient * ($c - 1)))-$($StartingAddress +
($AddressesPerClient * $c -1))"
```

```
    } else={
      /ip firewall nat add chain=clients action=jump jump-target="client-$c" \
      src-address="$($StartingAddress + ($AddressesPerClient * ($c - 1)))"
    }
```

650 

```
    # Translation rules
    :for a from=1 to=$AddressesPerClient do={
```

```
      /ip firewall nat add chain="client-$c" action=src-nat protocol=tcp \
      src-address="$($StartingAddress + (($c -1) * $AddressesPerClient) + $a - 1)" to-address=$PublicAddress to-
ports="$currentPort-$($currentPort + $PortsPerAddress - 1)"
```

```
      /ip firewall nat add chain="client-$c" action=src-nat protocol=udp \
      src-address="$($StartingAddress + (($c -1) * $AddressesPerClient) + $a - 1)" to-address=$PublicAddress to-
ports="$currentPort-$($currentPort + $PortsPerAddress - 1)"
```

```
      :set currentPort ($currentPort + $PortsPerAddress)
```

```
    }
}
}
```

The six local values can be adjusted and the script can be either simply pasted in the terminal or it can be stored in the system script section, in case the configuration needs to be regenerated later. 

After execution, you should get a set of rules: 

- `[admin@MikroTik] > ip firewall nat print Flags: X - disabled, I - invalid; D - dynamic` 

- `0    chain=srcnat action=jump jump-target=clients src-address=100.64.0.1-100.64.0.10` 

- `1    chain=clients action=jump jump-target=client-1 src-address=100.64.0.1-100.64.0.2` 

- `2    chain=client-1 action=src-nat to-addresses=2.2.2.2 to-ports=5000-5199 protocol=tcp src-address=100.64.0.1` 

- `3    chain=client-1 action=src-nat to-addresses=2.2.2.2 to-ports=5000-5199 protocol=udp src-address=100.64.0.1` 

- `4    chain=client-1 action=src-nat to-addresses=2.2.2.2 to-ports=5200-5399 protocol=tcp src-address=100.64.0.2` 

- `5    chain=client-1 action=src-nat to-addresses=2.2.2.2 to-ports=5200-5399 protocol=udp src-address=100.64.0.2` 

- `6    chain=clients action=jump jump-target=client-2 src-address=100.64.0.3-100.64.0.4` 

- `7    chain=client-2 action=src-nat to-addresses=2.2.2.2 to-ports=5400-5599 protocol=tcp src-address=100.64.0.3` 

- `8    chain=client-2 action=src-nat to-addresses=2.2.2.2 to-ports=5400-5599 protocol=udp src-address=100.64.0.3` 

- `9    chain=client-2 action=src-nat to-addresses=2.2.2.2 to-ports=5600-5799 protocol=tcp src-address=100.64.0.4` 

- `10    chain=client-2 action=src-nat to-addresses=2.2.2.2 to-ports=5600-5799 protocol=udp src-address=100.64.0.4` 

- `11    chain=clients action=jump jump-target=client-3 src-address=100.64.0.5-100.64.0.6` 

- `12    chain=client-3 action=src-nat to-addresses=2.2.2.2 to-ports=5800-5999 protocol=tcp src-address=100.64.0.5` 

- `13    chain=client-3 action=src-nat to-addresses=2.2.2.2 to-ports=5800-5999 protocol=udp src-address=100.64.0.5` 

- `14    chain=client-3 action=src-nat to-addresses=2.2.2.2 to-ports=6000-6199 protocol=tcp src-address=100.64.0.6` 

- `15    chain=client-3 action=src-nat to-addresses=2.2.2.2 to-ports=6000-6199` 

651 

```
      protocol=udp src-address=100.64.0.6
```

```
[...]
```
