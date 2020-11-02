# Protocol Comparison

| Parameter               | TFTP                                                             | NFS                                                              | HTTP                                                             |
|-------------------------|------------------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|
| Abbreviation            | Trivial File Transfer                                            | Network File System                                              | HyperText Transfer Protocol                                      |
| Transport Layer         | UDP;TCP                                                          | UDP - default; TCP also supported                                | TCP/IP generally; RUDP is also an alternative                    |
| State Handling          | Statefull                                                        | Stateless                                                        | Stateless                                                        |
| Packet Size Limitation  | Defined by Transport Layer Protocol; IPv4 - 65535 (based on MTU) | Defined by Transport Layer Protocol; IPv4 - 65535 (based on MTU) | Defined by Transport Layer Protocol; IPv4 - 65535 (based on MTU) |
| Authentication          | No Authentication                                                | User Authentication                                              | Basic + Digest Access Authentication                             |
| Encryption              | NA                                                               | TLS; Kerberos                                                    | TLS (HTTPS)                                                      |
| Resume Transfer         | None                                                             | Yes (ver > 3)                                                    | Yes                                                              |
| Protocol Versions & Age | First: 1981 by K.Sollins; Current: Rev RFC7440(Jan 2015)         | First: 1984 by Sun Microsystems; Current: NFSv4.2 (Nov 2016)     | First: 1991; Current: 3.0 (2018)                                 |
| Transfer Speeds (kbps)  |                                                                  |                                                                  |                                                                  |
| CPU Usage for 1GB data  |                                                                  |                                                                  |                                                                  |


# References
* [TFTP](https://tools.ietf.org/html/rfc1350)
* [NFSv4.2](https://tools.ietf.org/html/rfc7862)
* [Optimizing NFS Performance](https://tldp.org/HOWTO/NFS-HOWTO/performance.html)
* [NFS Classes for Extended Filesystem](https://docs.oracle.com/cd/E19455-01/806-1067/6jacl3e6p/index.html)

# HashTags
#protocols #applicationprotocols #osi #tftp #nfs #http