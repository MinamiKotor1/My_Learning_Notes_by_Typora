# PAC-GPT

[MinamiKotor1/NetworkPacketGenerator: Generate network packets using generative modeling (github.com)](https://github.com/MinamiKotor1/NetworkPacketGenerator)

[TOC]

## 心得

### Python代码中使用代理访问Openai api

#### api-key

```python
# 在openai api platform上获取api-key
openai.api_key = 'openai-api-key' 
```

#### 设置代理

```python
# Set the proxy URL and port
# clash记得开全局
proxy_url = 'http://127.0.0.1'
proxy_port = '7890'

# Set the http_proxy and https_proxy environment variables
os.environ['http_proxy'] = f'{proxy_url}:{proxy_port}'
os.environ['https_proxy'] = f'{proxy_url}:{proxy_port}'
```

### pickle包

pickle包用于序列和反序列化数据，其生成的文件格式名为.pkl

### scapy包

Scapy 是一个强大的 Python 库，主要用于创建、发送、嗅探和解析网络数据包（pcap）。它支持多种网络协议，并且可以轻松地进行网络数据包的构建和解码。

#### 构建数据包

```python
from scapy.all import IP, ICMP

packet = IP(dst="192.168.1.1")/ICMP()
```

#### 发送数据包

```python
from scapy.all import send

send(packet)
```

#### 嗅探数据包

```python
from scapy.all import sniff

packets = sniff(count=10)
packets.summary()
```

#### 解析数据包

```python
packet.show()
```

#### 保存和读取数据包

```python
from scapy.utils import wrpcap, rdpcap

wrpcap('packets.pcap', packets)
packets = rdpcap('packets.pcap')
```

### .pcappng

.pcap pro

> ### .pcapng 文件格式介绍
>
> .pcapng（Packet Capture Next Generation）文件格式是网络数据包捕获文件的一种格式，是 libpcap 格式（.pcap）的后续版本。与 .pcap 文件相比，.pcapng 提供了更多的功能和灵活性。以下是 .pcapng 文件格式的详细介绍：
>
> #### 1. **文件结构**
>
> .pcapng 文件由一个或多个块（block）组成，每个块包含不同类型的信息。主要的块类型包括：
>
> - **Section Header Block (SHB)**：每个 .pcapng 文件的开始都由一个 SHB 块开始，它包含文件格式的版本、字节顺序等全局信息。
> - **Interface Description Block (IDB)**：描述捕获接口的信息，如链路类型、接口名称等。
> - **Enhanced Packet Block (EPB)**：包含捕获的数据包，支持存储精确的时间戳和其他捕获元数据。
> - **Simple Packet Block (SPB)**：类似于 EPB，但不包含时间戳等额外信息。
> - **Name Resolution Block (NRB)**：包含主机名和 IP 地址的解析信息。
> - **Custom Block (CB)**：允许用户定义自定义的数据块。
>
> #### 2. **主要块类型详细描述**
>
> - **Section Header Block (SHB)**：
>   - **作用**：定义一个新的数据捕获会话。
>   - **字段**：
>     - Block Type：标识块类型（0x0A0D0D0A）。
>     - Block Total Length：块的总长度。
>     - Byte Order Magic：字节顺序标记（用于识别文件的字节序）。
>     - Major Version：主版本号。
>     - Minor Version：次版本号。
>     - Section Length：整个捕获节的长度。
>
> - **Interface Description Block (IDB)**：
>   - **作用**：描述捕获接口的参数。
>   - **字段**：
>     - Block Type：标识块类型（0x00000001）。
>     - Block Total Length：块的总长度。
>     - LinkType：链路层类型（如以太网、Wi-Fi 等）。
>     - SnapLen：捕获的数据包的最大长度。
>
> - **Enhanced Packet Block (EPB)**：
>   - **作用**：存储捕获的数据包及其元数据。
>   - **字段**：
>     - Block Type：标识块类型（0x00000006）。
>     - Block Total Length：块的总长度。
>     - Interface ID：接口标识符。
>     - Timestamp：捕获时间戳。
>     - Captured Packet Length：捕获的数据包长度。
>     - Original Packet Length：原始数据包长度。
>     - Packet Data：实际捕获的数据包。
>
> - **Simple Packet Block (SPB)**：
>   - **作用**：存储简单数据包信息，不包含时间戳。
>   - **字段**：
>     - Block Type：标识块类型（0x00000003）。
>     - Block Total Length：块的总长度。
>     - Packet Length：数据包长度。
>     - Packet Data：实际捕获的数据包。
>
> - **Name Resolution Block (NRB)**：
>   - **作用**：存储 IP 地址和主机名的解析信息。
>   - **字段**：
>     - Block Type：标识块类型（0x00000004）。
>     - Block Total Length：块的总长度。
>     - Records：包含 IP 地址和对应主机名的记录。
>
> - **Custom Block (CB)**：
>   - **作用**：允许用户存储自定义信息。
>   - **字段**：
>     - Block Type：标识块类型（0x00000BAD）。
>     - Block Total Length：块的总长度。
>     - Pen：私有企业编号（用于标识自定义块的所有者）。
>     - Data：自定义数据。
>
> #### 3. **优势与特点**
>
> - **灵活性**：.pcapng 文件允许在一个文件中捕获来自多个接口的数据包，并支持更多的元数据，如精确的时间戳、接口信息、名称解析等。
> - **扩展性**：支持自定义块，允许用户存储特定需求的数据。
> - **兼容性**：虽然 .pcapng 提供了更多功能，但大多数支持 .pcap 的工具也能处理 .pcapng 文件（如 Wireshark）。
>
> #### 4. **使用工具**
>
> - **Wireshark**：一个广泛使用的网络协议分析器，支持读取和写入 .pcapng 文件。
> - **tcpdump**：一个命令行工具，用于捕获和分析网络流量，支持 .pcapng 文件格式。
> - **Scapy**：一个强大的 Python 库，用于数据包处理和分析，支持读取和写入 .pcapng 文件。
>
> ### 结论
>
> .pcapng 文件格式提供了比 .pcap 更加丰富和灵活的捕获数据存储方式，适用于复杂的网络分析任务。它的结构设计允许在一个文件中存储更详细和多样化的信息，极大地提高了网络分析的效率和精度。