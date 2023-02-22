
<h1 style="text-align:center">通信</h1>

--------------------------------------------------------------------------------
[返回目录](outline.md)

tips:

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 串口](#-1-串口-)
  - [1.1. 第三方库 pyserial](#-11-第三方库-pyserial-)
    - [1.1.1. 基本流程](#-111-基本流程-)
    - [1.1.2. serial 类](#-112-serial-类-)
    - [1.1.3. 列举所有串口](#-113-列举所有串口-)
- [2. 网络](#-2-网络-)
  - [2.1. 以太网基础](#-21-以太网基础-)
  - [2.2. 标准库 socket](#-22-标准库-socket-)
    - [2.2.1. 基本](#-221-基本-)
    - [2.2.2. 创建 socket](#-222-创建-socket-)
    - [2.2.3. socket 类](#-223-socket-类-)
    - [2.2.4. 函数](#-224-函数-)
- [3. PCAP-NG 解析](#-3-pcap-ng-解析-)
  - [3.1. PCAPNG 文件结构](#-31-pcapng-文件结构-)
  - [3.2. 第三方库 python-pcapng](#-32-第三方库-python-pcapng-)
- [4. CRC](#-4-crc-)
  - [4.1. 第三方库:  crcmod](#-41-第三方库--crcmod-)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 串口

## 1.1. 第三方库 pyserial
* 安装: `pip install pyserial`
* 注意内部库名称为 `serial`
* [官方文档](https://pythonhosted.org/pyserial/)

### 1.1.1. 基本流程
``` python
import serial  # 注意库名称为 serial
# from serial import Serial
import time

ser = serial.Serial("COM3", 115200, timeout=5)  # 默认打开串口
tx_dat = ser.write(b"testing")  # 注意发送 bytes
time.sleep(1)
if rx_len := ser.in_waiting:
    rx_dat = ser.read(rx_len)
ser.close()
```
1. 创建串口对象: `Serial(..)`
1. 读/写(读/写数据都是 ==bytes== 类型)
    * 读操作: 是阻塞的, 要先查询有多少个字节, 除非已设置 timeout
1. 关闭串口: `对象.close()`

### 1.1.2. serial 类
* 构造: `Serial(*args, **kwargs)`
    * `port`: 串口名称
    * `baudrate`: 波特率, 默认 `9600`
    * `bytesize`: 数据位宽度, 默认 `8`
    * `parity`: 校验, 可选 `N\E\O\M\S`, 默认 `N`
    * `stopbits`: 停止位宽度, 可选 `1\1.5\2`, 默认 `1`
    * `timeout`: 读操作的 timeout
    * ...

* 主要方法
    分类 | 方法                                    | 说明
    -----|-----------------------------------------|--------------------------
    控制 | open()                                  | 打开串口
    ^    | close()                                 | 关闭
    读取 | read(size=1)                            | 读 n bytes, 阻塞, 除非设置 timeout
    ^    | read_all()                              | 读取全部, 阻塞
    ^    | read_until(terminator=b'\n', size=None) | 一直读到某个字符
    ^    | readline(size=-1)                       | 读取一行, 行终结符为 b'\n'
    ^    | readlines(hint=-1)                      | 读取所有行
    ^    | readall()                               | 一直读到 EOF
    写入 | write(data)                             | 写数据 (bytes 类型)
    ^    | writelines(lines)                       | 写n行数据
    ^    | flush()                                 | flush, 等所有数据写完

* 主要属性
    分类 | 成员          | 说明
    -----|---------------|-----------------------
    设置 | port          | 串口号
    ^    | baudrate      | 波特率
    ^    | bytesize      | 数据位宽度
    ^    | parity        | 校验, `N\E\O`: 无校验、奇校验、偶校验
    ^    | stopbits      | 停止位宽度
    ^    | timeout       | 超时
    ^    | write_timeout | 写超时设置
    状态 | is_open       | 是否已打开
    ^    | closed        | 是否已关闭
    ^    | in_waiting    | 缓存在未读的字节数
    ^    | name          | 串口名称, 可自定义

### 1.1.3. 列举所有串口
* `serial.tools.list_ports.comports()`
    * `from serial.tools.list_ports import comports()`
    * 返回 `list(ListPortInfo)`
    * 可使用 `len(返回值)` 获取串口数
    * 可用 `返回值[索引].device/description/hwid` 获取基本信息

--------------------------------------------------------------------------------
# 2. 网络

## 2.1. 以太网基础
* TCP流程
    ![TCP流程](/assets/TCP流程.png)
* UDP流程
    ![UDP连接](/assets/UDP连接.jpg)

## 2.2. 标准库 socket

### 2.2.1. 基本
* TCP 基本流程 (服务器)
    1. 创建 socket 连接, 嵌套字 type 为`SOCK_STREAM`
    1. bind 地址
    1. 监听 (listen)
    1. 等 client 发起连接后 accept
    1. 发送或接收
    1. 关闭
* TCP 基本流程 (客户端)
    1. 创建 socket 连接, 嵌套字 type 为`SOCK_STREAM`
    1. 发起连接 connect
    1. 发送或接收
    1. 关闭

* UDP基本流程
    1. 创建 socket 连接, 嵌套字 type 为`SOCK_DGRAM`
    1. 无需connect, 【可选】bind
    1. 发送或接收
    1. 关闭

* 示例
    * UDP 发送
        ``` python
        import socket
        udpSocket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
        sendArr = ('192.168.31.174',65535)
        udpSocket.sendto(b'testing...', sendArr)
        udpSocket.close()
        ```
    * UDP 接收
        ``` python
        import socket

        udpSocket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

        udpSocket.bind(("", 7789))
        recvData = udpSocket.recvfrom(1024)
        content, destInfo = recvData

        print("content is %s"%content)
        print("content is %s"%content.decode("utf-8"))
        print(recvData)

        udpSocket.close()
        ```

### 2.2.2. 创建 socket
* `socket(family=AF_INET, type=SOCK_STREAM, proto=0, fileno=None) -> socket 对象`
* `socketpair(..) -> socket 对象`
* `create_server(..) -> socket 对象`
* `create_connection(..) -> socket 对象`
其中:
* family
    * `AF_INET`: 网络协议 IPV4
        * 地址: `(host, port)`
            * host: 字符串, 网址 (如: siat.ac.cn) 或IP地址 (如: 127.0.0.1)
                * `''`表示任意地址
                * `'<broadcast>'`表示广播地址
            * port: integer
    * `AF_INET6`: 网络协议 IPV6
    * `AF_PACKET`: 底层网络接口 `(ifname, proto[, pkttype[, hatype[, addr]]])`
        * `ifname`: String specifying the device name.
        * `proto`: An in network-byte-order integer specifying the Ethernet protocol number.
        * `pkttype`: Optional integer specifying the packet type:◾PACKET_HOST (the default) - Packet addressed to the local host.
            * `PACKET_BROADCAST`: Physical-layer broadcast packet.
            * `PACKET_MULTIHOST`: Packet sent to a physical-layer multicast address.
            * `PACKET_OTHERHOST`: Packet to some other host that has been caught by a device driver in promiscuous mode.
            * `PACKET_OUTGOING`: Packet originating from the local host that is looped back to a packet socket.
        * `hatype`: Optional integer specifying the ARP hardware address type.
        * `addr`: Optional bytes-like object specifying the hardware physical address, whose interpretation depends on the device.
* type 包括: TCP协议`SOCK_STREAM` (默认), UDP协议`SOCK_DGRAM`, 底层协议`SOCK_RAW`, ...

### 2.2.3. socket 类
* 方法:
    分类   | 方法                                     | 说明
    -------|------------------------------------------|-----------------------------------------
    服务器 | bind(address)                            | 绑定地址
    ^      | listen([backlog])                        | 监听
    ^      | accept()                                 | 接受客户端连接, 返回 (socket object, address info)
    ^      | close()                                  | 关闭 socket
    客户端 | connect(address)                         | 连接远端
    ^      | connect_ex(address)                      | 连接远端, 返回 errno
    ^      | close()                                  | 关闭 socket
    发送   | send(data[, flags])                      | 发送数据, 返回计数
    ^      | sendall(data[, flags])                   | 发送全部数据
    ^      | sendto(data[, flags], address)           | 发送到指定地址, 返回计数
    ^      | sendfile(file[, offset[, count]])        | 发送文件
    接收   | recv(buffersize[, flags])                | 接受N个数据, 返回 bytes
    ^      | recv_into(buffer, [nbytes[, flags]])     | 接受N个数据, 存入指定 bytes
    ^      | recvfrom(buffersize[, flags])            | 接受N个数据, 返回 (data, address info)
    ^      | recvfrom_into(buffer[, nbytes[, flags]]) | 接受N个数据, 返回 (nbytes, address info)
    设置   | setsockopt(...)                          | 设置 socket 属性
    ^      | getsockopt                               | 查询 socket 属性
    ^      | setblocking(flag)                        | 设置是否阻塞
    ^      | getblocking()                            | 查询是否阻塞
    ^      | settimeout(timeout)                      | 设置超时
    ^      | gettimeout()                             | 查询超时
    ^      | set_inheritable(inheritable)             | 设置 socket 是否可继承
    ^      | get_inheritable()                        | 查询 socket 是否可继承
    ^      | getpeername()                            | 查询远端地址
    ^      | getsockname()                            | 查询本地地址
    其他   | makefile(...)                            | 将一个 I/O stream 连接到 socket
    ^      | detach()                                 | 断开 I/O stream 和 socket 的连接
    ^      | fileno()                                 | socket 文件描述符
    ^      | dup()                                    | 复制一个 socket
    ^      | share(process_id)                        | 分享另一个进程中的 socket
    ^      | shutdown(flag)                           | 关闭接收/发送侧
    ^      | ioctl(cmd, option)                       | -* 成员
    * family: 协议栈
    * type: 协议
    * proto: 以太网协议编号
    * timeout: 超时

### 2.2.4. 函数
分类     | 方法                                       | 说明
:--------|--------------------------------------------|------------------------------------------
地址     | inet_aton(string)                          | string 地址 -> bytes 地址
^        | inet_ntoa(packed_ip)                       | bytes 地址 -> string 地址
^        | inet_pton(af, ip)                          | 根据协议栈将 string 地址 转为 bytes 地址
^        | inet_ntop(af, packed_ip)                   | 根据协议栈将 bytes 地址 转为 string 地址
^        | getaddrinfo(...)                           | 获取地址信息
字节顺序 | htonl(integer)                             | 32位整数 -> 网络字节顺序的整数
^        | htons(integer)                             | 16位无符号整数 -> 网络字节顺序的整数
^        | ntohl(integer)                             | 网络字节顺序的整数 -> 32位整数
^        | ntohs(integer)                             | 网络字节顺序的整数 -> 16位无符号整数
socket   | fromfd(fd, family, type[, proto])          | 从文件描述符的副本创建 socket
^        | fromshare(info)                            | 从 socket.share(pid) 返回的 bytes 对象创建 socket
^        | socketpair(...)                            | 创建一对儿 socket
^        | create_connection(...)                     | 连结到指定地址, 并返回 socket
文件     | dup(integer)                               | 复制一个 socket 文件描述符
^        | close(integer)                             | 关闭一个 socket 文件描述符
设置     | setdefaulttimeout(timeout)                 | 设置默认超时, 单位 s
^        | getdefaulttimeout()                        | 查询默认超时, 单位 s
^        | gethostname()                              | 查询主机名称
^        | gethostbyname(host)                        | 查询主机地址
^        | gethostbyname_ex(host)                     | 查询主机地址, 返回 (name, aliaslist, addresslist)
^        | gethostbyaddr(host)                        | 查询主机信息, 返回 (name, aliaslist, addresslist)
^        | getnameinfo(sockaddr, flags)               | - 返回 (host, port)
^        | getprotobyname(name)                       | - 返回 integer
^        | getservbyname(servicename[, protocolname]) | - 返回 integer
^        | getservbyport(port[, protocolname])        | - 返回 string
^        | getfqdn(name='')                           | -

--------------------------------------------------------------------------------
# 3. PCAP-NG 解析

## 3.1. PCAPNG 文件结构
* pcapng 文件由多个 block 组成
    * block 结构
        ```
        0                   1                   2                   3
         0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        |                          Block Type                           |
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        |                      Block Total Length                       |
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        /                          Block Body                           /
        /          /* variable length, aligned to 32 bits */            /
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        |                      Block Total Length                       |
        +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
        ```
    * bolck 类型
        * 必要的 block
            * `Section Header Block`: 包含: 大小端 (用 `'<'` 或 `'>'` 表示), 硬件设备描述, OS 描述, 应用程序描述..等信息, 字符用 UTF-8 编码
            * `Interface Description Block`: 包含: 网络设备名称, 设备描述, 时间分辨率, 设备操作系统..等信息, 字符用 UTF-8 编码
        * 可选的 block
            * `Enhanced Packet Block`: 数据帧的信息, 包括: 网络设备ID, 时间戳 (2 个, 组成 64-bit 无符号时间戳), 捕获长度, 帧长度, 帧数据..等
            * `Simple Packet Block`: 简化的数据帧的信息, 仅包括: 帧长度, 帧数据
            * `Interface Statistics Block`: 包含: 网络设备ID, 时间戳 (2 个, 组成 64-bit 无符号时间戳), 起/止时间戳, 接收的帧数, 丢弃的帧数..等信息
            * `Name Resolution Block`:
* 文件结构
    ```
    Section Header
    |
    +- Interface Description
    |  +- Simple Packet
    |  +- Enhanced Packet
    |  +- Interface Statistics
    |
    +- Name Resolution
    ```

## 3.2. 第三方库 python-pcapng
> [官方文档](https://python-pcapng.readthedocs.io/en/latest/)
* 基本流程
    ``` python {.line-numbers}
    from pcapng import FileScanner
    from pcapng.blocks import SectionHeader, InterfaceDescription, EnhancedPacket, SimplePacket

    with open(path, "rb") as fp:                    # 打开 pcapng 文件
        scanner = FileScanner(fp)                   # 创建扫描器
        for block in scanner:                       # 获取 block
            if isinstance(block, EnhancedPacket):   # 判断是那种 block
                dat = block.packet_data             # 通过属性或方法, 获取 block 的具体信息
                ...                                 # 具体分析程序
    ```

--------------------------------------------------------------------------------
# 4. CRC

## 4.1. 第三方库:  crcmod
> [官方文档](http://crcmod.sourceforge.net/)

* 其中包括两个 module:
    * crcmod: 自定义CRC
    * predefined: 预定义的CRC

*  预定义CRC的使用
    * 方法1:
        1. 导入: `import crcmod.predefined`
        1. 初始化对象: `对象 = crcmod.predefined.PredefinedCrc(预定义的CRC模式字符串)` , 其中预定义的CRC模式字符串需要查表
        1. 必要时重置CRC `对象 = 对象.new()`
        1. 使用1次或多次计算CRC: `对象.update(bytes类型数据)`
        1. 获取校验值:
            * 成员变量 对象.crcValue
            * 方法 `对象.digest() -> bytes`
            * 方法 `对象.hexdigest() -> hex str`
    * 方法2:
        1. 导入: `import crcmod.predefined`
        1. 创建函数 `函数名 = crcmod.predefined.mkPredefinedCrcFun(预定义的CRC模式字符串)`
        1. 使用函数 `函数名(bytes类型数据) -> int`