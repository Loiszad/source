---
title: (三)swift面向对象
date: 2017-10-23 13:45:23
tags:
categories: Swift
---

### 1.Swift中的KVC
```
① 基本数据类型不能设置成可选的，而且要设置初始值，否则KVC会崩溃

② 属性不能是private的

③ KVC的方法是OC的方法，在运行时给对象发送消息，所以在使用KVC方法之前，应该调用super.init() 保证对象实例化完成
```