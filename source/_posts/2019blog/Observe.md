---
title: Observe
date: 2019-11-01 11:38:33
tags:
---

纯JS实现一个观察者
<!-- more -->
``` javascript
class Observe {
  static __message = {};

  static on(type, fn) {
    if (typeof this.__message[type] === "undefined") {
      this.__message[type] = [fn];
    } else {
      this.__message[type].push(fn);
    }
  }
  static subscribe(type, args) {
    if (!this.__message[type]) return;
    for (let i = 0; i < this.__message[type].length; i++) {
      this.__message[type][i].call(this, args);
    }
  }
  static off(type, fn) {
    if (this.__message[type] instanceof Array) {
      let i = this.__message[type].length - 1;
      for (; i >= 0; i--) {
        this.__message[type][i] === fn && this.__message[type].splice(i, 1);
      }
    }
  }
}
```

调用
``` javascript
  Observe.on("say", function(data) {
    console.log(data);
  });
  Observe.subscribe("say", "123");
  Observe.subscribe("say", "321");

  Observe.on("hello", hello);
  function hello(res) {
    console.log(res);
  }
  Observe.subscribe("hello", "hello");
  Observe.subscribe("hello", "world");
  Observe.off("hello", hello);
  Observe.subscribe("hello", "world");
```