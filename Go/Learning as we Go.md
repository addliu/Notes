## Learning as we Go

[TOC]

> **《学习Go语言(Golang)》**，中文教程出自[Learning Go zh cn](https://github.com/gunsluo/Learning-Go-zh-cn)
>
> Go语言学习笔记。



### 函数

**延迟代码**

对于下面这张代码：

```go
func ReadWrite() bool{
    file.Open("file")
    
    if failureX {
        file.Close() // 第一次调用
        return false
    }
    
    if failureY {
        file.Close() // 第二次调用
        return false
    }
    
    file.Close() // 第三次调用
    return true
}
```

这里一共调用了3次`file.Close()`方法，为了解决这些，Go 有了 `defer` 语句。在 `defer` 后指定的函数会在函数退出前调用。使用**延迟代码**技术可以优雅地简化代码，代码如下：
```go
func ReadWrite() bool{
    file.Open("file")
    defer file.Close()
    if failureX {
        return false
    }    
    if failureY {
        return false
    }    
    return true
}
```

可以将多个函数放入延迟列表中，延迟列表中的的函数按照后进先出(**LIFO**)的顺序执行。

### 包

包是函数和数据的集合。用`package`关键字定义一个包。文件名不需要与包名一致。包名的约定是使用*小写字符*。Go包可以由多个文件组成，但是使用相同的`package <name>`这一行。对于以下`even.go`中定义一个叫做`even`包
```go
package even

func Even(i int) bool { //可导出函数
    return i % 2 == 0
}

func odd(i int) bool { //私有函数
    return i % 2 == 1
}
```
名称以大写字母起始的是*可导出*的，可以在包外部调用。小写字母起始的是*私有*的。构建该包，需要将包复制到**$GOPATH**的相应目录：如下
```shell
% mkdir $GOPATH/src/even
% cp even.go $GOPATH/src/even
% go build
% go install
```
> 运行`go build`命令最好是到相应的文件夹（*$GOPATH/src/even*）下。否则可能会报出一些奇奇怪怪的错误。

> 公有函数的名字以大写字母开头，私有函数的名字以小写字母开头。这个规则同样适用于定义在包中的其他名字（新类型、全局变量）。注意，“大写” 的含义并不仅限于 US ASCII，它被扩展到了所有大小写字母表（拉丁文、希腊文、斯拉夫文、亚美尼亚文和埃及古文）。

