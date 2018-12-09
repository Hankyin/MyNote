# QNetworkReply

QNetworkReply类包含了QNetworkAccessManager发送的请求的数据和头部信息。

QNetworkReply类包含了与一数据和元数据，

QNetworkReply是一个按序访问的QIODevice，这意味着一旦数据从对象中读取，设备就不再保存它了。因此保存数据的责任由应用程序负责。每当更多的数据从网络中接收和处理，readyRead()信号就会被发射。

当接收到数据时，也会发出downloadProgress（）信号，但是如果对内容进行了任何转换（例如，解压缩和删除协议开销），则其中包含的字节数可能不代表接收的实际字节数。

即使QNetworkReply是连接到回复内容的QIODevice，它也会发出uploadProgress（）信号，该信号指示具有此类内容的操作的上载进度。

**注意** ：不要在连接到error和finished的槽函数中删除这个对象，使用deleteLater。