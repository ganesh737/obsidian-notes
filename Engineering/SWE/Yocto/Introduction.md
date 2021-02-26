# Yocto Embedded Linux

Status: In progress
Tags: competency

# Introduction

## Configurations

DL_DIR → Download folder for all archives, git repositories

SSTATE_CACHE → a global state folder for yocto to work on ... reduces build time for subsequent builds

## Building qemux86 image

bitbake core-image-minimal

runqemu qemux86 core-image-minimal -h — for help options

runqemy qemux86 core-image-minimal slirp — in case of internal networking

## Machine Configuration

machine configurations are part of meta-raspberrypi/conf/machine/

Choose the one suitable for your board → raspberrypi3-64 (want to run aarch64)

machine can be provided via command line itself for bitbake instead of local.conf file hardcoding as 

1. export MACHINE="raspberrypi3-64"
2. MACHINE="raspberrypi3-64" bitbake ...

## Image Configuration

image configurations are available in meta-raspberrypi/recipes-core/images/

They can also be put in folder named images on the outside

## Building for raspberrypi3

Bitbake builds are for the image

For basic rpi3 image -

bitbake core-image-base → because rpi-basic-image is deprecated

## Flashing Images

Images are generated as wic.bz2

They can be written to sdcard with the command -

sudo bmaptool copy core-image-base-raspberrypi3-64.wic.bz2 /dev/mmcblk0

## Reading from console

For putty to read directly without sudo - sudo usermod -a -G dailout ganesh

## Toaster

Toaster is a web ui provided with yocto for configuring and building images 

python3 -m venv venv

source ./venv/bin/activate

pip install -r ../poky/bitbake/toaster-requirements.txt

source toaster start webport=0.0.0.0:8000

