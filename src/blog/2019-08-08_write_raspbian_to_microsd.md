---
title: Writing RASPBIAN to MicroSD card
date: 2019-08-07 12:00
excerpt: Using a Raspberry Pi to setup another Raspberry Pi
type: post
blog: true
tags:
    - Bash
    - Raspberry Pi
    - MicroSD
    - Filesystems
    - Raspbian

---


## Preparing the MicroSD card

If the MicroSD card needs formatting you can follow [this guide](/blog/2019-08-07_format_microsd_on_raspberry_pi.html). 


## Determine which device is your MicroSD card

To determine which device to use (e.g. /dev/sda) see [this guide](/blog/2019-08-07_format_microsd_on_raspberry_pi.html#working-out-which-drive-is-your-microsd-card)

## Writing the operating system to the MicroSD

To write the Raspbian operating system to a MicroSD card for another Pi (or an alternative configuration of the same Pi) is quick and easy:


```
$ sudo dd bs=1M if=./2019-07-10-raspbian-buster.img of=/dev/sda status=progress conv=fsync
```

The Linux will respond with a progress report of the writing of the Raspbian image to the card:

```
31+0 records in
30+0 records out
31457280 bytes (31 MB, 30 MiB) copied, 0.761732 s, 41.3 MB/s
44040192 bytes (44 MB, 42 MiB) copied, 1 s, 43.1 MB/s
76+0 records in
75+0 records out
78643200 bytes (79 MB, 75 MiB) copied, 1.80717 s, 43.5 MB/s
89128960 bytes (89 MB, 85 MiB) copied, 2 s, 44.2 MB/s
121+0 records in
120+0 records out

...

3604+0 records in
3604+0 records out
3779067904 bytes (3.8 GB, 3.5 GiB) copied, 160.254 s, 23.6 MB/s
3604+0 records in
3604+0 records out
3779067904 bytes (3.8 GB, 3.5 GiB) copied, 160.254 s, 23.6 MB/s
pi@ian:~/Documents/Raspbian $ 
```



