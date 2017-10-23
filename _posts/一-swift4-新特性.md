---
title: (一)swift4 新特性
date: 2017-10-12 09:50:02
tags:
categories: Swift
---

## 开区间
swift4可以不指定区间的上界或者下界

### 1.无限序列
可以用开区间创建一个无限序列

`let arr = 1...`

### 2.zip函数
合并两个集合

### 3.集合的下标
在集合的下标中用开区间的话，集合的startIndex 和 endIndex会智能补充缺失的一边

```
let arr = [1,2,3,4,5,6]
arr[3...]  //取代arr[3..<arr.endIndex]
```


# 字符串

### 1.三引号
定义多行字符串，字符串中不需要写转义字符，结尾三引号的缩进，决定每一行头部被裁剪的空格是多少。

```
let str = """
		Hello World
		“你好啊”
		"""

```

### 2.Substring是字符串切片后的新类型
String和Substring两者都遵从StringProtocol    所以String和Substring行为很大程度上一样，Substring可以调用String的API。	

# 扩展
同文件内的扩展，private声明可见。

# Codable协议
在swift4.0 中，引入了新的Codable协议，可以让你在不添加其他特殊代码的情况下序列化和反序列化自定义的数据类型，从而不用担心值类型的丢失。更漂亮的是，你可以选择数据被序列化为什么样的格式：plist(XML)或者JSON。

```
struct Language:Codable {
    var name: String
    var version: Int
}

let swift = Language(name:"Swift",version:4)
let php = Language(name:"PHP",version:7)
let perl = Language(name:"Perl",version:6)

//JSON
let encoder = JSONEncoder()
let encoded = try? encoder.encode(swift)
if encoded != nil {
    if let json = String(data: encoded!,encoding:.utf8){
        print(json)
    }
}

let decoder = JSONDecoder()
if let decoded = try? decoder.decode(Language.self, from: encoded!)
{
    print(decoded.name)
}

//XML
//PropertyList
let propertyListEncoder = PropertyListEncoder()
let propertyListed = try? propertyListEncoder.encode(php)

let propertyDecoder = PropertyListDecoder()
if let value = try? propertyDecoder.decode(Language.self,from: propertyListed!)
{
   print(value.name)
}
```	