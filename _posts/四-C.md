---
title: (四)C++
date: 2014-8-13 14:02:55
tags:
categories: C
---

### 1.引用

1. 引用是C++比C扩充的一种数据类型，引用是为对象取一个别名，不占存储空间，引用类型说明符为&
1. 在声明引用变量类型时，必须同时使之初始化，即声明它是谁的引用，初始化之后，不能再次成为其他变量的引用，例如上面已经声明了int&a=b，就不能再声明int&a=c；
1. 引用不能为NULL，例如int&a=NULL是错误的。


### 2.友元

1. 定义为友元就可以直接访问类的私有成员 

```
class A{
	friend class B;
}
```


### 3.标准库容器

```
	//list
    list<string> arr;
    
    arr.push_back("1");
    arr.push_back("2");
    
    for(list<string>::iterator it=arr.begin();it!=arr.end();it++){
        cout<<*it<<"\n";
    }
    
    //map
    map<string,string> m;
    m["name"] = "wwwww";
    cout<<m["name"];
    
```


### 4.字符串

```
	//字符串的拼接
    string str = "hello";
    str += "world";
    cout<<str<<"\n";
    
    //不同类型的写入
    stringstream ss;
    ss<<"hello "<<"world "<<20;
    cout<<ss.str()<<"\n";
    
```


### 5.文件操作

```
	 //写
    ofstream of("data.txt");
    of<<"hello world";
    of.close();
    
    //读
    ifstream myIf("data.txt");
    stringbuf buf;
    myIf>>&buf;
    cout<<buf.str()<<"\n";
```













