# libcurl

## Programming Tutorial

### Setup

#### Installation on Ubuntu

```bash
sudo apt-get install libcurl4-openssl-dev
```

#### Compiling the Program: cflags

```bash
curl-config --cflags
```

#### Linker Flags

```bash
curl-confg --libs
```

#### Finding out the Available Features

```bash
curl-config --features
```

#### Finding out the Supported Protocols

```bash
curl-config --protocols
```

### Coding

#### Preparations for Using libcurl

##### Initialization
Use the below code for initialization of libcurl **once** in the process
```c
curl_global_init()
```

The options are a bit pattern to tell libcurl what are the libraries to be initialized.

The available options are -

1. Initialize all known sub modules
```c
CURL_GLOBAL_ALL
```
      This has the below options mainly -
    1. Initialization options for win32 sockets
```c
CURL_GLOBAL_WIN32
```
    2. Initialization for SSL
```c
CURL_GLOBAL_SSL
```

In case the initialization options are not mentioned, curl internally tries to find the best suitable options and initializes.

##### Cleanup

Once the program no longer uses libcurl, the below call should be performed -
```c
curl_global_cleanup()
```

This should be done once in a program’s life cycle.


#### Easy Interface

This the usual method that applications are using. It for easy initialization and working. The APIs return on success or error. So the application may be stuck in API call until the transfer is complete.

##### Initialization

Link: [curl easy init](https://curl.haxx.se/libcurl/c/curl_easy_init.html)

Use the below API for initialization -
```c
curl_easy_init()
```

* [Global initialization](#preparations-for-using-libcurl) is a must before easy initializing

##### Set Options

Link: [curl easy setopt](https://curl.haxx.se/libcurl/c/curl_easy_setopt.html)

Common Options that are set with categories -

###### Behavior Options
```c
CURLOPT_VERBOSE;           // verbose output from libcurl
CURLOPT_NOPROGRESS;        // no progress bar
CURLOPT_WILDCARDMATCH;     // wildcard match for filename
```

###### Error Options
```c
CURLOPT_STDERR;            // stderr replaces stream
CURLOPT_FAILONERROR;       // fail on HTTP 4xx errors
```

###### Network Options
```c
CURLOPT_URL;               // use URL to work on
CURLOPT_PATH_AS_IS;        // do not squash sequences like "/../" or "/./" in the URL
CURLOPT_PROTOCOLS;         // bitmap for disabling not required protocols
CURLOPT_DEFAULT_PROTOCOL;  // specify the default protocol
CURLOPT_CONNECT_TO;        // specify the host and port
CURLOPT_INTERFACE;         // bind connection to this locally
CURLOPT_LOCALPORT;         // bind connection to this port locally
CURLOPT_LOCALPORTRANGE;    // bind connection to this port range locally
CURLOPT_PORT;              // port number to connect to
```
[culropt url](https://curl.haxx.se/libcurl/c/CURLOPT_URL.html)
[curlopt path as is](https://curl.haxx.se/libcurl/c/CURLOPT_PATH_AS_IS.html)
[curlopt connect to](https://curl.haxx.se/libcurl/c/CURLOPT_CONNECT_TO.html)

###### HTTP Options

```bash
TODO
```

###### TFTP Options

```bash
TODO
```

###### FTP Options

```bash
TODO
```

###### Protocol Options

```bash
TODO
```

###### Connection Options

```bash
TODO
```

###### SSL & Security Options

```bash
TODO
```

###### SSH Options

```bash
TODO
```

#### Multi Interface

This method is for single threaded programs to act like multi-threaded. So the calls to libcurl contain a call back function so that on result, they are called for completion.

#### Shared Interface

In case multiple threads of a process need to use the same initialized libcurl interface, this the option to be used. It allows for multiple threads to get the same initialized handle for libcurl and perform thread specific requests.

### Sample Code & Testing

#### Code

The below sample code tries to fetch the file passed via command line argument.

Then, pushes it to stdout.

```c
#include <iostream>
#include <string>
#include <curl/curl.h>

int main(int argc, char* argv[])
{
    CURL* curlHandle;
    CURLcode ret;
    std::string url = "http://127.0.0.1:8000/";

    if(2 == argc) {
        url += std::string(argv[1]);
        std::cout << url << std::endl;
    }
    else {
        std::cerr << "Options are NOK" << std::endl;
        return -1;
    }

    //init libcurl
    curl_global_init(CURL_GLOBAL_ALL);

    //easy init
    curlHandle = curl_easy_init();

    // specify URL
    curl_easy_setopt(curlHandle, CURLOPT_URL, url.c_str());

    // get it
    ret = curl_easy_perform(curlHandle);

    if(CURLE_OK == ret) {
        std::cout << "Success !!!" << std::endl;
    }

    // cleanup curl stuff
    curl_easy_cleanup(curlHandle);

    // cleanup libcurl
    curl_global_cleanup();

    return 0;
}
```

#### Build

The build is performed with below commands -
```bash
g++ libcurl_easy_fetch_stdout.cpp -std=c++11 -L/usr/lib/x86_64-linux-gnu -lcurl
```

#### Test

The server used is the simpleHTTPServer provided with python.

It can be run as below -
```bash
python -m SimpleHTTPServer
```

This creates a server with the current directory.

So we can run the below command and output as below -
```bash
./a.out hello_world.txt
http://127.0.0.1:8000/hello_world.txt
hello, world!!!
Success !!!
```

For wrong files, the code needs to be fine tuned :P
```bash
./a.out hello_world.txt1
http://127.0.0.1:8000/hello_world.txt1
<head>
<title>Error response</title>
</head>
<body>
<h1>Error response</h1>
<p>Error code 404.
<p>Message: File not found.
<p>Error code explanation: 404 = Nothing matches the given URI.
</body>
Success !!!
```

It also needs to be checked if the output to stdout is a stream or only once complete transfer is complete!!!

# References

1. [programming tutorial](https://curl.haxx.se/libcurl/c/libcurl-tutorial.html)
2. [libcurl easy](https://curl.haxx.se/libcurl/c/libcurl-easy.html)
3. [libcurl multi](https://curl.haxx.se/libcurl/c/libcurl-multi.html)
4. [libcurl shared](https://curl.haxx.se/libcurl/c/libcurl-share.html)
5. [libcurl examples](https://curl.haxx.se/libcurl/c/example.html)


# Hashtags

#libcurl #networking #library #curl