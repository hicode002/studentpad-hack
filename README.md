# studentpad-hack
some hacks for studentpad for example bzt-w09 ags2-w09 x1pro

This is used to analyze studentpad such as bzt-w09 ags2-w09 x1pro and find bugs to get a better solution.
These pads have specific systems and protections for only studying so that analyzing them is useful.

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
      BZT-W09:
        VCOM_ENTER successful
        BOOTLOADER_UNLOCK successful
        TWRP_RECOVERY successful
        NORMAL_OS successful
        BACKUP_ORIGIN_OS successful without initial iflytek userdata.img(view in origin_os folder's README.md)
        DUAL_BOOT_ANDROID  successful
        SECURE_BOOT_DISABLED continueing and hard to achieve
        ORIGIN_OS_HACK Origin OS hack successful,but origin iflytek software hack isn't started now.
        COMPLETELY_BOOT_FROM_SDCARD hard to achieve(almost impossible)
        KVM_ENABLED not start
        INSTALL_POSTMARKETOS continueing
  
  
    Other chips:
         Kirin710:
            BOOTLOADER_UNLOCK may work ,not tested , view 710unlock.7z
         Some ROMs have been uploaded, view Releases for more information.
   
