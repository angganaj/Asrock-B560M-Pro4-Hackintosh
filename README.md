# Asrock B560M Pro4 Hackintosh
<!--
- [Spek](#spek)
- [Kexts](#kexts-used)
- [boot-args](#gpu-specific-boot-args)
- [Special notes](#special-notes)
- [Work & Not](#work--not)
- [BIOS settings](#bios-settings)
    - [For Intel 11th gen CPU users](#for-intel-11th-gen-cpu-users)
- [Map your USB](#map-your-usb)
- [References & thanks](#references--thanks)
-->

<p align="center"><img src=https://www.asrock.com/mb/photo/B560M%20Pro4(M2).png></p>
<p align="center"><img src=img/cs1.png></p>
<p align="center"><img src=img/bm.jpg></p>

<br><br>
# Spek :
| Spek | Type  |
| -------------     | ------------------------------ |
| CPU               | [Intel i5-10400F](https://www.intel.com/content/www/us/en/products/sku/199278/intel-core-i510400f-processor-12m-cache-up-to-4-30-ghz/specifications.html) |
| CPU Fan           | [Noctua NH-L9X65](https://noctua.at/en/nh-l9x65) |
| Motherboard       | [ASRock B560M Pro4 ](https://www.asrock.com/mb/Intel/B560M%20Pro4/index.asp) |
| RAM               | [GSkill 32 GB](https://www.gskill.com/product/165/184/1536125673/F4-3000C14Q-32GVR-EOL) |
| VGA               | [Sapphire RX 5600 XT](https://www.sapphiretech.com/en/consumer/pulse-radeon-rx-5600-xt-6g-gddr6) |
| remot on-off      | [Ewelink Wifi Smart Switch](https://aliexpress.com/i/33042974681.html) |
| NVME              | [WD SN350](https://www.westerndigital.com/products/internal-drives/wd-green-sn350-nvme-ssd#WDS240G2G0C) |
| WiFi & Bluetooth  | [Fenvi T919](https://www.fenvi.com/product_detail_16.html) |

<br><br>

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

# Kexts used:
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

<br><br>

# GPU Specific `boot-args`
Parameter|Description
|--|--|
agdpmod=pikera|Used for disabling board ID checks on Navi GPUs(RX 5000 series), without this you'll get a black screen.<br>**Don't use if you don't have Navi** (ie. Polaris and Vega cards shouldn't use this).
alcid="XX'' | layout 11, 12, 23, 66, 69, 77

<br><br>

# Special notes
- USB port mapping is **REQUIRED**. [Guide](https://dortania.github.io/OpenCore-Post-Install/usb/intel-mapping/intel.html)
- **`XhciPortLimit`** - Needed **`DISABLE`** if you use Big Sur 11.3+. 
	- Please Mapping USB in macOS Catalina before install Big Sur or Newer for best results.[USBPorts.kext](https://github.com/USBToolBox/kext)	
- **`AppleXcpmCfgLock`** - Please **`ENABLE`** if you cannot disable`CFG-Lock` in BIOS.
- Does NOT SUPPORT iGPU in 11th Gen.
- You NEED dGPU (dedicated/discrete GPU (eg. RX 560, 570, 580, 590, RX 5700 XT, etc).

<br><br>

# Work & Not

# ✅
* QE/CI
* CPU Power Management
* Restart, Sleep and Shutdown
* Internal Speaker, Mic, Headphone Audio
* iMessage and FaceTime
* Handoff and Continuity
* Ethernet
* WiFi
* HDMI DP Output
* HDMI DP Audio
* All USB Ports
* Etc

# ❌
- not yet found

<br>

# BIOS settings
**Enable**

* Intel Virtualization Technology (VT-x)
* Multi-processor
* UEFI Boot
* Intel VT-d (or set `DisableIoMapper` in the `config.plist` to `FALSE`
* SATA Mode to AHCI
* XHCI Handoff
* Above 4G Decoding and Clever Access Memory (or set `ResizeAppleGpuBars` to `-1`)

**Disable**

* Legacy ROM support
* Secure Boot
* Intel SGX

<br>

# For Intel 11th gen CPU users
Your iGPU will not be supported in macOS due to Apple's transistion to Apple Silicon, so you can skip the iGPU configuration step. Using an F-series CPU would be beneficial here.

Also, 11th Gen CPUs are required to change the CPUID by adding these entries under `Root > Kernel > Emulate` as Apple also doesn't support them out of the box:

| Key | Type | Value |
| --- | --- | --- |
| Cpuid1Data | Data | \<EA060900000000000000000000000000\> |
| Cpuid1Mask | Data | \<FFFFFFFF000000000000000000000000\> |
| DummyPowerManagement | Boolean | 0 |
| MaxKernel | String | |
| MinKernel | String | |

<br>

## Config your iGPU
Not required if you don't have one. [**Follow these instructions**](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#deviceproperties).

<br>

## Map your USB
Using [**USBToolBox**](https://github.com/USBToolBox/tool) is recommended.
Map your ASM107x USB controller (entries 2.0 and 3.0) as type `255` (Internal) as those two stay on all the time.

**Note:** You must exclude your RGB controller during the mapping process, as it will cause sleep problems and the RGB LEDs will freeze until you fully halt the machine.

## Add your own `PlatformInfo` entries using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
Use:
* `iMac20,1` if you have an 8-core or lower CPU with an iGPU (ie. i7-10700)
* `iMac20,2` if you have a 10-core CPU (ie. i9-10900)
* `iMacPro1,1` (or `MacPro7,1` with the [**RestrictEvents**](https://github.com/acidanthera/RestrictEvents) kext) if you don't have an iGPU (ie. AMD dGPU with a F-series CPU such as the i5-10400F like me). 

<br><br>

# helpful app
- [Hackintool](https://github.com/benbaker76/Hackintool)
- [About This Hack](https://github.com/0xCUB3/About-This-Hack)
- [balenaEtcher](https://github.com/balena-io/etcher)
- [OCAuxiliaryTools](https://github.com/ic005k/OCAuxiliaryTools)
- [Stats](https://github.com/exelban/stats)

<br><br>

# References & thanks
- [Apple inc](https://www.apple.com/)<br>
- [dortania.github.io](https://dortania.github.io/OpenCore-Install-Guide/config.plist/comet-lake.html#starting-point)<br>
- [olarila.com](https://www.olarila.com/)<br>
- [HackintoshLover](https://t.me/HackintoshLover)<br>
