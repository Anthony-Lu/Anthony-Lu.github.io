---

layout:     post
title:      为什么 `Map` 的 `get()` 方法参数是 `Object` 而不是泛型
subtitle:   
date:       2021-08-01
author:     月光下的海
header-img: img/1.jpg
catalog: true
tags:
    - Java
    - Map

---

##### 背景

- 最近看到一个有意思的话题: `Java` 中的 `Map` 的 `get()` 方法参数为什么是 `Object` 而不是使用泛型 `K` 

 > 后来在网上找到了 `Map` 的作者(同时也是 `Java Collection FrameWork` 的作者) Josh Bloch 的一段关于此问题的说明:
 >  - that they attempted to generify the get method of Map, remove method and some other, but "it simply didn't work". There are too many reasonable programs that could not be generified if you only allow the generic type of the collection as parameter type.
 >  - The example given by him is an intersection of a List of Numbers and a List of Longs.
 >  - Josh Bloch 给出的例子是使用 `List<Number>` 和 `List<Long>` 时的场景。我的理解大意就是为了兼容，因为 `get()` 方法的规范并没有要求你要检索的 `key` 与该方法参数的类型相同，它们依赖于equals方法规范的实现。
 >  - 比如在 `List#equals()` 方法的规范中提到:如果两个列表以相同的顺序包含相同的元素，则它们被定义为相等。此定义可确保 `equals()` 方法在 `List` 接口的不同实现中能够正常工作。
 >  - 假设给定的是一个 `Map<ArrayList,String>`,但是 `get()` 时候使用的 `key` 是一个具有相同内容的 `LinkedList`,参数被设计为泛型 `K` 时就会编译不通过了。
 

##### 附注:
- [https://stackoverflow.com/questions/857420/what-are-the-reasons-why-map-getobject-key-is-not-fully-generic](https://stackoverflow.com/questions/857420/what-are-the-reasons-why-map-getobject-key-is-not-fully-generic)
- [https://stackoverflow.com/questions/104799/why-arent-java-collections-remove-methods-generic](https://stackoverflow.com/questions/104799/why-arent-java-collections-remove-methods-generic)



