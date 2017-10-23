---
title: (二)swift notice
date: 2017-10-17 10:05:45
tags: Swift
categories: Swift
---

### 1.反转

```
(0...10).reversed()

```

### 2.utf8编码，每个汉字占3字节

### 3.字符串的格式化
```
let h=9
let m=8
let s=5

let formatStr = String(format:"%02d:%02d:%02d",h,m,s)
```

### 4.字符串的子串
```
let num = "15500008888"
let s = num.replacingOccurrences(of: "0000", with: "****")

//截取 0000  
let range = num.range(of: "0000")
let s1 = num[range!]
let s2 = num[index...]

var phoneNum = "15899998888"
let str = phoneNum[String.Index(encodedOffset: 3)...String.Index(encodedOffset: 6)]
phoneNum.replacingOccurrences(of: str, with: "****")
```

### 5.swift类可以不继承任何父类，oc不可以

### 6.模糊效果
```
let effectView = UIVisualEffectView(effect: UIBlurEffect(style: .light))
effectView.frame = CGRect(origin: CGPoint(x: 0, y: 0), size: CGSize(width: 200, height: 300))

view.addSubview(effectView)
```

### 7.自定义启动图
在控制器的viewdidload里添加imageview  然后淡化移除


### 8.可选解包和强制解包
不需要计算的时候可以用可选解包，反之用强制解包，因为可选项不能直接参与到计算！

### 9.内存分配视图分析循环引用

### 10. weak 和 unowned
weak: 弱引用

unowned: 修饰的对象是assign的，不会强引用，但是如果对象释放，指针地址不会变化，如果继续调用，就会出现野指针的问题