Toaster is available on [http://0.0.0.0:8000/toastergui/landing/](http://0.0.0.0:8000/toastergui/landing/)

## RPI3 customizations

More on customising the RPI3 image is available in [https://meta-raspberrypi.readthedocs.io/en/latest/extra-build-config.html](https://meta-raspberrypi.readthedocs.io/en/latest/extra-build-config.html)

# Sec4: Yocto, Bitbake and others

## Bitbake

Starts with bblayers file and include the metadata conf/layer.conf file

Recipies are the basis for the tasks with shell and python code

creates index of tasks, sorted by their dependencies

for each recipe -

- do_fetch - download to DL_DIR
- do_patch - tmp/work directory for extraction, then working on top of it
- do_configure
- do_compile
- Output, Package - deb, rpm, ipk

## Bitbake - RootFS

looks for IMAGE_INSTALL variable for a list of packages to install

the filesystem is then wrapped according to IMAGE_FSTYPES and IMAGE_FEATURES

final images are in tmp/deploy/images/$MACHINE

open rootfs can be found in tmp/work/raspberrypi3_custom-poky-linux-gnueabi/example-image/1.0-r0/rootfs/

## Bitbake - Tasks

Run all tasks for a recipe -

bitbake recipe-name

List tasks available for a recipe-

bitbake recipe-name -c listtasks

Run a specific task for a recipe

bitbake recipe-name -c task-name

## Bitbake: Useful Commands

bitbake -k —> continue with build for all possible components

bitbake recipe-name -fc cleansstate —> cleans sstate ... so package can be built from scratch

bitbake -D —> debug

bitbake -n —> dry run

bitbake -h

## Bitbake: viewing dependencies

bitbake -g core-image-base -u taskexp —> Opens task dependency list

## Yocto Layout

### build Folder

build

-buildhistory —>

-cache

-conf —> bblayers.conf, local.conf for configurations

-downloads —> $DL_DIR

-sstate-cache —> $SSTATE_DIR

-tmp —> compilation artifacts, sysroot, etc

### tmp Folder

tmp

-abi_version

-buildstats

-cache

-deploy — build products - images, packages, sdks

-hostools

-log

-pkgdata

-saved_tmpdir

-sstate-control

-stamps

-sysroots — shared library headers, utilities, 

-sysroots-components

-sysroots-uninative

-work — source code, task configuration, logs, package content

### Work directory

PN —> Package Name

PV —> Package Version

PR —> Package Revision

rpi-build

    tmp

        ${PACKAGE_ARCH}-poky-${TARGET_OS}

            ${PN}

                ${PV}-${PR}      — ${WORKDIR}

                    ${BPN}-${PV} — ${S} for do_fetch and do_unpack, ${B} for do_compile

                    image              —${D} do install

                    package            — ${PKGD}

                    pkgdata             — ${PKGDESTWORK}

                    packages-split   — ${PKGDEST}

                        ${PN}

                        ...

                    recipe-sysroot                — Target

                    recipe-sysroot-native      — Host

        ${MACHINE}-poky-${TARGET_OS}

work - all-poky-linux — contains architecture independent packages

work - x86_64-linux — contains host sysroot contents so for cross compilation

work - aarch64-poky-linux — aarm64 architecture specific packages

work - raspberrypi3_64-poky-linux — contains machine specific packages

### local.conf variables

$MACHINE — Target machine selection

$DL_DIR — downloads directory

$SSTATE_DIR — shared state directory

$TMPDIR — build output

$DISTRO — distribution

$PACKAGE_CLASS — packages format

$SDK_MACHINE — SDK target machine

$EXTRA_IMAGE_FEATURES — extra image packages

### Bitbake Recipe Naming

${PN}_${PV}

- PN: Package Name
- PV: Package Version
- Don't use "_" as part of package name
- Wild card "%" can be used in the version field
- Additionally, you can define in the recipe file:
    - PE: Package Epoch, default value is 0
    - PR: Package Revision, default value is "r0"

### Bitbake: Recipe Anatomy

- $SRC_URI: List of files or sources or repos
    - Ex: "git://github.com/project-name/project.git;branch=branch-name"
        - "branch-name" isn't needed if master
    - Ex: "http://some.url.com/archive.gz;name=custom-name"
- $SRC_URI[file-name.md5sum]: Checksum for "file-name" file in SRC_URI
- $SRC_REV: commit hash in case of git
- $DEPENDS: List of build dependencies
- $RDEPENDS: List of runtime dependencies
- do_install(), do_patch(), etc — the task definitions
- External recipes contain PACKAGES that show additonal packages that they provide which might be of use for us

### Bitbake: Recipe Syntax

Bitbake recipe environment variables - ../poky/meta/conf/bitbake.conf

[https://docs.yoctoproject.org/dev-manual/common-tasks.html#recipe-syntax](https://docs.yoctoproject.org/dev-manual/common-tasks.html#recipe-syntax)

### Bitbake: Packaging

RPM, DEB, IPK, TAR

## Seaching for Recipes

Search for Recipes you want in -[https://layers.openembedded.org/layerindex/branch/master/recipes/](https://layers.openembedded.org/layerindex/branch/master/recipes/)

It also tells the layer which contains the recipe and the dependencies for it and any other layer that it depends on ...

Ex: For networkmanager, it is found in meta-networking layer

# Sec5: Layers & Recipe

## bitbake-layers

adds options for adding or removing or create bblayer.conf

Some useful commands -

- bitbake-layers show-layers
- bitbake-layers show-recipes "*-image-*" — searches for all recipes that contain image
- bitbake-layers create-layer meta-cup; cd rpi-build;
bitbake-layers add-layer ../meta-cup

## creating machines

Pro: allows for capturing parts that enable certain features in our conf file for permanent retension

create one in conf/machine with the details as below 

```bash
#@TYPE: Machine
#@NAME: RaspberryPi 3 Development Board (32bit) - Custom Machine
#@DESCRIPTION: Machine configuration for the RaspberryPi 3 in 32 bits mode

MACHINEOVERRIDES =. "raspberrypi3:"

DEFAULTTUNE ?= "cortexa7thf-neon-vfpv4"
require conf/machine/include/tune-cortexa7.inc
include conf/machine/include/rpi-base.inc

MACHINE_EXTRA_RRECOMMENDS += "\
    linux-firmware-rpidistro-bcm43430 \
    linux-firmware-rpidistro-bcm43455 \
    bluez-firmware-rpidistro-bcm43430a1-hcd \
    bluez-firmware-rpidistro-bcm4345c0-hcd \
"

SDIMG_KERNELIMAGE ?= "kernel7.img"
UBOOT_MACHINE = "rpi_3_32b_config"
SERIAL_CONSOLES ?= "115200;ttyS0"

VC4DTBO ?= "vc4-fkms-v3d"
ARMSTUB ?= "armstub7.bin"

# Enable serial console
ENABLE_UART = "1"
DISABLE_SPLASH = "1"
DISABLE_RPI_BOOT_LOGO = "1"
```

## creating custom distros

create a distro file is conf/distro

```bash
MAINTAINER = "ganesh <ganesh.rvec@gmail.com>"

require conf/distro/poky.conf

DISTRO = "example-distro"
DISTRO_NAME = "example distro"
DISTRO_VERSION = "1.0"
DISTRO_CODENAME = "example"
SDK_VENDOR = "-exampledistro"
SDK_VERSION = "sdkversion"

# set hostname
hostname_pn-base-files = "example"

# update to systemd init instead of sysvinit
DISTRO_FEATURES_append = " systemd"
VIRTUAL-RUNTIME_init_manager = "systemd"
DISTRO_FEATURES_remove += "sysvinit"
VIRTUAL-RUNTIME_initscripts = "systemd-compat-units"
DISTRO_FEATURES_BACKFILL_CONSIDERED = "sysvinit"

# remove unused features
DISTRO_FEATURES_remove += " bluetool ext2 irda pcmcia pci 3g nfc x11 opengl multiarch wayland vulkan pulseaudio bluez5"

# set the default timezone
DEFAULT_TIMEZONE = "Asia/Kolkata"
```

List image features with 

```bash
bitbake example-image -e | grep "^DISTRO_FEATURES"
```

Timezone can be configured with adding required package in [example-image.bb](http://example-image.bb) i.e. tzdata and tzdata-asia

The default timezone for the device is configured in the distro.conf file

The configuration for root user password can be done in distro.conf or image recipe

[https://wiki.yoctoproject.org/wiki/FAQ:How_do_I_set_or_change_the_root_password](https://wiki.yoctoproject.org/wiki/FAQ:How_do_I_set_or_change_the_root_password)

## recipetool

helps in autogenerating recipes ... we need to customize them as per our needs after that ...

It is a OpenEmbedded tool

```bash
options:
  -d, --debug     Enable debug output
  -q, --quiet     Print only errors
  --color COLOR   Colorize output (where COLOR is auto, always, never)
  -h, --help      show this help message and exit

subcommands:
  setvar          Set a variable within a recipe
  newappend       Create a bbappend for the specified target in the specified layer
  create          Create a new recipe
  edit            Edit the recipe and appends for the specified target. This obeys $VISUAL if set, otherwise $EDITOR, otherwise vi.
  appendfile      Create/update a bbappend to replace a target file
  appendsrcfiles  Create/update a bbappend to add or replace source files
  appendsrcfile   Create/update a bbappend to add or replace a source file
```

### creating for source files

```bash
recipetool create -N hello-world-cpp-makefile -V 1.00 files/hello-world-cpp-makefile.tar.gz
```

### creating from remote git repository (recommended)

```bash
recipetool create -N python-flash-hello-world -V 1.00 https://github.com/hubshuffle/python-flask-hello-world.git
```

## Python Flask deployment with service file

```bash
# Recipe created by recipetool
# This is the basis of a recipe and may need further editing in order to be fully functional.
# (Feel free to remove these comments when editing.)

# Unable to find any files that looked like license statements. Check the accompanying
# documentation and source headers and set LICENSE and LIC_FILES_CHKSUM accordingly.
#
# NOTE: LICENSE is being set to "CLOSED" to allow you to at least start building - if
# this is not accurate with respect to the licensing of the software being built (it
# will not be in most cases) you must specify the correct value before using this
# recipe for anything other than initial testing/development!
LICENSE = "CLOSED"
LIC_FILES_CHKSUM = ""

SRC_URI = "\
git://github.com/hubshuffle/python-flask-hello-world.git;protocol=https \
file://python-flask-hello-world.service \
"

# Modify these as desired
PV = "1.00+git${SRCPV}"
SRCREV = "ef935ecdf7b081fbc86ae9a71812e64a6a138301"

RDEPENDS_${PN} = " python3 python3-flask "

S = "${WORKDIR}/git"

inherit systemd

do_install () {
	# install python script
	install -d "${D}${bindir}"
	install -m 0755 app.py "${D}${bindir}/python-flask-hello-world.py"

	# install the service file
	install -d "${D}${systemd_unitdir}/system"
	install -m 0644 "${WORKDIR}/python-flask-hello-world.service" \
		"${D}${systemd_unitdir}/system"
}

FILES_${PN} += "\
${bindir}/python-flask-hello-world.py \
${systemd_unitdir}/system/python-flask-hello-world.service\
"

SYSTEMD_SERVICE_${PN} = "python-flask-hello-world.service"
```

```bash
[Unit]
Description=Python Flash Hello World

[Service]
Type=simple
Restart=always
RestartSec=10s
StandardOutput=syslog
StandardError=syslog
ExecStart=/usr/bin/python-flask-hello-world.py

[Install]
WantedBy=multi-user.target
```

```python
#!/usr/bin/env python3

from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

## Using patches in a Recipe

### using devshell

```bash
bitbake python-flask-hello-world -c devshell
# make the changes
# git commit -am "message"
# git format-patch HEAD~1
# copy the patch file to files folder
# Add the file to SRC_URI in the bb file
```

## Appending Recipes

```bash
FILESEXTRAPATHS_prepend := "${THISDIR}/files:"

SRC_URI += "\
file://railwire_ganesh.nmconnection \
"

do_install_append() {
    # install network config file
    install -m 0600 "${WORKDIR}/railwire_ganesh.nmconnection" "${D}${sysconfdir}/NetworkManager/system-connections"
}
```

## Package management

The below configurations can be added to distro config file to configure for a distro

```bash
# configure package management                                                                                          
EXTRA_IMAGE_FEATURES += "package-management"                                                                            
PACKAGE_CLASSES_append = " package_ipk "                                                                                
IMAGE_INSTALL_append = " opkg "                                                                                         
PRSERV_HOST = "localhost:0"                                                                                             
PACKAGE_FEED_URIS = "http://192.168.0.108:8080"                                                                         
PACKAGE_FEED_BASE_PATHS = ""                                                                                            
PACKAGE_FEED_ARCHS = "cortexa7t2hf-neon-vfpv4"
```

Start a python server in the ipk folder of your host machine

```bash
python3 -m http.server 8080
```

Check the file /etc/opkg/base-feeds.conf. It should have the information about the server

```bash
#This can be referred by target for newer packages
opkg update
opkg install ***
```

## Creating a CMake Recipe

Creating the recipe is easier with 

```bash
recipetool -N cmake-hello-world -V 1.00 https://github.com/ganesh737/cmake-hello-world.git
```

Add section for do_install() if is it not mentioned in the CMakeLists.txt file

# SDK

Yocto allows to generate a sharable SDK that contains the toolchain and other parts to compile and generate image

```bash
bitbake example-image -c populate_sdk
```

# Using devtool

devtool lets us modify the sources as available either from an extracted workspace or clone or local cloned folder

```bash
# Method 1
devtool modify linux-raspberrypi
cd workspace/sources/linux-raspberrypi/
bitbake linux-raspberrypi -c menuconfig
# the below command copies the diff to the layer of our choice
devtool finish linux-raspberrypi meta-example
# now, build the changes
bitbake linux-raspberrypi

# Method 2
devtool modify -n linux-raspberrypi workspace/sources/linux-raspberrypi/

# Checking which workspaces are in devtool
devtool status

# Reset local changes with
devtool reset linux-raspberrypi
```

# Working with Qt

# Helpful things

Use screen for serial console with logging

```bash
screen -L -Logfile /home/ganesh/vmshare/logging/rpi/rpi_serial_$(date +%Y%m%d%k%M).log /dev/ttyUSB0 115200
```

Use the below command to work properly with command prompt only

```bash
command | tee > (xclip)

# output is available with key combination of 'Shift + Insert'
# or the below command
xclip -o
```

## Find out which recipe provides a file

```bash
oe-pkgdata-util find-path /usr/bin/nmcli
```

## Sample License File

```bash
available in poky/meta/files/common-licenses/
```

## Debug shell

```bash
bitbake recipe-name -c devshell
```

# References

- Bitbake Guide: [https://a4z.gitlab.io/docs/BitBake/guide.html](https://a4z.gitlab.io/docs/BitBake/guide.html)
- Yocto Project Quick Start: [https://www.yoctoproject.org/docs/latest/brief-yoctoprojectqs/brief-yoctoprojectqs.html](https://www.yoctoproject.org/docs/latest/brief-yoctoprojectqs/brief-yoctoprojectqs.html)
- Toaster Manual: [https://www.yoctoproject.org/docs/latest/toaster-manual/toaster-manual.html](https://www.yoctoproject.org/docs/latest/toaster-manual/toaster-manual.html)
- Yocto Reference Manual: [https://www.yoctoproject.org/docs/latest/ref-manual/ref-manual.html](https://www.yoctoproject.org/docs/latest/ref-manual/ref-manual.html)
- Yocto Developers Manual: [https://www.yoctoproject.org/docs/latest/dev-manual/dev-manual.html](https://www.yoctoproject.org/docs/latest/dev-manual/dev-manual.html)