# U-Boot

## U-Boot Utilities

### mmc

MMC Sub System
```bash
Usage:
mmc info - display info of the current MMC device
mmc read addr blk# cnt
mmc write addr blk# cnt
mmc erase blk# cnt
mmc rescan
mmc part - lists available partition on current mmc device
mmc dev [dev] [part] - show or set current mmc device [partition]
mmc list - lists available devices
mmc hwpartition [args...] - does hardware partitioning
  arguments (sizes in 512-byte blocks):
  [user [enh start cnt] [wrrel {on|off}]] - sets user data area attributes
  [gp1|gp2|gp3|gp4 cnt [enh] [wrrel {on|off}]] - general purpose partition
  [check|set|complete] - mode, complete set partitioning completed
  WARNING: Partitioning is a write-once setting once it is set to complete.
  Power cycling is required to initialize partitions after set to complete.
mmc setdsr <value> - set DSR register value
```

[TI U-Boot User Guide](http://processors.wiki.ti.com/index.php/Linux_Core_U-Boot_User%27s_Guide)
[U-Boot mmc read write command usage](https://embeddedma.blogspot.in/2013/06/uboot-mmc-read-write-command-usage.html)

# Hashtags

#uboot #bootloader