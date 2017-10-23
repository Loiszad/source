---
title: Socket
date: 2013-09-11 14:51:01
tags: Java
categories: Java
---


## 1.客户端和服务端

**阻塞：从流中读数据、server.accept

```java

public class Client {
	public static void main(String[] args) {
		Socket socket = null;
		BufferedWriter bw = null;// 向服务器写
		BufferedReader br = null;// 表示从键盘读入
		BufferedReader br1 = null;// 表示从服务器读
		try {
			socket = new Socket("10.211.55.2", 12345);// 在客户端建立一个socket，同时申请连接ip为localhost的主机，访问端口号为12345的应用程序
			System.out.println("申请连接服务器。。");
			String str = "hello";
			bw = new BufferedWriter(new OutputStreamWriter(
					socket.getOutputStream()));
			br = new BufferedReader(new InputStreamReader(System.in));
			br1 = new BufferedReader(new InputStreamReader(
					socket.getInputStream()));
			str = br.readLine();// 从键盘读入一句 阻塞的
			bw.write(str);
			bw.newLine();
			bw.flush();
			String s1 = br1.readLine();
			System.out.println("服务器说：" + s1);

		} catch (UnknownHostException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}

public class Server {
	public static void main(String[] args) {
		ServerSocket server = null;
		BufferedReader br = null;// 表示从输入流中读数据
		BufferedWriter bw = null;// 表示向客户端说话
		try {
			server = new ServerSocket(12345);
			System.out.println("服务器已建立，等待客户端连接。。");
			Socket ss = server.accept();// 连接客户端，返回一个socket  阻塞的
			System.out.println("已有客户端连接。。。");
			br = new BufferedReader(new InputStreamReader(ss.getInputStream()));
			bw = new BufferedWriter(
					new OutputStreamWriter(ss.getOutputStream()));
			String str = br.readLine();// 表示接收客户端的输入  阻塞的
			// int len = 0;
			// char[] c = new char[20];
			// len = br.read(c);
			// String str = new String(c, 0, len);
			System.out.println("from：" + ss.getLocalAddress());
			System.out.println("port：" + ss.getPort());
			System.out.println("客户端说：" + str);
			String s1 = "你好，我是服务器";
			bw.write(s1);
			bw.newLine();
			bw.flush();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

}


```