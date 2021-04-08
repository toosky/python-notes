# python-notes

### socket

#### udp client

```
import socket

def main():
    # 创建udp 套接字
    udp = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

    while True:
        # 获取用户输入
        send_data = input("请输入发送的信息:")

        # 退出
        if send_data == 'exit':
            break

        # 使用套接字发送接送数据(发送信息， 接收方地址)
        # udp.sendto(b"this is a test to send messgae",("192.168.20.171",8000))
        udp.sendto(send_data.encode('gbk'),('192.168.20.171',8000))

    # 套接字关闭
    udp.close()

if __name__ == "__main__":
    main()
```

#### udp server

```
import socket

def main():
    # 创建套接字
    udp = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

    # 绑定端口地址
    udp.bind(('',8000))

    while True:
        # 接收信息 最大1024个字节
        recv_data = udp.recvfrom(1024)
        print(recv_data)

    # 关闭套接字
    udp.close()

if __name__ == "__main__":
    import os
    try:
        main()
    except Exception as e:
        print(e)
    finally:
        os.system('pause')
```

接收信息格式：

(b'13131313\r\n', ('192.168.20.171', 10000))

***

#### tcp client

```
def main():
    import socket

    tcp = socket.socket(socket.AF_INET,socket.SOCK_STREAM)

    ip = input("请输入连接的地址：")
    port = int(input("请输入连接的端口："))
    tcp.connect((ip,port))

    while True:

        inpu = input()
        if inpu == 'exit':
            break
        tcp.send(inpu.encode('gbk'))

    tcp.close()

if __name__ == "__main__":
    try:
        import os,traceback
        main()
    except:
        traceback.print_exc()
    finally:
        os.system("pause")
```

#### tcp server

```
def main():
    import socket

    tcp = socket.socket(socket.AF_INET,socket.SOCK_STREAM)

    port = int(input("请输入端口："))
    tcp.bind(("",port))

    tcp.listen()

    client, addr = tcp.accept()

    while True:
        data = client.recv(1024).decode('gbk')
        print(str(addr)+":"+data)
        if data == 'exit':
            break
        client.send(data.upper().encode('gbk'))
    

    client.close()
    tcp.close()

if __name__ == "__main__":
    try:
        import os,traceback
        main()
    except:
        traceback.print_exc()
    finally:
        os.system('pause')
```



