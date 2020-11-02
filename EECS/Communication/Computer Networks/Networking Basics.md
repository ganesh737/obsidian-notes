Linux: TCP/IP socket
        Ip address
        Port Number

* Server Side
* Client Side

* Option: non-blocking
* Always start the server first -> listen in specific port number
* Next start the client -> connect to server()

write()/read()
send()/recv()

Note:
    Data frame/data transfer
    Structure of data frame
    [header][body][footer]
    header: destination, data frame length
    body: data in binary
    footer: some character to define that is the end of data frame

Boost has one library for streaming. Need to explore
Streaming is written chunk by chunk
Chunk size is decided based on memory sender/receiver, network speed, performance of sender/receiver

IP address can be part of configuration or something
Usually DNS server is used to resolve it

UDP Con --> no ack

Socket() can be extended for Bluetooth connectivity -> unique ID needs to be explored

1 socket 1 port
1 Linux process multiple ports are possible - not possible for single IP, single port

Ref Links:
* [Socket Programming](https://www.geeksforgeeks.org/socket-programming-cc)
* [Socket manpage](https://man7.org/linux/man-pages/man2/socket.2.html)
* [TCP manpage](https://man7.org/linux/man-pages/man7/tcp.7.html)
* [Poco C++ Libraries](https://pocoproject.org/docs/Poco.Net.html)
* [boost::beast](https://www.boost.org/doc/libs/1_70_0/libs/beast/doc/html/beast/using_io.html)