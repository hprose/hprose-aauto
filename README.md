# Hprose for AAuto Quicker

[![Join the chat at https://gitter.im/hprose/hprose-aauto](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/hprose/hprose-aauto?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

>---
- **[Introduction](#introduction)**
- **[Usage](#usage)**
    - **[Synchronous Invoking](#synchronous-invoking)**
    - **[Synchronous Exception Handling](#synchronous-exception-handling)**
    - **[Asynchronous Invoking](#asynchronous-invoking)**
    - **[Asynchronous Exception Handling](#asynchronous-exception-handling)**

>---

## Introduction

*Hprose* is a High Performance Remote Object Service Engine.

It is a modern, lightweight, cross-language, cross-platform, object-oriented, high performance, remote dynamic communication middleware. It is not only easy to use, but powerful. You just need a little time to learn, then you can use it to easily construct cross language cross platform distributed application system.

*Hprose* supports many programming languages, for example:

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

Through *Hprose*, You can conveniently and efficiently intercommunicate between those programming languages.

This project is the implementation of Hprose for AAuto Quicker.

## Usage

### Synchronous Invoking
Hprose for AAuto Quicker only has a client, you can use it like this:

```lua
import hprose;

io.open();

var client = hprose.client.create("http://hprose.com/example/");
io.print(client.hello("world"));

execute("pause")
io.close();
```

### Synchronous Exception Handling

If an error occurred on the server, or your service function/method throw an exception. it will be sent to the client, and the client will throw it as an exception. You can use the try statement to catch it.

### Asynchronous Invoking

When you develop winform application, you'd better to use asynchronous invoking:

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

### Asynchronous Exception Handling

When using asynchronous invoking, you need to pass an error callback function after succuss callback function to receive the server-side exception. If you omit this callback function, the client will ignore the exception, like never happened.
