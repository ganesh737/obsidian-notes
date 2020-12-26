# 1 Memory Management

# 2 Collections

## QList vs QVector

QVector --> Continuous memory location
QList --> allocates as when required at random locations

QVector usually outperforms QList usually

## QHash

stores key value pairs for very fast lookup


## QSet

hash table based implementation from Qt
stores values in unspecified order and provides very fast lookup

## QMap

provides a red-black-tree-based dictionary
ordered and a little slower than QHash

## QLinkedList

stores a list of values and provides an iterator based access

use it if guaranteed contant time insertion in the middle of the list
iterates to items rathen than indeces

# 3 Working with settings

QSettings -> stores the key value pairs for an application... it may be in plain text so we need to encrypt if we really want to store some information ...

way to use it -
```c
QCoreApplication::setOrganizationName("syncknowlgedge");
QCoreApplication::setOrganizationDomain("syncknowledge.com");
QCoreApplication::setApplicationName("tester2");

QSettings settings(QCoreApplication::organizationName(), QCoreApplication::applicationName());

// save a settings
// settings.setValue("test", 123);

// read the setting back
qInfo() << settings.value("test").toString();
qInfo() << settings.value("test").toInt();
```

the stored information is available across reboot of the application is accessed with the organizationName, applicationName combo

Try to use groups as much as possible ... Adds additional layer for individual parts of the application to save their settings

```
// starts with -
settings.beginGroup(group);

// ends with -
settings.endGroup();
```

It saves as a key value pair with data type -
QString --> key
QVariant --> value

# 4 Working with File System

## QIODevice and QBuffer

QIODevice is QTs abstraction of the complete lower levels of a system. It can be used to open files, BT devices and many more.

QBuffer class provides a QIODevice interface for a QByteArray

Reads and writes are done with QByteArray

file and device data may need flush the data to the device with buffer.flush()

Always close the device with buffer.close()

## QDir

object can exist even if the folder does not exist so always check if the folder exists before usage

mkdir -> make directory in current directory
mkpath -> make the entire path

remove() -> remove named empty directory
removeRecursively() -> remove all files and folders that are subfolders

cdUp() -> up one folder path
current() -> current directory path object
currentPath() -> current directory path as QString

## QFileInfo

Gets file information like size, birthDate, lastModifiedTime, etc

## QStorageInfo

Use it for working with volumes of the system

## QFile

```c
QFile file(path);
file.write(QByteArray);
file.flush();
file.close();
```

## Reading File

Reading can be done as -
file - file.readAll() --> best for small files otherwise it takes up a lot of time
lines - file.readLine() --> best for text files and not for binary files
bytes - file.read() --> best for larger files or want to read as byte array

## QDataStream

Definite starting point with ending when we specify

## QTextStream

## QLockFile

avoids deadlock for file access

setStaleLockTime(time) to unlock after ms

# 5 Exploring QDebug

Available logging are -
qInfo()
qDebug()
qWarning()
qCritical()
qFatal()

## Message Handler

Use a logging class to simplify logging ... It should take care about logging to stdout, stderr, logfile ...

# 6 Encoding

ASCII -> American Standard Code for Information Interchange

UTF-8 --> variable width character encofing capable of encoding many language characters

use by setting in QTextStream with setCode("UTF-8")

base64 --> group of similar binary-to-text encoding schemes ... uses 6-bit data fields for each character
mainly used in transfering data

hex --> representation of the data in machine understandable format

QTextCodec

# 7 qCompress and qUncompress

uses zLib for compression and decompression

# 8 Serialization

Writing an object to hdd and reading it back later

read back in the same order as write

can save version information for version compatiiblity	

JSON Serialization qtci8_3

XML Serialization qtci8_4

# 9 Algorithms

qDeleteAll

qFill --> deprecated for std::fill()

qSort --> deprecated for std::sort()

qCopy --> deprecated for std::copy()

qEqual -->  deprecated for std::equal()

# 10 Working with OS

QSysInfo
qInfo() << "Boot Id: " << sys.bootUniqueId();
qInfo() << "Build: " << sys.buildAbi();
qInfo() << "Cpu: " << sys.buildCpuArchitecture();
qInfo() << "Kernel: " << sys.kernelType();
qInfo() << "Version: " << sys.kernelVersion();
qInfo() << "Mac: " << sys.macVersion();
qInfo() << "Windows: " << sys.windowsVersion();
qInfo() << "Host: " << sys.machineHostName();
qInfo() << "Product: " << sys.prettyProductName();
qInfo() << "Type: " << sys.productType();
qInfo() << "Version: " << sys.productVersion();

QProcess qtci10_2

QExit qtci10_3

# 11 Timers

QTimer::singleShot(timems, &functionName) --> Timer in current thread

QFileSystemWatcher for watching FS changes like files or dirs ... Any change to a file is treated as change to dir

# 12 Metadata

metadata is a way to accesss the meta information in terms of properties and methods available to all QObjects

setProperty to set property

creating own meta information qtci12_5
Q_CLASSINFO("Author", "Ganesh")

Q_DISABLE_COPY(classname)

# 13 Design Patterns in Qt

## Singleton

https://github.com/voidrealms/qtci13-1

## Builder

https://github.com/voidrealms/qtci13-2

## Factory

https://github.com/voidrealms/qtci13-3

## Pool

https://github.com/voidrealms/qtci13-4

## D-Pointer

https://github.com/voidrealms/qtci13-5
