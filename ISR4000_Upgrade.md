# ISR4000

#### Pre Checks
* Check IOS Image
```
show version
```
* show Rommon
```
show platform
```
* show flash contents
```
dir bootflash:
```
### Upgrade IOS Image
#### Copy bin image

* Copy from server to bootflash
```
copy tftp: bootflash:
```
* Copy from usbflash to boot flash
```
copy usbflash0 bootflash:
```
#### Verify with MD5
```
verify /md5 flash:package
```
#### Set Boot image
```
boot system flash bootflash:isr-univeralk893435r.bin
```
#### Verify that boot image is set
```
show run | include boot
```

#### Copy Running config to startup config
```
copy run start
```

#### Restart the Switch
```
reload
```

### Upgrade ROMMON
#### Copy Rommon
```
copy usbflash0: bootflash:
```

#### Verify MD5
```
verify /md5 bootflash:package
```

#### Install new Rommon
```
upgrade rom-monitor filename bootflash:package R0
```
* R0 is the rom monitor that will be upgraded


### Update CPLD
#### Backup bootflash
```
copy running-config bootflash:running-config_backup
```
#### Config register to 0x0
```
conf t
config-register 0x0
end
copy run start
```
#### Reload ensure that the Rommon prompt is displayed

```
reload
```

#### initiate update
* boot from usb0
```
boot usb0:package.bin
```
* boot from bootflash
```
boot bootflash:package.bin
```

#### Check that rommon update
```
show hw-programmable 0
```
