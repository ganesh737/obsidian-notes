# systemd

## Basics

* Closely coupled with udev and d-bus
* Nodes are called Units. They are of different types
    * services
    * devices
    * mount points
    * sockets
    * ...
* Graph edges record dependencies between units
    * Functional dependencies --> positive and negative requirements (Requires=…, Conflict=…)
    * Temporal dependencies --> time domain / ordering dependencies
    * Functional and temporal are orthogonal
    * Adding a temporal dependency is not enough to get the dependency started
        * Only functional dependency ensures that unit will be started
* Units
    * Dynamically created at runtime
        * Ex: device units
    * Statically defined in unit files
* Services
    * Units that run applications
    * Types of services
        * simple  --> long lived, follow-ups started immediately
        * oneshot --> follow-up units after main process exits
        * forking --> traditional UNIX daemon
        * dbus    --> applications that provide D-Bus service under a known name
        * notify  --> 
            * application notifies systemd when follow up units can be started
            * by default only main process is allowed to send the notification
            * NotifyAccess=all --> allows child processes to send notifications as well
* Targets
    * Virtual Units where no action is taken
    * Exist in order to collect dependencies to other units(ex: group of services or other targets)
* Devices and udev integration
    * Device units are created dynamically from udev notifications 
        * Used by systemd internally to track dependencies
    * Udev rules can also request other types of units(ex: services)


Synchronizing services-
* SD_NOTIFY
* socket activation using a socket unit
* dbus activation

## Hints

Better to group services by target units. Then have dependency between the target unit

[Having multiple ExecStart is possible for oneshot](https://stackoverflow.com/questions/48195340/systemd-with-multiple-execstart)

# Reference

Link Little Description
http://0pointer.net/blog/projects/systemd-for-admins-1.html
verifying boot up
http://0pointer.net/blog/projects/systemd-for-admins-4.html
killing services
http://0pointer.net/blog/projects/blame-game.html
blame game of which process takes more time to startup :P
http://0pointer.net/blog/projects/the-new-configuration-files.html
configuration files
http://0pointer.net/blog/projects/instances.html
starting/stopping/finding a service instance (maybe for serial port)
http://0pointer.net/blog/projects/systemctl-journal.html
find the status of a service
http://0pointer.net/blog/projects/self-documented-boot.html
finding documentation for a service (the new way. Only available if the service has a documentation). 

Tried it for ```getty@tty1.service``` on CTP target running Linux 4.0.9.
Referred me to get more information from the link http://0pointer.net/blog/projects/serial-console.html

http://0pointer.net/blog/projects/watchdog.html
is more relevant for checking boot loader; because the watchdog is usually configured with bootloader
http://0pointer.net/blog/projects/serial-console.html
interesting on how the serial console is allocated from system side
http://0pointer.net/blog/projects/journalctl.html
checkout the Live View and Basic Filtering section
http://0pointer.net/blog/projects/detect-virt.html
maybe more relevant towards RN-AIVI which has hypervisor
http://0pointer.net/blog/systemd-for-administrators-part-xxi.html
I don’t know how it is implemented in RN-AIVI. But it is a method of having hypervisor.


Extras:
http://0pointer.net/blog/projects/systemd-for-admins-2.html        ->  maybe useful for debugging
http://0pointer.net/blog/projects/systemd-for-admins-3.html        -> Convert A SysV Init Script Into A systemd Service File
http://0pointer.net/blog/projects/three-levels-of-off.html         -> OFF levels for a service
http://0pointer.net/blog/projects/changing-roots.html              -> changing root directory for a process
http://0pointer.net/blog/projects/on-etc-sysinit.html              -> on system initialization
http://0pointer.net/blog/projects/inetd.html                       -> connecting to a network socket after sshd.service is active
http://0pointer.net/blog/projects/security.html                    -> securing the system services
http://0pointer.net/blog/projects/resources.html                   -> deals with CPU resource management
http://0pointer.net/blog/projects/socket-activated-containers.html -> systemd connecting to IP network


After all this, we do need a little bit of developer perspective to understand how they are going to write to it.
The below links deal with how systemd works as a socket.
How to post a message from C program, Python program to the systemd socket. 
http://0pointer.de/blog/projects/systemd.html 
http://0pointer.net/blog/projects/socket-activation.html 
http://0pointer.net/blog/projects/socket-activation2.html 
http://0pointer.net/blog/projects/journal-submit.html 

http://0pointer.net/blog/projects/systemd-for-admins-1.html
http://0pointer.net/blog/projects/systemd-for-admins-2.html
http://0pointer.net/blog/projects/systemd-for-admins-3.html
http://0pointer.net/blog/projects/systemd-for-admins-4.html
http://0pointer.net/blog/projects/three-levels-of-off.html
http://0pointer.net/blog/projects/changing-roots.html
http://0pointer.net/blog/projects/blame-game.html
http://0pointer.net/blog/projects/the-new-configuration-files.html
http://0pointer.net/blog/projects/on-etc-sysinit.html
http://0pointer.net/blog/projects/instances.html
http://0pointer.net/blog/projects/inetd.html
http://0pointer.net/blog/projects/security.html
http://0pointer.net/blog/projects/systemctl-journal.html
http://0pointer.net/blog/projects/self-documented-boot.html
http://0pointer.net/blog/projects/watchdog.html
http://0pointer.net/blog/projects/serial-console.html
http://0pointer.net/blog/projects/journalctl.html
http://0pointer.net/blog/projects/resources.html
http://0pointer.net/blog/projects/detect-virt.html
http://0pointer.net/blog/projects/socket-activated-containers.html


# Hashtags

#linux #systemd #startup