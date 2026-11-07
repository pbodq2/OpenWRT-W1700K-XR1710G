
## Limitations / bugs

The main OS *.itb binary is in ubi 2.0 layout. Users need a corresponding ubi 2.0 chainloader as well. Please check out the repos on [naoki66](https://github.com/naoki66/Gemtek-brightspeed-chainloader/releases), [YYH2913](https://github.com/YYH2913/http-uboot/releases) or [hurrian](https://github.com/hurrian/w1700k-ubi-installer/releases). Please **DO NOT** use any chainloader compiled from this build.

---
### Toggle HW / SW Offload:
It is recommended to control it by the Airoha FlowSense app button rather than the built-in Firewall page. The app includes extra part of API control. Also, It is recommended to disable Packet Steering on the Interface page if you turn on HW Offloading.

---
### MT76 (MT7996AV + MT7976GN + MT7977AN + MT7977BN) 6GHz radio driver bugs in certain scenarios:

#### Mesh node:

HW / SW / NO offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |  MASTER (AP) |live|
| 5 GHz  |    MASTER (AP)  |live|
| 6 GHz  | *MESH (802.11s)*|live (**requires both 2.4GHz and 5GHz live first**)|

HW / SW / NO offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |MASTER (AP)|live|
| 5 GHz  |*MESH (802.11s)*|live|
| 6 GHz  |MASTER (AP)|live (**requires 2.4GHz lives first**)|

#### Ordinary gateway (router) or dumb AP bridge:
HW / SW / NO offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |MASTER (AP)|live|
| 5 GHz  |MASTER (AP)|live|
| 6 GHz  |MASTER (AP)|live (**requires either 2.4GHz or 5GHz lives first, 6GHz cannot lives standalone**)|

#### WISP:
SW / NO offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |MASTER (AP)|live|
| 5 GHz  |MASTER (AP)|live|
| 6 GHz  |*client*|live (**requires 5GHz alive first, client's upload throughtput drops half, download is not affected**)|

HW offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |MASTER (AP)|live|
| 5 GHz  |MASTER (AP)|live|
| 6 GHz  |*client*|**dead, not support**|

SW / NO offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |MASTER (AP)|live|
| 5 GHz  |*client*|live (full up/dwn throughtput)|
| 6 GHz  |MASTER (AP)|live (**requires 2.4GHz lives first**)|

HW offload
| Radio   |      Mode      |  Result |
|:---------|:-------------|:------|
| 2.4 GHz |MASTER (AP)|live|
| 5 GHz  |*client*|live (full up/dwn throughtput)|
| 6 GHz  |MASTER (AP)|**dead, not support**|

---
### apps pre-loaded in this build

| Names   |      Remarks      |
|----------|:-------------:|
|luci-app-airoha-flowsense||
|luci-app-airoha-npu|without devmem mode exposed for security concern|
|luci-app-w1700k-fancontrol|
|luci-app-wol|
|luci-app-usteer|for managing 802.11 k/v/r in Mesh|
|~~wpad-basic-mbedtls~~ wpad-wolfssl|full mesh support to 802.11 k/v/r/s
|~~dnsmasq~~ dnsmasq-full|prerequisite of certain VPN software|
|luci-app-tailscale-community|VPN app|
|luci-proto-wireguard|VPN app|
|kmod-nft-socket|prerequisite of certain proxy software|
|kmod-nft-tproxy|prerequisite of certain proxy software|
|kmod-inet-diag|prerequisite of certain proxy software|
|kmod-netlink-diag|prerequisite of certain proxy software|
|kmod-mtd-rw|for unlocking and updating mtd0 (the chainloader)|


