Unlike other android devices,
Huawei devices using Kirin chips have their unique partition layout and unique boot process.

iflytek device BZT-W09 uses huawei mediapad c5.Iflytek does not change any huawei boot process and lowlevel system compnets.

iflytek just uses huawei's providing version and userdata partiton to realize its limited system.

iflytek does not change any partition except version and userdata partition.

So ,the iflytek system is the same as C00 normal system.

But it just changes version partition to use xml and txt to disable and enable some configurations,and changes userdata partition to install its own software and encrypt the userdata  partition
 using AES. But the encryption keys are in the normal world ,not secure world.
 
 Huawei uses GPT partition table and it does not use standard UEFI boot.
 
#### Huawei Kirin boot process:
  BootROM(PBL): initalize LPMCU and SRAM.
  
  the PBL checks the signature of xloader and loads xloader.
  
  The xloader checks the signature of uce or fastboot and loads uce/fastboot
  
  For Kirin 659(BZT-W09) ,there is no uce,so xloader directly loads fastboot.
  
  Huawei uses its own secure boot .
  
  the signature's algorithm is SHA256(hard to hack)
  
  It is stored in OTP(efuse) ,a read-only area.
  
  Once it is written,it can not be rewritten again.
  
  So we can not rewrite the signature.
  
  Huawei will check the signature during booting,if it does not match,the device will not boot.
  
  The signature keys are produced by huawei and it is secret ,so we can not know it.
  
  The signature keys for same model share the same.
  
  But OTP also has a special area , it can only be increased but can not be decreased.
  
  It stores your version number.
  
  So You can only upgrade to newer versions , but can not roll back ( But for some devices ,this aren't configured well)
  
  It also stores the main version number(C923)
  
  So without bootloader unlock ,you should not flash C00 normal system ,or your device may be bricked.
  
  In fastboot the Main ACPU(CPU) will initalize.
  
  And real RAM initalizes.
  
  fastboot teeos xloader PBL all run in EL3.
  
  fastboot will check the dts(device tree) partition's signature and load it.
  
  The device tree iss like computer's drivers.
  
  It stores the screen  and other hardware's drivers info.
  
  So if it is incompatible , the screen will not turn on.
  
  Different model of devices 's dts is not compatible.
  
  Same model but different version's dts is not compatible.
  
  But for BZT-W09 ,we find some interesting things.
  
  Same version and same model, but the dts for different devices maybe incompatible!
  
  So we need to backup our dts before doing any flashing to make sure your device can be recovered.
  
  After loading dts , the fastboot will check whether bootloader is unlocked(we are not sure if bootloader is unlocked ,the dts's signature is still checked)
  
  If bootloader is unlocked , it can load any kernel and ramdisk.
  
  But if it is locked , it can only load kernel and ramdisk with huawei own signature.
  
  This is called USERLOCK
  
  It can be unlocked for Kirin 960 and older except Kirin 710 and Kirin 710a.
  
  You need the device unlock code to unlock device.
  
  You need use "fastboot oem unlock unlock_number" to unlock  your device.
  
  The unlock_number is 16 length number.
  
  It isn't stored in the device.
  
  But its SHA256 is stored in nvme partition.
  
  So we can rewrite nvme partition to use our own unlock number.
  
  If bootloader is unlocked ,or the signature matches , the device starts to load kernel and ramdisk.
  
  the ramdisk will; start init process to load Android system.
  
  The system  partition is the main Android system.
  
  Then the common Android boot process is done.
  
  For iflytek BZT-W09
  
  iflytek will load the StudentLaucher as desktop.
  
  And it uses huawei mdm service to start controlled system.
  
  So if we can modify version and userdata partition,we can use C00 normal system without other changes.
  
  ##### Recovery Mode
  
  For EMUI8.0, recovery's kernel and the normal system's kernel share the same.
  
  If kernel loads success, but ramdisk loads failed.
  
  The device will boot into recovery mode using recovery_ramdisk partition.
  
  In recovery ,we can do factory reset, but  Huawei official recovery has very limited functions.
  
  However, Iflytek forbids factory reset.
  
  But the recovery's signature is still checked in fastboot.
  
  ##### Fastboot Mode
  
  Huawei uses Android fastboot protocol
  
  But in fact ,it is quite different.
  
  Huawei's fastboot runs in EL3,but it loads kernel in EL! and the normal system runs in EL1.
  
  Its fastboot has very limited functions.
  
  fastboot reset
  
  fastboot oem get-bootinfo( USERLOCK state)
  
  fastboot oem lock-state info (USERLOCK state and FBLOCK state)
  
  fastboot flash (if FBLOCK locked ,can only flash recovery_ramdisk recovery_vbmeta vbmeta system ramdisk kernel userdata, if not locked ,it can flash any partitions)
  
  fastboot erase( the same as above)
  
  
  In fastboot ,we can recover bricked devices, or  flash different systems.
  
  But to enable full fastboot function ,We need to unlock FBLOCK
  
  FBLOCK state is stored in nvme partition.
  
  So we can rewrite it to unlock FBLOCK.
  
  
  But in normal fastboot ,we can not modify nvme partition.
  
  
 Fastboot also shows the unlocked warning if USERLOCK is unlocked and it cannot be disabled unless your lock the USERLOCK again.
 
 ##### eRecovery Mode
 
 Almost same as recovery partition 
 
 But it has its own kernel and vendor 
 
 erecovery_kernel
 
 erecovery_vendor
 
 erecovery_ramdisk
 
 erecovery_vbmeta
 
 ##### Download Mode (VCOM Mode)
 
 It is the most important part.
 
 We can short the testpoint in the mother board.
 
 Then we can enter the VCOM Mode.
 
 In this mode ,we can upload any xloader and fastboot without check.
 
 So we can load factory fastboot to modify partitions.
 
 Then we can unlock FBLOCK and rewrite the unlock code.
 
 It gives a connection between computer and device.
 
 It doesn't depend on any partition but on PBL.
 
 But for Kirin 970 k710 710a 980 990 , VCOM will also check the signature of xloader and fastboot ,but it has many bugs ,so we can still hack it.
 
 But newest research has reported it.
 
 So huawei disabled VCOM Mode during an OTA update for this chips.
 
 Fortunately, BZT-W09 is not affected.
  
