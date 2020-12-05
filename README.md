#### dd_method_OS_usb_iso_creation_guide
# Create Bootable Media in 2 Steps 

### Using Windows or MacOS? I recommend this tool:
#### Fedora Media Writer (Windows/MacOS)
https://getfedora.org/en/workstation/download/
#### It is well made, safe, simple, installs any iso or removes (restoring the media). 



# Using Linux: DD Method

#### If you are using Linux to make a bootable USB (et al) from an .iso or .img, you do this in two steps using the DD method in a linux terminal. 

# Step 1. Get name of device

```
$ dmesg
```

#### Make sure you are writing to the correct drive/device/media. Run 'dmesg' in a terminal to see what the name of the USB (which you inserted into your computer) is called


#### The output will look something like this:
```
[  251.091225] usb-storage 3-7:1.0: USB Mass Storage device detected
[  251.091537] scsi host6: usb-storage 3-7:1.0
[  251.091591] usbcore: registered new interface driver usb-storage
[  251.093885] usbcore: registered new interface driver uas
[  254.436918] scsi 6:0:0:0: Direct-Access              USB Flash Drive  PMAP PQ: 0 ANSI: 6
[  254.437780] sd 6:0:0:0: Attached scsi generic sg2 type 0
[  254.440852] sd 6:0:0:0: [sdb] 30322688 512-byte logical blocks: (15.5 GB/14.5 GiB)
[  254.442728] sd 6:0:0:0: [sdb] Write Protect is off
[  254.442731] sd 6:0:0:0: [sdb] Mode Sense: 23 00 00 00
[  254.444051] sd 6:0:0:0: [sdb] No Caching mode page found
[  254.444053] sd 6:0:0:0: [sdb] Assuming drive cache: write through
[  254.463928]  sdb: sdb1 sdb2
```


#### What you are looking for is the name of that USB. In this example it is called "sdb," which you can see printed many times. You can also see the drive size which may help to identify the drive.



# Step 2. DD

```
$ sudo dd if=THE_NAME_OF_YOUR_FILE of=/dev/NAME_OF_YOUR_USB bs=8M status=progress oflag=direct
```

#### Note 1: You can change the details (and look online for other approaches) but this a standard set of parameters for DD.

#### Note 2: The easiest way is to open a terminal where your .iso file is, but you can also put in the whole file path.

#### Note 3: This will "destroy" whatever was on the drive you are pointing this at, so be careful to pick the correct drive! 

#### e.g.

```
$ sudo dd if=fedora_36.iso of=/dev/sdX bs=8M status=progress oflag=direct
```
or
```
$ sudo dd if=/path/to/image.iso of=/dev/sdX bs=8M status=progress oflag=direct

```

# Done!

