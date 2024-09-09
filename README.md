# lenovo-miix-520-hackintosh
[README](README.md) | [中文文档](README_zh.md)

MiiX 520 MacOS EFI
Boots 10.14.x - 15.X.X Beta.

Thanks  [jamesxxx1997](screw pcbeta and their invite system, no link xD) for translating into English.


#### Index

1. Hardware configuration
2. System Screenshot
3. What is working
4. What is not working
5. Bug and solution
	NONE DETECTED YET, missing sleep when lid closed atm, will update soon.
6. Release version
7. Comon FAQ
	- 1:Pre-install preparation - Make a new EFI partition if on a blank SSD, copy root of this folder, install MacOS from any thumbdrive, but boot from SSD.
	- 2:Why touchscreen cannot use after installation? - Is SSDT-TPL1 enabled in Opencore Configurator?
	- 4:Can I update the system? - Yes, at the moment, at least.
	- 5:Can I use SD card reader? - Yes, install the Sinetek-rtsx.kext in the OC/Kexts folder and enable in OC Configurator.
	- 6:How to use wifi and Bluetooth？ - Broadcom and Intel Wifi + Bluetooth supported.


## 1.Hardware configuration

- Machine type model ：Lenovo MiiX 520
- cpu：i5 8250u 
- iGPU：uhd620
- RAM：8G
- Sound：alc298
- WIFI card：Intel 8265
- Display：12.2" FHD
- Resoution：1920x1200
- NVME SSD：Crucial 1TB
- bios：6NCN39WW

## 2.System screenshot

- OpenCore bootloader screenshot：
<div align=center><img src="https://raw.githubusercontent.com/acai66/lenovo-miix-520-hackintosh-CLOVER/master/Resource/images/OpenCoreBootloader.png" width="95%" /></div>

- Mac OS screenshot：
<div align=center><img src="https://github.com/DosDokTor/lenovo-miix-520-ventura/blob/DosDokTor-patch-1/MacOS15.png" width="95%" /></div>

## 3.What is working

1. Sound card / iGPU / wifi card：OK
2. usb：OK
3. battery status：OK
4. brightness control：OK
5. CPU frequency control：OK
6. Sleep when lid closed/Awake when lid opened：Not Yet/Will be fixed soon.
7. Touchscreen , active stylus：OK
8. bluetooth：OK
9. wake up by usb mouse and keyboard：OK
10. SD card reader : Copy Sinetek-rtsx.kext in /EFI/OC/Kexts and enable the kext in OC Configurator
## 4.What is not working

1. I2C pressure sensitivity (No solution)
2. Camera (No solution)
3. iMessage（solution）
4. Fingerprint reader (No solution)

## 5.bug and solution

### bug1: Touchpad and touchscreen cannot use simultaneously

No longer present, works as of 31/05/2023.

### bug2: After wake from sleep , keyboard type cover not working （will work again after unplug/replug）

No longer present, works as of 31/05/2023, confirmed to wake the system too. 

## 6.release version

### v4.0 -- 2024-09-08 - Queen Elizabeth II Edition
- Opencore 101 Update for macOS Sequoia Beta 6. 

### v3.0 -- 2023-05-31
- Update the latest OpenCore and drivers, and support the latest macOS 13.5 Beta 2

### v2.5 -- 2020-12-15
- Update the latest OpenCore and drivers, and support the latest macOS 11.0.1.
- CLOVER will be deprecated.
- Add Intel wifi and BT support.
- Enable Apple Secure Boot.


### v2.5 beta -- 2020-07-02
- Update the latest OpenCore and drivers, and support the latest macOS 11.0 (10.16).
- Fix hotkeys in opencore GUI.

### v2.4 -- 2020-05-22
- Update the latest CLOVER, OpenCore and drivers, and support the latest macOS 10.15.4
- Support hotkeys and touchscreen in opencore GUI.
- Fix missing battery in settings->energy saver.

### v2.3 -- 2020-04-09
- Update the latest CLOVER, OpenCore and drivers, and support the latest macOS 10.15.4
- Support opencore GUI.

### v2.2 -- 2020-03-13
- Update the latest CLOVER, OpenCore and drivers, and support the latest macOS 10.15.3
- Support opencore startup audio.

### v2.0 -- 2020-01-02 -- machine translation
- Update the latest CLOVER, OpenCore and drivers, and support the latest MacOS 10.15.2
- A large number of OpenCORE configurations are optimized, starting from this version, i will mainly update the opencore bootloader.
- Fix USB configuration and iPad charging problem
- Changing the WiFi country to NZL will support more 5GHz WiFi bands without affecting 2.4GHz bands.
- Update the solution to the problem of bug2, test support Mac OS 10.15
- Note 1: if the OC boot does not automatically scan out the windows or Linux boot items, please manually add the boot configuration to the config.plist of the OC.
- Note 2: the ACPI and other patches in the OC will take effect on all systems, so windows booted by the OC will recognize the model as MacBook Pro, and will also support the startup disk switching of the native Mac OS (to be tested).
- Note 3: Recently, a lot of changes have been made for hotpatch OC. My side is normal at present. If there is any abnormal bug, please send issue. I am the American version of Miix 520, and the BIOS version of 6ncn35ww. Some hotpatch patches depend on the DSDT table in the BIOS, so the BIOS version is best consistent.

