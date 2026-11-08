
## Limitations / bugs

The main OS *.itb binary is in ubi 2.0 layout. Users need a corresponding ubi 2.0 chainloader as well. Please check out the repos on [naoki66](https://github.com/naoki66/Gemtek-brightspeed-chainloader/releases), [YYH2913](https://github.com/YYH2913/http-uboot/releases) or [hurrian](https://github.com/hurrian/w1700k-ubi-installer/releases). Please **DO NOT** use any chainloader compiled from this build.

---
### Toggle HW / SW Offload:
It is recommended to control it by the Airoha FlowSense app button rather than the built-in Firewall page because the app includes extra part on this control function. Also, It is recommended to disable Packet Steering on the Interface page if you turn on HW Offloading.

---
### MT76 (MT7996AV + MT7976GN + MT7977AN + MT7977BN) 6GHz radio driver bugs in certain scenarios:
Due to various bugs in different upstream driver versions, the 6 GHz radio sometimes cannot be activated, especially in CLIENT mode.
Please refer to each release for detail, each release situation is different.



---
### apps pre-loaded in this build

| Names   |      Remarks      |
|----------|:-------------:|
|luci-app-airoha-flowsense||
|luci-app-airoha-npu|without devmem mode exposed for security concern|
|luci-app-w1700k-fancontrol|
|luci-app-wol|
|luci-app-usteer|for 802.11 k/v/r roaming management|
|~~wpad-basic-mbedtls~~ wpad-wolfssl|for full roaming / mesh support on 802.11 k/v/r/s
|~~dnsmasq~~ dnsmasq-full|prerequisite of certain proxy / VPN software|
|luci-app-tailscale-community|VPN app|
|luci-proto-wireguard|VPN app|
|kmod-nft-socket|prerequisite of certain proxy software|
|kmod-nft-tproxy|prerequisite of certain proxy software|
|kmod-inet-diag|prerequisite of certain proxy software|
|kmod-netlink-diag|prerequisite of certain proxy software|
|kmod-mtd-rw|for unlocking and updating mtd0 (the chainloader partition)|


