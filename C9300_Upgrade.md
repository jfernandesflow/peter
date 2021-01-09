### Change Blocksize for TFTP transfer
* This will increase each block so that les blocks need to be transfered this will allow for faster download speeds


#### Step 1: Clean Up

* This will clean up any ununsed packages
```
Switch# request platform software package clean switch all
Switch# install remove inactive
```

#### Step 2: copy image to flash

##### Copy new image to flash
* To show file systems attached
```
show file systems
```


* Copy from TFTP server to Flash
```
copy tftp: flash:
```

* Copy from USB to flash
```
copy usbflash0: flash:
```

* Check flash has successfully copied
```
Switch# dir flash: *.bin
```


#### Step 3: Set boot variable

* Set boot variable to package.conf
```
Switch(config)# boot system flash:packages.conf
Switch(Config)# exit
```
* write to memory
```
Switch# write memory
```

* show boot system
```
Switch# show boot system
```
The current boot variable should have changed
The boot variable on next reload may not say the same
dont worry

#### Step 4:

##### To install the bin file on the Flash

```
Switch# request platform software package install
```

* An example of installing bin file to all switches

```
Switch# request platform software package install switch all file flash:cat9k_iosxe.16.09.01.SPA.bin auto-copy
```
You must include the `all` to install on all switches  

----------

```
Switch# install add file flash:cat9k_iosxe.16.09.01.SPA.bin activate commit
```
