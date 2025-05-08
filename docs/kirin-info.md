For Kirin 960 and older ,they use old codebase.Their secure boot signature is different from newer socs'.And they stock USERLOCK state in oeminfo
with storaging the aes encrypted data(encryption key is USRKEY) of specified strings ABABCDCD(EF) for unlocked,EFEFABCD(EF) for relocked.,others for locked.
And USRKEY stores in nvme,it is sha256 of the unlock code.
And FBLOCK state stores in nvme.
So the unlock code can be written.

For Kirin 710,710A,980 and newer,if the initial version of EMUI is EMUI9 or older,there exists permanent unlocking method.Although they encrypt oeminfo and nvme
partition,but if we use patched fastboot to force to run oeminfo_lock_stat_write(1),you can unlock bootloader.
For FBLOCK,they add a lot of limits.If you want to get fblock unlocked,you need to make the value of rd_lock 1 which stores in oeminfo but encryted with hmac or rsa
algorithm.If you just write FBLOCK state in nvme,you also need to make sure the secure_debug value stored in efuse is zero.fastboot will check both values.

And huawei leaves a special method to get temporary FBLOCK unlock.
fastboot oem hwdog certify begin
or fastboot oem hwdog certify enc begin
then you will get a token.If you have the rsa private keys of huawei,you can sign the token and save it into slock.bin
then fastboot flash slock slock.bin to get fblock unlocked.
This is why there exists a lot of paid tools to get temporary bootloader unlock.(leaked rsa keys maybe illegal)

For EMUI10 and newer,the USERLOCK is written to be locked in fastboot images.So this means you cannot get bootloader unlocked permanently without replacing fastboot with
factory unlocked one.But FBLOCK can be unlocked permanently ,you need to write in oeminfo with rsa private keys.
And temporary FBLOCK unlocking method is still usable.
![image](https://github.com/user-attachments/assets/5da7af7f-7155-406b-8836-90d7055ca23a)

There exists bootrom download mode.
You can get into this mode only whether by shorting the testpoints or erasing xloader partition(or making xloader partition verification fails_)
In this mode ,you can send xloader.img to memory to load xloader (in download mode)
And in xloader,you are in download mode,you can send fastboot.img to memory directlyfor Kirin970 and older and send uce.img then fastboot.img for Kirin 710,710A,980,and newer.
In fastboot mode,if you are from download mode,the dts will not init.So the screen and vibrator will not turn on.
dts partition is shared between fastboot and kernel.
fastboot use dts partition to light the screen and initialize hardware.
without dts,you can still use fastboot commands.But you can not load into kernel if dts is not init in fastboot mode.

There exists special usb download mode in erecovery.
If you press volume + - and power with usb plugged in,you will enter this mode.
fastboot getvar rescue_enter_recovery can also enter this mode.
In this mode,you will see two ports
They are Android PCUI adapter and DBadapter reserved interface
Dbadapter is used to flash stock firmware(origin UPDATE.APP)(need version number matched)
But I don't know how  the port works.I get usb-capture when using paid tools LieRenXianshua,
thsy send headers for each image,then send data,then send footers.But the sended data is completely different from the data stored in update.app or the extracted img.
![image](https://github.com/user-attachments/assets/743da508-3726-4ed4-89fc-b3ac41a6aeb7)
![image](https://github.com/user-attachments/assets/d2474a03-1fec-4c28-abea-1774fbe063b3)
the difference is too big.
But Before sending any real images,the tool will send a sha256rsa.img extracted from update.app.
(format is the same as above)
the data of sha256rsa.img is the same as the tool sends to phone.

So I think the data must be encrypted using some algorithms before sending to phone.
I don't know.
And if we just send part of images from update.app,the phone will print an error and stop any writing to emmc.
But I don't see any messages sent to phone are about the numbers or the length of images.
This is so strange.

And for old CPU,some tools can upload any images to phone in this mode.
In this way ,they can achieve going to brom download mode without testpoint
This may use some exploits,but I don't know.

Secureboot for Kirin:
Kirin uses special secure boot.
They store a public key in efuse
and they store this key in emmc,too.
the bootrom will verify whether these keys are the same.
then for loading xloader,they will use keys stored in emmc.
for each image,they use three certs.The full signature takes the place of 0x1000 bytes.
This is called VRL header.
In vrl header,there is firmware version.So in theory,there is an only-allow-adding countert  storing version value to achieve
anti-rollback.
but for all socs older than Kirin 990,the version value is 0.
From EMUI10,huawei uses vbmeta .
fastboot will verify the vrl header of vbmeta partition,if it passes,then fastboot will check the signature of boot recovery ramdisk erecovery version product vendor...
(almost all partitions except low level firmwares) ,if they are the same as signature stoed in vbmeta.If all checks pass,the phone will boot.
Another important thing is that the signature storing in vbmeta only changes when major android version changes(eg from EMUI9 to EMUI10)
And for the same big version number(e.g bZC-w00 bzt-w09),different small version number(c000 c923...) shares the same vrl public key and most of signature stored in vbmeta
the system vendor product partition are the exceptions.So don't flash vbmeta partitions(any vbmeta_xxx) and super partition(or system vendor product) when the bootloader is locked.
Or you will get a bricked device!!!!
And the secure boot will also check whether the version number is matched between oeminfo and vbmeta_xxx super(system vendor product).I can not confirm which stores the version number.
If not matched,you will get your device has loader a different operating syetem and then rebooting into erecovery.
---------------------------------------------------------------------------------------




