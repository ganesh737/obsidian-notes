# fdisk

## Partition

```bash
echo -e "o\nw\n" | ${DISK_COMMAND} ${_DEVICE}
DISK_COMMAND=fdisk
_DEVICE=/dev/mmcblk1
_PART_NAME=3
_PARTSECTORS_START=196672
_PARTSIZE=102400
echo -e "n\np\n"${_PART_NAME}"\n"${_PARTSECTORS_START}"\n+"${_PARTSIZE}"\n\nw\n" | ${DISK_COMMAND} ${_DEVICE} >/dev/null
```

## Options

```bash
Command (m for help): m
Command Action
a       toggle a bootable flag
b       edit bsd disklabel
c       toggle the dos compatibility flag
d       delete a partition
l       list known partition types
n       add a new partition
o       create a new empty DOS partition table
p       print the partition table
q       quit without saving changes
s       create a new empty Sun disklabel
t       change a partition\'s system id
u       change display/entry units
v       verify the partition table
w       write table to disk and exit
```

# Hashtags

#linux #fdisk