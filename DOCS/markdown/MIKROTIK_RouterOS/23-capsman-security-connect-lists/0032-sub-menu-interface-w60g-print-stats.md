## Sub-menu: `/interface w60g print stats` 

Provides more detailed information about Beamforming occurrences and some debug information: 

```
/interface w60g print stats name: wlan60-1
beamforming-event: 310
tx-io-msdu: 0
tx-sw-msdu: 154 663
tx-fw-msdu: 102
tx-ppdu: 220 147
tx-ppdu-from-q: 40 327
tx-mpdu-new: 154 663
tx-mpdu-total: 184 759
tx-mpdu-retry: 30 096
rx-ppdu: 166 636
rx-mpdu-crc-err: 4 817
rx-mpdu-crc-ok: 285 649
```

Station interface properties 

**==> picture [13 x 13] intentionally omitted <==**

ap-bridge device requires License level 4 (click for more information)  to support more than one connected client 

Connected clients are treated as individual interfaces, after successful connection new station interface is created. 

After update default configuration still works - newly created station interface is moved to default bridge.
