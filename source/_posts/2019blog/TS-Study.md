---
title: TS-Study
date: 2020-01-10 11:11:27
tags:
---

typescript说起来用了一段时间了，但是感觉还是只停留在简单的定义数据类型。
下面是用ts高级类型来灵活处理数据的一些总结。
<!-- more -->

# Partial *将一个类型的成员属性全部设置为可选模式*

我们先定义一个Person类
``` javascript
type Person = {
  name:string;
  age:number
}
```
之前都是在各个属性加？实现可选属性，这样如果属性繁多，想一个个添加就很麻烦，这时候工具函数Partial就派上用场了。
``` javascript
type Partial<T> = {
  [P in keyof T]?:T[P];
}

// 这样Person所有属性都变成可选的了，除了属性值是对象的
type PartialPerson = Partial<Person>
```

现在再加上contact属性
``` javascript
type Person = {
  name:string;
  age:number;
  contact:{
    phone:number;
    email:string;
  }
}
type PartialPerson = Partial<Person>
```
这样的话contact是可选的，但是contact里面的属性依然不是，所以可以优化一下Partial
``` javascript
type deepPartial<T> = {
  [P in keyof T]?T[P] extends Object ? deepPartial<T[P]> : T[P]
}

type partialPerson = deepPartial<Person>
```
这样做了判断，如果属性是对象的话，会将对象属性中的属性也配置为可选的

# Required *设置所有属性必选*
根据上面可选还能衍生出必选的高级类型设置
``` javascript
type Required<T> = {
  [P in keyof T]-?:T[P];
}
```
-表示去除？*(可选)*，就是必选

# Readonly *属性只可读*
``` javascript
type Readonly<T> = {
  readonly [P in keyof T]:T[P]
}
```

# Record *转化属性的类型*
``` javascript
type Record<K extends keyof any,T> = {
  [P in K]:T
}
type AnimalType = 'cat' | 'dog' | 'frog';

interface AnimalDescription {
  name: string, title: string
}

type AnimalObj = Record<AnimalType, AnimalDescription>

const AnimalMap: AnimalObj= {
   cat: { name: '猫', title: 'cat' },
   dog: { name: '狗', title: 'dog' },
   frog: { name: '蛙', title: 'wa' },
};
```

`K extends keyof T` 这样是表示K把T的属性名作为类型，K就是T的属性名
