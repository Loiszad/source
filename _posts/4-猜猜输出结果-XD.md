---
title: 猜猜输出结果 XD~~
date: 2013-08-27 15:08:55
tags: Java
categories: Java
---

```java

public static void main(String[] args) {
	try {
		System.out.println(1);
		return;
	} catch (Exception e) {
		e.printStackTrace();
	} finally {
		System.out.println(2);
	}
}

```

**输出结果是1 2**