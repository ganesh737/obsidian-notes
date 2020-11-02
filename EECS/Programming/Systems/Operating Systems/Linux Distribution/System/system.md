# Linux Distributions

## System Start-up

The system start-up has the below stages -
1. BIOS
2. MBR
3. GRUB
4. Kernel
5. systemd/init
6. Run Levels

### Run Levels

0 - halt
1 - single user mode
2 - multi-user, without NFS
3 - full multi-user mode
4 - unused
5 - X11
6 - reboot

Accordingly, there are /etc/rc.\<RUN LEVEL>.d/ so that files are executed at particular run level
S --> start --> used during startup
K --> kill --> used during shutdown


## Storage

### Partitioning

#### Partition Headers

##### MBR

Primary partition headers are stored at the start of the memory device.

Logical partition headers are stored along with the partition

##### GPT

Primary partition headers are stored in the initial 34KB of memory device

Backup is stored in last 34KB of memory device

GUID --> Globally Unique IDentifiers
GPT → GUID Partition Table
LBA --> Logical Block Address


#### Partition Utilities

[[EECS/Programming/Systems/Operating Systems/System Components/File Systems/fdisk]]

[[EECS/Programming/Systems/Operating Systems/System Components/File Systems/gdisk]]

### File Systems

#### Basic Structure

```bash
/etc        # Configuration files
/home       # user folders
/proc
/usr        # Universal System Resources
/tmp        # temporary directory on RAM
```

## Processes

### IDs

PID --> Process ID
UID --> User ID

# Hashtags

#linux