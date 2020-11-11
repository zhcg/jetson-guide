# jetson-guide
NVIDIA jetson系列使用过程中总结的一些方法技巧


```
#命令进入recovery模式
sudo reboot --force forced-recovery   
```

```
#开启最大性能
sudo nvpmodel -m 0  
sudo jetson_clocks 
```

```
#RTC测试
sudo hwclock

timedatectl
```

1、进recovery模式
     

```
完全擦除烧写
     sudo ./flash.sh rtso-hxnv001 mmcblk0p1

     只烧写dtb
     sudo ./flash.sh -k kernel-dtb rtso-hxnv001 mmcblk0p1

     只烧写kernel，烧写前先进系统删除/boot/Image 
     sudo ./flash.sh -k kernel rtso-hxnv001 mmcblk0p1
```


2、dd命令烧写分区


```
kernel分区可能同样需要删除/boot/Image
      sudo dd if=your_image  of=/dev/mmcblk0pxx

      mmcblk0pxx 可以通过命令查看相应分区
      sudo gdisk -l /dev/mmcblk0
```


烧写失败，EEPROM报错

```
1）SKIP_EEPROM_CHECK=1; #in jetson-xavier.conf bypass the error
2）i2cset modify the eeprom crc value
   ./bootloader/chkbdinfo -i bootloader/cvm.bin #crc错误时可提示正确crc
```
