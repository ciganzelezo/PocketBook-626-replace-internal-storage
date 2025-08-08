# PocketBook-626-replace-internal-storage
Guide/general information about replacing internal storage in the ebook reader PocketBook 626 (Touch Lux 2) and other PocketBook devices
Since i didn't see a definitive guide that worked, i've decided to make one myself, so others won't have to go throught hours of torture like me.
The credits go to users on the mobileread.com forum, mainly _nhedgehog_,_m4mmon_ and others.

## Souces
- [mobileread thread](https://www.mobileread.com/forums/showthread.php?t=278728)
- [Richard Butrons blog post](https://richard.burtons.org/2016/07/01/changing-the-cid-on-an-sd-card/)
- [Lunator's blog post](http://luator.de/linux/2019/11/23/pocketbook-replace-memory.html)
- Also credit goes to a russian forum (link is dead)

## About the device

### Hardware
- PocketBook 626, and probably most of the other models except the very old ones use a micro SD card for internal storage (don't confuse it with the additional storage, that is also a micro SD card.
  - As everyone knows, SD cards don't really live that long, and over time, they often die or become read-only. That means it deletes all the stuff you saved after shutting down the reader.

### OS
- The device uses linux with very unstandard configuration that was made to be as cryptic as possible, so people like me or you can't do stuff they want
- It has 10 partitions that look like this
  - p1 is the _main/user data_ parition where books and apps are stored, it's also the parition that shows up when you connect the reader to a PC
```
Device          Boot   Start      End  Sectors   Size Id Type
/dev/mmcblk0p1       1011712 31116287 30104576  14,4G  b W95 FAT32
/dev/mmcblk0p2  *      73728   139263    65536    32M  6 FAT16
/dev/mmcblk0p3             1  1009664  1009664   493M 85 Linux extended
/dev/mmcblk0p5        139264   172031    32768    16M 83 Linux
/dev/mmcblk0p6        172032   204799    32768    16M 83 Linux
/dev/mmcblk0p7        204800   275455    70656  34,5M 83 Linux
/dev/mmcblk0p8        275456   776191   500736 244,5M 83 Linux
/dev/mmcblk0p9        776192   976895   200704    98M 83 Linux
/dev/mmcblk0p10       976896  1009663    32768    16M 83 Linux
```
- The system checks the CID (Card Identification Data) of the SD card, to check if the card is the original one, other systems also do this (GPS devices, kiosks, etc.)
  - So just cloning the whole image to another SD card won't work, if the CID does not match the original one, the reader just shows a sand clock at boot (in most cases)

## Manuals

### Read CID of and SD card
- Be aware that in order to correctly interact with a SD card, you need a device with embedded card reader. **USB readers can't read the cid**, since the computer sees the device as unspecified USB mass storage device
- It's easiest to do in Linux - `cat /sys/block/mmcblkX/device/cid` - replace X with the correct number (you can check with `lsblk`)
- On Windows, you'll have to use specialized apps, i don't have experience with that, so you'll have to find something yourself
- It's also possible to do in rooted android - You'll have to identify the correct disk number, most probably it's 1 because 0 is device storage
  - To execute the command either download a Android terminal emulator app or use [adb](https://developer.android.com/tools/adb)
    - **How to do it with adb:** `adb shell`, `su`,`/sys/block/mmcblkX/device/cid`

### Buy unlocked micro SD card
- Look up _unlocked CID micro SD_ or _custom CID micro SD_ or something along those lines. They are also sometimes called _coldgards_, mainly chinese sellers will pop up, but i've found a rather reliable seller from Europe - [zelemar.eu](https://zelemar.eu/)
- You can either buy card that will already ship to you with with your custom CID, or the CID can be changed with some software they provide
..to be continued
