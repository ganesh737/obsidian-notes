# mke2fs

## ext4
```bash
mkfs.ext4 $P3_FORMAT_OPTIONS $_PART_LABEL $_DEVICE
mkfs.ext4 -N 4000 -I 128 -J size=2 -m 2 -E lazy_itable_init,nodiscard -L persistent /dev/mmcblk1p3
```

## loop device

```bash
sudo losetup /dev/loop0 PARTITION_SCHEMA64_DEFAULT_DEFAULT_64_32
sudo kpartx -a /dev/loop0
sudo mkfs.ext4 /dev/mapper/loop0p3
mkdir test
sudo mount /dev/mapper/loop0p3 test
sudo kpartx -d /dev/loop0
```

# Hashtags

#linux #cmdline #mkfs #kpartx #losetup #mount #userland