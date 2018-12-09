# 使用Qt 进行网络编程

Qt 网络模块提供了允许你编写TCP/IP客户端服务器的类，它提供了一些底层类比如QTcpSocket，QTcpServer和QUdpSocket等代表网络底层概念的类，还提供了一些上层类比如QNetworkRequest，QNetworkReply和QNetworkAccessManager来使用通用协议进行网络操作，还提供了QnetworkConfiguration，QNetworkConfigurationManager和QNetworkSession来实施不记名管理。

## 用于网络编程的Qt C++类

Namespaces



| [QSsl](qssl.html) | Declares enums common to all SSL classes in Qt Network |
| ----------------- | ------------------------------------------------------ |
|                   |                                                        |

Classes



| [QAbstractNetworkCache](qabstractnetworkcache.html)          | The interface for cache implementations                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [QNetworkCacheMetaData](qnetworkcachemetadata.html)          | Cache information                                            |
| [QHstsPolicy](qhstspolicy.html)                              | Specifies that a host supports HTTP Strict Transport Security policy (HSTS) |
| [QHttpMultiPart](qhttpmultipart.html)                        | Resembles a MIME multipart message to be sent over HTTP      |
| [QHttpPart](qhttppart.html)                                  | Holds a body part to be used inside a HTTP multipart MIME message |
| [QNetworkAccessManager](qnetworkaccessmanager.html)          | Allows the application to send network requests and receive replies |
| [QNetworkCookie](qnetworkcookie.html)                        | Holds one network cookie                                     |
| [QNetworkCookieJar](qnetworkcookiejar.html)                  | Implements a simple jar of QNetworkCookie objects            |
| [QNetworkDiskCache](qnetworkdiskcache.html)                  | Very basic disk cache                                        |
| [QNetworkReply](qnetworkreply.html)                          | Contains the data and headers for a request sent with QNetworkAccessManager |
| [QNetworkRequest](qnetworkrequest.html)                      | Holds a request to be sent with QNetworkAccessManager        |
| [QNetworkConfigurationManager](qnetworkconfigurationmanager.html) | Manages the network configurations provided by the system    |
| [QNetworkConfiguration](qnetworkconfiguration.html)          | Abstraction of one or more access point configurations       |
| [QNetworkSession](qnetworksession.html)                      | Control over the system's access points and enables session management for cases when multiple clients access the same access point |
| [QAuthenticator](qauthenticator.html)                        | Authentication object                                        |
| [QDnsDomainNameRecord](qdnsdomainnamerecord.html)            | Stores information about a domain name record                |
| [QDnsHostAddressRecord](qdnshostaddressrecord.html)          | Stores information about a host address record               |
| [QDnsLookup](qdnslookup.html)                                | Represents a DNS lookup                                      |
| [QDnsMailExchangeRecord](qdnsmailexchangerecord.html)        | Stores information about a DNS MX record                     |
| [QDnsServiceRecord](qdnsservicerecord.html)                  | Stores information about a DNS SRV record                    |
| [QDnsTextRecord](qdnstextrecord.html)                        | Stores information about a DNS TXT record                    |
| [QHostAddress](qhostaddress.html)                            | IP address                                                   |
| [QHostInfo](qhostinfo.html)                                  | Static functions for host name lookups                       |
| [QNetworkDatagram](qnetworkdatagram.html)                    | The data and metadata of a UDP datagram                      |
| [QNetworkAddressEntry](qnetworkaddressentry.html)            | Stores one IP address supported by a network interface, along with its associated netmask and broadcast address |
| [QNetworkInterface](qnetworkinterface.html)                  | Listing of the host's IP addresses and network interfaces    |
| [QNetworkProxy](qnetworkproxy.html)                          | Network layer proxy                                          |
| [QNetworkProxyFactory](qnetworkproxyfactory.html)            | Fine-grained proxy selection                                 |
| [QNetworkProxyQuery](qnetworkproxyquery.html)                | Used to query the proxy settings for a socket                |
| [QAbstractSocket](qabstractsocket.html)                      | The base functionality common to all socket types            |
| [QLocalServer](qlocalserver.html)                            | Local socket based server                                    |
| [QLocalSocket](qlocalsocket.html)                            | Local socket                                                 |
| [QSctpServer](qsctpserver.html)                              | SCTP-based server                                            |
| [QSctpSocket](qsctpsocket.html)                              | SCTP socket                                                  |
| [QTcpServer](qtcpserver.html)                                | TCP-based server                                             |
| [QTcpSocket](qtcpsocket.html)                                | TCP socket                                                   |
| [QUdpSocket](qudpsocket.html)                                | UDP socket                                                   |
| [QSslCertificate](qsslcertificate.html)                      | Convenient API for an X509 certificate                       |
| [QSslCertificateExtension](qsslcertificateextension.html)    | API for accessing the extensions of an X509 certificate      |
| [QSslCipher](qsslcipher.html)                                | Represents an SSL cryptographic cipher                       |
| [QSslConfiguration](qsslconfiguration.html)                  | Holds the configuration and state of an SSL connection       |
| [QSslDiffieHellmanParameters](qssldiffiehellmanparameters.html) | Interface for Diffie-Hellman parameters for servers          |
| [QSslEllipticCurve](qsslellipticcurve.html)                  | Represents an elliptic curve for use by elliptic-curve cipher algorithms |
| [QSslError](qsslerror.html)                                  | SSL error                                                    |
| [QSslKey](qsslkey.html)                                      | Interface for private and public keys                        |
| [QSslPreSharedKeyAuthenticator](qsslpresharedkeyauthenticator.html) | Authentication data for pre shared keys (PSK) ciphersuites   |
| [QSslSocket](qsslsocket.html)                                | SSL encrypted socket for both clients and servers            |

Detailed Description

To include the definitions of the module's classes, use the following directive:

```

  #include <QtNetwork>

```

To link against the module, add this line to your [qmake](../qmake/qmake-manual.html) .pro file:

```

  QT += network
 
```

## 用于HTTP和FTP的高层网络操作

网络访问API是一些类的集合，这些类提供了通用的网络操作，

QNetworkRequest类代表了一个网络请求，它的行为同时也像一个通用的信息容器，包含了与请求相关的数据，比如任何头部信息和使用的加密信息。当一个请求对象被创建的时候需要指定一个URL，这决定了请求使用的协议，目前支持HTTP，FTP和本地文件URL的上传下载。

网络操作的协调工作由QNetworkAccessManager类负责，当一个请求被创建后，这个类就会分发它并且发射信号来报告它的进度，这个manager还负责使用cookies来在客户端上存储数据，认证请求，和使用代理。

网络请求的回复由QNetworkReply负责，当请求被分发后QNetworkAccessManager就会创建回复对象。QNetworkReply提供的信号可以被用来监视每个独立的回复，或者开发者可以选择使用manager的信号来实现这个目的，从而抛弃对于回复的引用。因为QNetworkReply是QIODevice的子类，回复可以处理成同步或异步的，。

每个应用或者库可以创建一个或多个QNetworkAccessManager实例来处理网络通信。