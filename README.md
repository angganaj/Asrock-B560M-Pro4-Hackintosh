# Asrock B560M Pro4 Hackintosh
#
<p align="center"><img src=https://www.asrock.com/mb/photo/B560M%20Pro4(M2).png></p>
<p align="center"><img src=img/cs1.png></p>
<p align="center"><img src=img/bm.jpg></p>

# Spek :
| Spek | Type  |
| -------------     | ------------------------------ |
| CPU               | [Intel i5-10400F](https://www.intel.com/content/www/us/en/products/sku/199278/intel-core-i510400f-processor-12m-cache-up-to-4-30-ghz/specifications.html) |
| CPU Fan           | [Noctua NH-L9X65](https://noctua.at/en/nh-l9x65) |
| Motherboard       | [ASRock B560M Pro4 ](https://www.asrock.com/mb/Intel/B560M%20Pro4/index.asp) |
| RAM               | [GSkill 32 GB](https://www.gskill.com/product/165/184/1536125673/F4-3000C14Q-32GVR-EOL) |
| VGA               | [Sapphire RX 5600 XT](https://www.sapphiretech.com/en/consumer/pulse-radeon-rx-5600-xt-6g-gddr6) |
| remot on-off      | [Ewelink Wifi Smart Switch](https://aliexpress.com/i/33042974681.html) |
| NVME              | [XPG SX8200 Pro](https://www.xpg.com/us/xpg/583) |
| WiFi & Bluetooth  | [Fenvi T919](https://www.fenvi.com/product_detail_16.html) |


# Kexts used:
<!--
- [AppleALC.kext](https://github.com/acidanthera/AppleALC)
- [IntelMausi.kext](https://github.com/acidanthera/IntelMausi)
- [Lilu.kext](https://github.com/acidanthera/Lilu)
- [RestrictEvents.kext](https://github.com/acidanthera/RestrictEvents)
- [SMCProcessor.kext](https://github.com/acidanthera/VirtualSMC)
- [SMCSuperIO.kext](https://github.com/acidanthera/VirtualSMC)
- [USBPorts.kext](https://github.com/USBToolBox/kext)
- [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC)
- [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen)
- [XHCI-unsupported.kext](https://github.com/johnlimabravo/XHCI-unsupported)
-->

Kext|Description|for
|--|--|--|
[AppleALC.kext](https://github.com/acidanthera/AppleALC/releases)|Used for AppleHDA patching, allowing support for the majority of on-board sound controllers.|Audio
[IntelMausi.kext](https://github.com/acidanthera/IntelMausi/releases)|Intel's 82578, 82579, I217, I218 and I219 NICs are officially supported.| Ethernet
[Lilu.kext](https://github.com/acidanthera/Lilu/releases)|Patch many processes, required for AppleALC, WhateverGreen, VirtualSMC and many other kexts.
[SMCProcessor.kext](https://github.com/acidanthera/VirtualSMC/releases)|Used for monitoring CPU temperature, doesn't work on AMD CPU based systems.
[SMCSuperIO.kext](https://github.com/acidanthera/VirtualSMC/releases)|Used for monitoring fan speed, doesn't work on AMD CPU based systems.
[VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC/releases)|Emulates the SMC chip found on real macs, without this macOS will not boot.<br>Alternative is FakeSMC which can have better or worse support, most commonly used on legacy hardware.
[WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)|Used for graphics patching, DRM fixes, board ID checks, framebuffer fixes, etc; all GPUs benefit from this kext.
[NVMeFix](https://github.com/acidanthera/NVMeFix/releases)|Used for fixing power management and initialization on non-Apple NVMe.|NVMe device
[SATA-Unsupported](https://github.com/khronokernel/Legacy-Kexts/blob/master/Injectors/Zip/SATA-unsupported.kext.zip)|Adds support for a large variety of SATA controllers, mainly relevant for laptops which have issues seeing the SATA drive in macOS.<br>We recommend testing without this first.
[RestrictEvents](https://github.com/acidanthera/RestrictEvents/releases)|Better experience with unsupported processors like AMD, Disable MacPro7,1 memory warnings and provide upgrade to macOS Monterey via Software Updates when available.

# GPU Specific `boot-args`
Parameter|Description
|--|--|
agdpmod=pikera|Used for disabling board ID checks on Navi GPUs(RX 5000 series), without this you'll get a black screen.<br>**Don't use if you don't have Navi** (ie. Polaris and Vega cards shouldn't use this).

# Special notes

- USB port mapping is **REQUIRED**. [Guide](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html)
- **`XhciPortLimit`** - Needed **`DISABLE`** if you use Big Sur 11.3+. 
	- Please Mapping USB in macOS Catalina before install Big Sur or Newer for best results.[USBPorts.kext](https://github.com/USBToolBox/kext)	
- **`AppleXcpmCfgLock`** - Please **`ENABLE`** if you cannot disable`CFG-Lock` in BIOS.
- Does NOT SUPPORT iGPU in 11th Gen.
- You NEED dGPU (dedicated/discrete GPU (eg. RX 560, 570, 580, 590, RX 5700 XT, etc).


### GPU-Specific `boot-args`
Parameter|Description
:----|:----
agdpmod=pikera|Used for disabling board ID checks on Navi GPUs(RX 5000 series), without this you'll get a black screen.<br>**Don't use if you don't have Navi** (ie. Polaris and Vega cards shouldn't use this).
# Working ✅:
* QE/CI
* CPU Power Management
* Restart, Sleep and Shutdown
* Internal Speaker, Mic, Headphone Audio
* Ethernet
* WiFi
* HDMI DP Output
* HDMI DP Audio
* All USB Ports
* Etc

# Not Working ❌:
- not yet found


# References & thanks
- [Apple inc](https://www.apple.com/)<br>
- [dortania.github.io](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#starting-point)<br>
- [olarila.com](https://www.olarila.com/)<br>
- [HackintoshLover](https://t.me/HackintoshLover)<br>