# Hprose for AAuto Quicker

>---
- **[简介](#简介)**
- **[使用](#使用)**
    - **[同步调用](#同步调用)**
    - **[同步异常处理](#同步异常处理)**
    - **[异步调用](#异步调用)**
    - **[异步异常处理](#异步异常处理)**

>---

## 简介

*Hprose* 是高性能远程对象服务引擎（High Performance Remote Object Service Engine）的缩写。

它是一个先进的轻量级的跨语言跨平台面向对象的高性能远程动态通讯中间件。它不仅简单易用，而且功能强大。你只需要稍许的时间去学习，就能用它轻松构建跨语言跨平台的分布式应用系统了。

*Hprose* 支持众多编程语言，例如：

* AAuto Quicker
* ActionScript
* ASP
* C++
* Dart
* Delphi/Free Pascal
* dotNET(C#, Visual Basic...)
* Golang
* Java
* JavaScript
* Node.js
* Objective-C
* Perl
* PHP
* Python
* Ruby
* ...

通过 *Hprose*，你就可以在这些语言之间方便高效的实现互通了。

本项目是 Hprose 的 AAuto Quicker 语言版本实现。

## 使用

### 同步调用

Hprose for AAuto Quicker 的客户端同步调用使用很简单：

```lua
import hprose;

io.open();

var client = hprose.client.create("http://hprose.com/example/");
io.print(client.hello("world"));

execute("pause")
io.close();
```

### 同步异常处理

服务器端如果发生错误，或者服务器端的服务函数或方法抛出异常，将会被发送到客户端，并且将在客户端抛出异常，你可用使用try语句来捕获它。

### 异步调用

当在开发 winform 应用时，你最好使用异步调用，这样在通讯中界面也不会发生卡住假死的现象：

```lua
import win.ui;
import hprose;

/*DSG{{*/
var winform = ..win.form(text="AAuto Form";right=599;bottom=399)
winform.add(
button={cls="button";text="button";left=50;top=194;right=129;bottom=223;z=1};
edit={cls="edit";left=45;top=39;right=269;bottom=177;edge=1;multiline=1;z=2}
)
/*}}*/

winform.button.oncommand = function(id,event){
    var client = hprose.client.create("http://hprose.com/example/");
    client.hello("async world", function(result) {
        winform.edit.text = 'result: \r\n' ++ result;
    }, function(name, err) {
        winform.edit.text = 'error: \r\n' ++ err;
    });
}

winform.show()
win.loopMessage();
```

### 异步异常处理

当时用异步调用时，你需要在成功回调函数之后再传递一个错误回调函数来接收服务器端异常（就像上面例子那样）。如果你忽略了该回调函数，客户端将忽略异常，就像从来没发生过一样。
