# Linux Unified Keys Setup (LUKS)

## dm-verity

```bash
dd if=/dev/zero of=rfs.img bs=1M count=1024
mkfs.ext4 rfs.img
losetup -f
sudo losetup /dev/loop1 rfs.img
sudo e2fsck -fy /dev/loop1
sudo resize2fs /dev/loop1 992M
/sbin/dumpe2fs rfs.img |grep "Block count" | sed -e 's/[^0-9]//g'
/sbin/dumpe2fs rfs.img |grep "Block size" | sed -e 's/[^0-9]//g'
sudo veritysetup --verbose --debug --data-block-size=4096 --data-blocks=253952 --hash-block-size=4096 --hash-offset=1040187392 --format=1 format /dev/loop1 /dev/loop1
# store the roothash and salt values from the output
# cryptsetup 1.6.6 processing "veritysetup --verbose --debug --data-block-size=4096 --data-blocks=253952 --hash-block-size=4096 --hash-offset=1040187392 --format=1 format /dev/loop1 /dev/loop1"
# Running command format.
# Allocating crypt device /dev/loop1 context.
# Trying to open and read device /dev/loop1.
# Initialising device-mapper backend library.
# Formatting device /dev/loop1 as type VERITY.
# Crypto backend (gcrypt 1.6.5) initialized.
# Detected kernel Linux 4.4.0-148-generic x86_64.
# Setting ciphertext data device to /dev/loop1.
# Trying to open and read device /dev/loop1.
# Hash creation sha256, data device /dev/loop1, data blocks 253952, hash_device /dev/loop1, offset 253953.
# Using 3 hash levels.
# Data device size required: 1040187392 bytes.
# Hash device size required: 1048387584 bytes.
# Updating VERITY header of size 512 on device /dev/loop1, offset 1040187392.
#VERITY header information for /dev/loop1
#UUID:                   ed7a18df-6f86-42f7-b1a7-bc435bf4ceef
#Hash type:              1
#Data blocks:            253952
#Data block size:        4096
#Hash block size:        4096
#Hash algorithm:         sha256
#Salt:                   d833f1d5bc29dfeab5b214b42d228a199b76f9fea083b5e98a48b057d429582c
#Root hash:              ab8602ca8f29371cb5dddaf1f40c050ba8f4e8ae1ed5b96e18e756c1fd352f8c
# Releasing crypt device /dev/loop1 context.
# Releasing device-mapper backend.
#Command successful.

sudo veritysetup --verbose --debug --data-block-size=4096 --data-blocks=253952 --hash-block-size=4096 --hash-offset=1040187392 verify /dev/loop1 /dev/loop1 49143d3246eb8b58e483215750bc0468757d2078a57b48a74e3114ce2dadde07g
```

# Reference

[LUKS Wiki](https://gitlab.com/cryptsetup/cryptsetup/wikis/home)
[DMCrypt](https://gitlab.com/cryptsetup/cryptsetup/-/wikis/DMCrypt)
[Linux Kernel - dm-verity](https://www.kernel.org/doc/Documentation/device-mapper/verity.txt)
[LWN verity](https://lwn.net/Articles/459420/)

# Hashtags

#linux #security #luks