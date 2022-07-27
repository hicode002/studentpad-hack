```
push parted to bzt-w09:
  uncheck the system write protection in twrp before mounting system.
  mount system.
  connect device to computer.
  use "adb push parted /system/bin/parted"
  then use"adb shell"
  then use "chmod 755 /system/bin/parted"
  then you can use!
parted:
  use "parted /dev/block/xxx" to enter.
  mklabel : remake partition table for the disk (will lose all the data),input msdos for mbr ,gpt for gpt.
  print :print partition table
  quit :exit parted and save changes
  unit : change the display unit of print command(B KB MB GB TB)
  mkpart: mkpart partition_name filesystem start_sector end_sector
  rm: delete partitions
  
 How to format partitions:
  mkfs.fat
  mkfs.ntfs
  mkfs.ext2
  mkfs.ext4 (may not exist)
  
  make_ext4
  make_f2fs
  
  
  ```
