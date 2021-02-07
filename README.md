# 基于Socket接口实现自定义协议通信
浙江大学zqf计算机网络Lab7
### 作业要求
根据自定义的协议规范，使用Socket编程接口编写基本的网络应用软件。
* 掌握C语言形式的Socket编程接口用法，能够正确发送和接收网络数据包
* 开发一个客户端，实现人机交互界面和与服务器的通信
* 开发一个服务端，实现并发处理多个客户端的请求
* 程序界面不做要求，使用命令行或最简单的窗体即可
* 功能要求如下： 
  * 运输层协议采用TCP  
  * 客户端采用交互菜单形式，用户可以选择以下功能：
    * 连接：请求连接到指定地址和端口的服务端
    * 断开连接：断开与服务端的连接
    * 获取时间: 请求服务端给出当前时间
    * 获取名字：请求服务端给出其机器的名称
    * 活动连接列表：请求服务端给出当前连接的所有客户端信息（编号、IP地址、端口等）
    * 发消息：请求服务端把消息转发给对应编号的客户端，该客户端收到后显示在屏幕上
    * 退出：断开连接并退出客户端程序
  * 服务端接收到客户端请求后，根据客户端传过来的指令完成特定任务：
    * 向客户端传送服务端所在机器的当前时间
    * 向客户端传送服务端所在机器的名称
    * 向客户端传送当前连接的所有客户端信息
    * 将某客户端发送过来的内容转发给指定编号的其他客户端
    * 采用异步多线程编程模式，正确处理多个客户端同时连接，同时发送消息的情况
* 根据上述功能要求，设计一个客户端和服务端之间的应用通信协议
* 本实验涉及到网络数据包发送部分不能使用任何的Socket封装类，只能使用最底层的C语言形式的Socket API

### 自定义协议
| type | id | content |
| ---- | ---- | ---- |

* 3位的type表示数据包类型，相应数据包含以下类型：
  * 100: 响应获取时间请求，返回时间信息
  * 101: 响应获取服务器名字请求，返回服务器名字信息
  * 110：响应获取客户端列表请求，返回客户端列表信息
  * 111：响应发送消息请求，返回信息发送成功消息
  * 000：响应断开请求，返回成功断开信息
  * 001：响应连接请求，返回成功连接信息
* 5位的id表示客户端编号，最多支持32个客户端，不使用时为默认值11111
* string类型的消息内容content
