
java.net.SocketException: Can't assign requested address

解决：
虚拟机参数：
`-DJava.NET.preferIPv4Stack=true`

