# studentpad-hack
some hacks for studentpad for example bzt-w09 ags2-w09 x1pro bzc-w00 bzi-w00 c3 c5 c6 c8

This is used to analyze studentpad such as bzt-w09 ags2-w09 x1pro and find bugs to get a better solution.
These pads have specific systems and protections for only studying so that analyzing them is useful.

#### View ![exploit/README.MD]exploit/readme.md!! I have new Kirin710A exploit using CVE!!
### DISCLAIMER:
  This is a free program that isn't allowed to be sold or use for business.
  
  Everyone can edit it if it has  good ideas.
  
  This is just for studying.
  
  Our final purpose is to solve the bugs and find better solutions for security,not just to hack.
  
  All of our actions must be in law.
  
  We promise we will not do anything illegal and damage any organizations' or company's profits.
  
  If you use our programm to do illegal things, I will not take any responsibility.
  
  If you brick your phone or tablet , I will not take any responsibility.
  
  If you want to share your ideas or make any changes ,please use English.
  
  
  Anyone who wants to edit it needs to contact me, then I will give him/her the permission to edit this repo.
  
  o81018o is also an editor of this repo.
  
  He also publishes Chinese guides.
  
  view docs/other_docs.md to view them.
  
  2022.8.20
  
  Start to write full docs 
  #### New progress on 2022.8.17
  #### New Progress on 20250509
  This is a repo collecting studentpad hacking,such as unlocking bootloader ,dual boot,getting root access,flashing back to normal system.
  Now We can use checkm30 bootrom exploit to get Huawei Mediapad C3(BZC-W00) into normal system and getting temporary bootloader unlocking
  This repo now supports
  Huawei BZT-W09
  Huawei AGS2-W09
  Huawei BZC-W00
  Huawei BZI-W00
  and all devices with kirin 960 and lower
  or Kirin 710,Kirin 710A,Kirin970,Kirin 980(not tested)

  Now we can achieve:
  Flash to normal system 
  
  Get temporary bootloader unlock(fblock)
  
  Permanently unlock bootloader with EMUI9 and lower
  
  Dump partitions via patched fastboot(Kirin710,Kirin 960 and lower)

  To get C00 firmware,view https://professorjtj.github.io/

  For more details about checkm30 bootrom exploit and flashing procedure,view docs/.
  
  ### PROGRESS MADE NOW
    Maintaining devices:
      BZT-W09/BAH2-W09/BZC-W00/BZI-W00:
        VCOM_ENTER successful
        BOOTLOADER_UNLOCK successful,but for BZC-W00 and BZI-W00,can only get temporary unlock
        TWRP_RECOVERY successful
        NORMAL_OS successful
        BACKUP_ORIGIN_OS successful without initial iflytek userdata.img(view in origin_os folder's README.md)
        DUAL_BOOT_ANDROID  successful
        ROOT_ACCESS for BZT-W09/BAH2-W09,persistent root.for BZC-W00/BZI-W00,temporary root.(Or use kernel exploit to get root,but is still temporary)
        SECURE_BOOT_DISABLED temporary successful,but can not persistently disable it(may need an oeminfo exploit)
        ORIGIN_OS_HACK Origin OS hack successful,but origin iflytek software hack isn't started now.
        COMPLETELY_BOOT_FROM_SDCARD there is no need to achieve that.We can use kexec-hardboot or just edit vendor/init.rc
        KVM_ENABLED can be achieved,but need a KVM-ENABLED kernel.
        INSTALL_POSTMARKETOS not planned

      Onion Q20/Onion S20/Onion S30:
        use mediatek devices.
        Can be exploited by bootrom vulnerabilities
        Use mtkclient to dump partitions and unlock bootloader
        BOOTLOADER LOCK STATE stored in seccfg,can be rewritten.
        Flashing GSI works
        BOOTROM_ENTER successful
        PRELOADER_ENTER partial,because some sla enabled devices can not handshake in preloader mode
        TWRP_RECOVERY I do not know the partition where recovery stores in
        NORMAL_OS successful,flash GSI.for Q20,use android 11.For S20,use android 12.For S30,use android 10/12.
        ROOT_ACCESS successful
        BACKUP_ORIGIN_OS successful,just use mtkclient
        DUAL_BOOT_ANDROID not tried,need sdcard or repartition gpt.
        ORIGIN_OS_HACK can be achieved easily by repacking super,but not tried
        KVM_ENABLED not tried,but can use mtkclient or lk-patch to achieve that.
        SECURE_BOOT_DISABLED mtkclient for temporary,patching lk can achieve persistent bypass.But to replace trustfirmware or other low-level bootloader,we need sbc disabled or a preloader exploit(CVE 2023,not tried)
        INSTALL_POSTMARKETOS hard to achieve,because no kernel source.

      
  
  
    For Kirin 710,it shares the same exploit address with Kirin 710A.No need to use any board firmware.
   