### v1.9 -- 2019-08-23
- Update the latest self-compiled clover and drivers to support the latest macOS 10.15 beta 6
- Update the latest self-compiled OpenCore
- Further streamlining redundant hotpatch patches
- Adding ssdt-usbx.aml to avoid potential USB power problems
- Note 1: If the touch screen fails after updating the beta6 system, run kext utility to repair the permission and rebuild the cache
- Note 2: config.plist in Clover and OpenCORE have been added brcmfx-country=CN to support 12 and 13 WiFi bands of 2.4 ghz, but this will cause the lack of 5 GHz WiFi band. brcmfx-country=US supports more 5 GHz bands, but there are no 12 and 13 bands. Wifi band reference [wiki](https://zh.wikipedia.org/wiki/WLAN信道列表), the actual available bands should be tested by yourself.

### v1.8 -- 2019-07-16
- Update clover version
- Update driver version,support macOS 10.15 beta3
- fix bug2 in new macOS10.15
- OC boot loader will be updated in v1.9

### v1.6 -- 2019-05-15

- Fix power management、use ssdt hotpatch or devices property to inject sound card layout id kext
- dd cpufriend , dynamically inject macOS CPU power management data , change the lowest frequency from 1.3ghz to 800mhz , saving more electricity when computer is unused
- Streamlined some redundant kext
- Update kext and clover version
- 取消仿冒6代u与核显，据说可以实现显卡硬解；
- Fix the battery dsdt patch logic , but cannot feel any difference with this fix
- Cancel verbose mode(-v) in clover bootloader
- Provide dsdt.aml under ACPI/patched/WINDOWS/ , in order to fix the problem which USA version of miix 520 cannot recognize fingerprint under newer version of bios (for windows system)
- Test and add OpenCore bootloader , it is not complete so it is only for testing and not recommended in daily usage.

### v1.5 -- 2019-04-05

- Fix the multitouch gesture of touchscreen

### v1.4 -- 2019-03-29

- Update clover version
- Update driver version
- Streamline the redundant file in driver64uefi and kexts.
- Fix iGPU kext and keep macos i2c kext from loading.

### v1.3 -- 2019-01-26

- Update clover version。
- Add boot sound [常见问题解答7](https://github.com/acai66/lenovo-miix-520-hackintosh-CLOVER#7开机声音怎么开启与关闭)。
- Modify battery model information to miix 520，an update without pratical significance.
- Do not add SD card reader kext by default , to manually add it ,look [常见问题解答8](https://github.com/acai66/lenovo-miix-520-hackintosh-CLOVER#8读卡器能驱动吗)。


### v1.2 -- 2018-12-30

- Replace VirtualSMC.kext with fakesmc.kext
- Replace SMCBatteryManager.kext，with ACPIBatteryManager.kext
- Update clover option to 4831
- Update the version of kexts
- Set iGPU fake id 19168086，solve the problem: water ripple when creating widget in dashboard
- Test adding SD card reader kext

### v1.1 -- 2018-10-14

- Change the brightness control way to AppleBacklightFixup，[check for more](https://bitbucket.org/RehabMan/applebacklightfixup)。
- Set the boot option : automatically boot last booted volume after 10 seconds.

### v1.0 -- 2018-10-11

- Original version.

## 7. Comon FAQ

### 1: Pre-install preparation

1. Create USB installer , using a flash drive which have capacity bigger than 8GB；
2. A partition in hard drive for mac；The ESP(EFI system partition) should bigger than 200mb；
3. Bios setting : boot mode is uefi ; disabled the secure boot
4. A disk image for macos mojav
5. Create install media with a tool that burn the disk image to USB drive , recommend [etcher](https://www.balena.io/etcher/)
6. After creating usb drive , replace the OC file , which is in the Esp partition of USB drive , with the OC in github
7. After the installation , add clover boot options for all entries。
	

### 2: Why touchscreen cannot use after installation?
A: This bug might result from voodooi2c.kext interruption with system i2c kext or fail to inject kext. After installation , please restart again , if the touchscreen still can not use , please manually remove the AppleIntelLpssI2C.kext and AppleIntelLpssI2CController.kext and run kext utility to rebuild your kextcache , then test the touchscreen again.

### 3: Why after wake up from sleep mode , keyboard type cover not working?
A: please look up to the “bug and solution” part in readme

### 4: Can I update the system
A: Theoretically , you can update system without a doubt.


### 5: Can I use SD card reader?
A: The SD card reader kext isn’t added by default , for it is not stable , having issues with boot or something. The SD card reader kext is Sinetek-rtsx.kext is said to have issues. If you have problem with it , please compile the kext by yourself，[Sinetek-rtsx](https://github.com/sinetek/Sinetek-rtsx)

### 6: How to use wifi and Bluetooth？
A: Testing support for intel wifi card, but for better experience it’s recommend wifi card like bcm94352z Lenovo version, and it is not recommend to use usb wifi dongle for unstability.

