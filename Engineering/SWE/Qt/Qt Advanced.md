# 1 QT Threads

QThread as are by default in wait or halt state ... we need to start it to start the thread ...

Note: Don't use QThread inheritance ... Since we are changing the QThread behaviour ... So moveToThread is a better option with signals and slots for communication ...

if we simply start a thread, it runs on the main thread instead of its own individual thread ... it runs on its own thread when it is moved to that thread and then connected, started ...

ThreadPools are better than QList of QThread*

QMutex --> solves thread race condition ... Mutually Exclusive Flag ...
	Recursive --> thread can lock and unlock the mutex any number of times ... number of locks should be equal to number of unlocks
	NonRecursive --> thread can lock a mutex only once & then delete the mutex

QMutexLocker --> Simplifies QMutex usage
	Create and forget ...
	Create and it gets destroyed when it goes out of scope ... And mutex also gets unlocked on its own
	
QSemaphore --> multiple threads lock and synchronize

make sure to use Qt::QueuedConnection for signal and slot connection otherwise there can be problems with signals and slots in multi-threaded application

## Signals and Slots in Threads

slot can be run in sender thread or receiver thread based on the configuration

Qt::AutoConnection - runs on both
Qt::QueuedConnection - runs on main thread
Qt::DirectConnection - runs on thread
Qt::BlockingQueuedConnection - blocks
Qt::UniqueConnection - combined with others

## Qt Concurrent

QFuture -> asynchronous communication

QtConcurrent::blockingMapped(values,&do_map) --> blocking main thread

QFutureWatcher to wait for future values qtca1_14

Use QtConcurrent::map(list, method) to make the method go over all values of list

QFutureWatcher slots in qtca1_16

QFutureIterator in qtca1_17

QFutureSynchronizer in qtca1_18
it includes a waitForFinished

# 2 Networking

## Pointers

using ports < 1024 need special rights ... so they are called admin ports

## QHostAddress & QNetworkInterface

qtca2_1

QHostAddress has methods to find out if it is loopback, protocol, etc

## QUdpSocket

qtca2_2

ports once bound need to be released for another application to use it

Protocol or RFC (Request for Comments)

qtca2_3

QUdpSocket::ShareAddress --> non blocking bind so that multiple applications can connect in parallel

## QTcpSocket

qtca2_4

Main interface is QAbstractSocket

socket.bytesAvailable --> provides information on the number of available bytes so we can do buffering properly

## QNetworkProxy

qtca2_5

Can be set per socket or per application

## QSslSocket

qtca2_6

This internally contains the QTcpSocket class so using this is like using it on top of tcp

## Synchronous TCP

qtca2_7

## Synchronous UDP

qtca2_8

## QNetworkAccessManager HTTP

qtca2_9

encapsulated http & ssl at its core ... helps reduce the complexity related to QTcpSocket or QSslSocket

PUT --> sending files
POST --> post requests

## QNetworkAccessManager FTP

qtca2_10

## QTcpServer

qtca2_11

single threaded server

## Multi-threaded TCP server

qtca2_12

Need to extend QTcpServer with our changes


## ssl server - creating a certificate

Dangerous to do it this way for production systems !!!

Create a cert - https://stackoverflow.com/questions/33198360/qt-with-qsslsocket-not-connecting-properly

Step 1: Generate a Private Key
openssl genrsa -des3 -out server.key 1024

Step 2: Generate a CSR (Certificate Signing Request)
Common Name (eg, your name or your server's hostname):example.com
openssl req -new -key server.key -out server.csr

Step 3: Remove Passphrase from Key
cp server.key server.key.org
openssl rsa -in server.key.org -out server.key

Step 4: Generating a Self-Signed Certificate
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

Test the connection
openssl s\_client -connect 127.0.0.1:2020

## ssl server - creating the server

qtca2_14

# 3 Libraries and Plugins

## shared library

qtca3_1

internal library

LD_LIBRARY_PATH=mylib ./myapp

## shared external library

qtca3_2

LD_LIBRARY_PATH=../build-qtca3_1-Desktop_Qt_5_15_2_GCC_64bit-Debug/mylib/ ./qtca3_2

In case app depends on library that is using some QT library like 'QT+=network', then the app also should include it its project file
demo in qtca3_3

## static library

qtca3_4
CONFIG += staticlib

con: other applications need a rebuild in case of library changes.
so this is not the usually preferred way of building apps and libraries

## plugins

qtca3_5

CONFIG += plugin

myplugin.h - ```Q_PLUGIN_METADATA(IID QGenericPluginFactoryInterface_iid FILE "myplugin.json")```

The value for QGenericPluginFactoryInterface_iid should be replaced with proper identifier

copy the plugin.so to generic plugins folder for our application to use

### Application Plugins

qtca3_6

QPluginLoader

### Plugins from other authors

qtca3_7

# 4 Databases

organized collection of data

https://www.db4free.net/

# 5 Unit Testing

## introduction
QTest QtTest classes are used

initTestCase --> before the test case
cleanupTestCase --> end of all test cases
init --> before each test case
cleanup --> after each test case

## data driven testing

foo
foo_data --> add data for testing foo

QTest comes with a database for adding data and use for testing
```
QTest::addColumn<QString>("name");
QTest::addColumn<int>("age");

QTest::addRow("Invalid") << "test" << 1000;
QTest::addRow("Old") << "test" << 60;

// in foo -
QFETCH(QString, name);
QFETCH(int, age);

// use name and age in test... foo will run for all the filled values
```

## benchmarking

QBENCHMARK

not the same as code profiling

# Qt Deploying Applications

## mac

bundle

https://github.com/voidrealms/qtca-6-2

Step1: Generate app bundle with below config and release build
```
CONFIG += app_bundle
```
Step2: Run the below command to generate dmg 
```
macdeployqt qtca.app -dmg
```

## linux

AppImage

[linuxdeployqt](https://github.com/probonopd/linuxdeployqt)

[AppImage](https://appimage.org)
[AppImageKit](https://github.com/AppImage/AppImageKit)

Step1: Run the below command to generate dmg 
```
./linuxdeployqt-6-x86_64.AppImage <PATH TO BINARY> -qmake=<PATH TO QMAKE> -unsupported-allow-new-glibc
```

## windows

```
build in release
show the exe
Run windeploy qt
<PATH TO QT>\mingw73_64\bin\windeployqt.exe "<PATH TO BINARY>"
Run it and show its still having issues
Show Dependancy walker and show the yellow items
 Still missing
    LIBGCC_S_DW2-1.DLL
    LIBSTDC++-6.DLL
    Look in the Ming32Bit folder
    C:\Qt\5.12.2\mingw73_32\bin
Copy the yellow libs
Show the EXE runs
// My favorite tool is INNO Setup
```


Nice Tool: DependencyWalker

# Assertions

Q_ASSERT to assert or fail the process
