# mmc

```bash
sh-3.2# /usr/bin/mmc
Usage:
        mmc extcsd read <device>
                Print extcsd data from <device>.
        mmc writeprotect get <device>
                Determine the eMMC writeprotect status of <device>.
        mmc writeprotect set <device>
                Set the eMMC writeprotect status of <device>.
                This sets the eMMC to be write-protected until next boot.
        mmc disable 512B emulation <device>
                Set the eMMC data sector size to 4KB by disabling emulation on
                <device>.
        mmc gp create <-y|-n> <length KiB> <partition> <enh_attr> <ext_attr> <device>
                create general purpose partition for the <device>.
                Dry-run only unless -y is passed.
                NOTE!  This is a one-time programmable (unreversible) change.
                To set enhanced attribute to general partition being created set
                 <enh_attr> to 1 else set it to 0.
                To set extended attribute to general partition
                 set <ext_attr> to 1,2 else set it to 0
        mmc enh_area set <-y|-n> <start KiB> <length KiB> <device>
                Enable the enhanced user area for the <device>.
                Dry-run only unless -y is passed.
                NOTE!  This is a one-time programmable (unreversible) change.
        mmc write_reliability set <-y|-n> <partition> <device>
                Enable write reliability per partition for the <device>.
                Dry-run only unless -y is passed.
                NOTE!  This is a one-time programmable (unreversible) change.
        mmc status get <device>
                Print the response to STATUS_SEND (CMD13).
        mmc bootpart enable <boot_partition> <send_ack> <device>
                Enable the boot partition for the <device>.
                To receive acknowledgment of boot from the card set <send_ack>
                to 1, else set it to 0.
        mmc bootbus set <boot_mode> <boot_bus_width> <device>
                Set the boot mode and boot bus width for the <device>.
        mmc bkops enable <device>
                Enable the eMMC BKOPS feature on <device>.
                NOTE!  This is a one-time programmable (unreversible) change.
        mmc hwreset enable <device>
                Permanently enable the eMMC H/W Reset feature on <device>.
                NOTE!  This is a one-time programmable (unreversible) change.
        mmc hwreset disable <device>
                Permanently disable the eMMC H/W Reset feature on <device>.
                NOTE!  This is a one-time programmable (unreversible) change.
        mmc sanitize <device>
                Send Sanitize command to the <device>.
                This will delete the unmapped memory region of the device.
        mmc rpmb write-key <rpmb device> <key file>
                Program authentication key which is 32 bytes length and stored
                in the specified file. Also you can specify '-' instead of
                key file path to read the key from stdin.
                NOTE!  This is a one-time programmable (unreversible) change.
                Example:
                  $ echo -n AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHH | \
                    mmc rpmb write-key /dev/mmcblk0rpmb -
        mmc rpmb read-counter <rpmb device>
                Counter value for the <rpmb device> will be read to stdout.
        mmc rpmb read-block <rpmb device> <address> <blocks count> <output file> [key file]
                Blocks of 256 bytes will be read from <rpmb device> to output
                file or stdout if '-' is specified. If key is specified - read
                data will be verified. Instead of regular path you can specify
                '-' to read key from stdin.
                Example:
                  $ echo -n AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHH | \
                    mmc rpmb read-block /dev/mmcblk0rpmb 0x02 2 /tmp/block -
                or read two blocks without verification
                  $ mmc rpmb read-block /dev/mmcblk0rpmb 0x02 2 /tmp/block
        mmc rpmb write-block <rpmb device> <address> <256 byte data file> <key file>
                Block of 256 bytes will be written from data file to
                <rpmb device>. Also you can specify '-' instead of key
                file path or data file to read the data from stdin.
                Example:
                  $ (awk 'BEGIN {while (c++<256) printf "a"}' | \
                    echo -n AAAABBBBCCCCDDDDEEEEFFFFGGGGHHHH) | \
                    mmc rpmb write-block /dev/mmcblk0rpmb 0x02 - -
        mmc cache enable <device>
                Enable the eMMC cache feature on <device>.
                NOTE! The cache is an optional feature on devices >= eMMC4.5.
        mmc cache disable <device>
                Disable the eMMC cache feature on <device>.
                NOTE! The cache is an optional feature on devices >= eMMC4.5.

        mmc help|--help|-h
                Show the help.

        mmc <cmd> --help
                Show detailed help for a command or subset of commands.
```

# Reference

[mmc-tools](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/mmc/mmc-tools.txt)
[MMC](http://trac.gateworks.com/wiki/MMC)

# HashTags

#linux #mmc #userland