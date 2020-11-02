# Android Recovery Mode

Check it out:
	Entering Android Recovery:
		https://groups.google.com/forum/#!topic/android-porting/t4aD6IeHZ-0

./frameworks/base/services/tests/servicestests/src/com/android/server/locksettings/recoverablekeystore/storage/RecoverySnapshotStorageTest.java
./frameworks/base/services/tests/servicestests/src/com/android/server/locksettings/recoverablekeystore/storage/RecoverySessionStorageTest.java
./frameworks/base/services/tests/servicestests/src/com/android/server/locksettings/recoverablekeystore/RecoverySnapshotListenersStorageTest.java
./frameworks/base/services/core/java/com/android/server/locksettings/recoverablekeystore/storage/RecoverySnapshotStorage.java
./frameworks/base/services/core/java/com/android/server/locksettings/recoverablekeystore/storage/RecoverySessionStorage.java
./frameworks/base/services/core/java/com/android/server/locksettings/recoverablekeystore/RecoverySnapshotListenersStorage.java
./frameworks/base/services/core/java/com/android/server/RecoverySystemService.java
./frameworks/base/core/java/android/os/RecoverySystem.java
./frameworks/base/core/java/android/security/keystore/recovery/RecoverySession.java
./frameworks/base/core/java/android/security/keystore/recovery/RecoveryController.java
./frameworks/base/core/java/android/security/keystore/recovery/RecoveryCertPath.aidl
./frameworks/base/core/java/android/security/keystore/recovery/RecoveryCertPath.java
./libcore/luni/src/main/java/libcore/util/RecoverySystem.java
./cts/tests/tests/os/src/android/os/cts/RecoverySystemTest.java


Literature:
https://android.googlesource.com/platform/bootable/recovery/
https://source.android.com/security/verifiedboot/
https://source.android.com/devices/tech/ota/nonab/device_code
https://source.android.com/devices/bootloader/partitions-images
https://source.android.com/devices/bootloader/flashing-updating
https://www.slideshare.net/chrissimmonds/android-bootslides20
https://github.com/csimmonds/boot-extract
https://www.slideshare.net/amraldo/android-booting-scenarios
https://www.slideshare.net/nanik/learning-aosp-android-booting-process
https://stackoverflow.com/questions/10885670/cache-recovery-folder-in-android
https://forum.xda-developers.com/showthread.php?t=1853159
https://www.xda-developers.com/how-to-boot-to-recovery/
https://www.xda-developers.com/aosp-recovery-touch-support-coming/
https://cecs.wright.edu/~pmateti/Courses/4440/Lectures/Internals/
http://cecs.wright.edu/~pmateti/Courses/4900/Lectures/Internals/Android-Internals-2.html


commit aff42013cf1b0ec57b914c88e410c4d27d5346b6
Author: Oleksii Gulchenko <oleksii.gulchenko@globallogic.com.ua>
Date:   Fri Jul 15 12:00:00 2016 +0300

Added Bootloader Control Block module driver.

Android userspace tells the kernel that it wants to boot into recovery
or some other non-default OS environment by passing a string argument
to reboot(). It is left to the OEM to hook this up to their specific
bootloader.

This driver uses the bootloader control block (BCB) in the 'misc'
partition, which is the AOSP mechanism used to communicate with
the bootloader. Writing 'bootonce-NNN' to the command field
will cause the bootloader to do a oneshot boot into an alternate
boot label NNN if it exists. The device and partition number are
passed in via kernel command line.

It is the bootloader's job to guard against this area being uninitialzed
or containing an invalid boot label, and just boot normally if that
is the case. The bootloader will always populate a magic signature in
the BCB; the driver will refuse to update it if not present.

Change-Id: Ie4aec30146d51ef55f086a71190b51a2bb54e784
Signed-off-by: Andrew Boie <andrew.p.boie@intel.com>
Signed-off-by: Oleksii Gulchenko <oleksii.gulchenko@globallogic.com.ua>
Signed-off-by: Oleg Kosheliev <oleg.kosheliev@globallogic.com>


# Hashtags

#android #recoverymode
