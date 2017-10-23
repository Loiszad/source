---
title: IO
date: 2013-09-04 16:31:37
tags: Java
categories: Java
---

## 一、流的分类

**1.按流向分：输入流和输出流**
**2.按单位分：字节流和字符流**
**1.按功能分：节点流和处理流**



## 二、遍历文件并过滤

```java
File[] f1 = file.listFiles(new FileFilter() {

			@Override
			public boolean accept(File pathname) {
				if (pathname.toString().contains("user")) {
					return true;
				}
				return false;
			}
		});

```


## 三、流的读写

```java

//字节
int len = 0;
byte[] b = new byte[1024 * 1024];
while ((len = is.read(b)) != -1) {
	os.write(b, 0, len);
}

```


## 五、内存流 

```java

//ByteArrayOutputStream往内存写  ByteArrayInputStream从内存读
String str = "helloworld";
ByteArrayOutputStream baos = new ByteArrayOutputStream();
baos.write(str.getBytes());
System.out.println(baos.toString());// 通过toString从内存流中获取数据
ByteArrayInputStream bais = new ByteArrayInputStream(baos.toByteArray());
int temp = 0;
while ((temp = bais.read()) != -1) {
	System.out.println((char) temp);
}

```

## 六、随机读取文件 RandomAccessFile

```java
File file = new File("c:\\pro\\ee.txt");
RandomAccessFile raf = new RandomAccessFile(file, "rw");
System.out.println("-->" + raf.getFilePointer());

int temp = raf.read();
System.out.println((char) temp);
System.out.println("-->" + raf.getFilePointer());
raf.skipBytes(4);// 向后跳过4个字节
System.out.println("-->" + raf.getFilePointer());
temp = raf.read();
System.out.println((char) temp);
raf.seek(1);// 将指针设置距离开头1个字节
System.out.println("-->" + raf.getFilePointer());
System.out.println((char) temp);

```
