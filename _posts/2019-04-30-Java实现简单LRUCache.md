---
layout:     post
title:      简单的LRU Cache实现(Java)
subtitle:   利用LinkedHashMap实现简单缓存
date:       2019-04-30
author:     月光下的海
header-img: img/post-bg-desk.jpg
catalog: true
tags:
    - Java
    - LRU
    - Cache

---

### LRU简介

- LRU是英文` Least Recently Used`的缩写 ，翻译过来就是“最近最少使用”，LRU缓存就是使用这种原理实现，简单的说就是缓存一定量的数据，当超过设定的阈值时就把一些过期的数据删除掉。采用LRU算法实现的话就是将最老的数据删掉。

#### 代码实现

- 可利用Java中现有的数据结构`LinkedHashMap` 实现。根据`LinkedHashMap` 本身已经实现了顺序存储的特点，重写removeEldestEntry 方法。
- 继承方式


```java
package com.anthony.util;

import java.util.LinkedHashMap;
import java.util.Map;
/**
 * 利用LinkedHashMap实现简单缓存
 * Created by luxuebing on 2019/4/30
 */
public class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private static final float DEFAULT_LOAD_FACTOR = 0.75f;
    private final int CACHE_SIZE;
    public LRUCache(int cacheSize) {
        //tru表示按照访问顺序进行排序
        super((int) (Math.ceil(cacheSize / DEFAULT_LOAD_FACTOR) + 1), DEFAULT_LOAD_FACTOR, true);
        CACHE_SIZE = cacheSize;
    }
    /**
     * 当map中数据量超出指定的缓存大小时，删除最老的数据
     */
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > CACHE_SIZE;
    }
    public static void main(String[] args) {
        LRUCache<Integer, Object> cache = new LRUCache(4) {{
            put(1, "h");
            put(2, "e");
            put(3, "l");
            put(4, "l");
            put(5, "o");
        }};
        cache.forEach((k, v) -> System.out.println(k + "==" + v));
    }
}

Console:
2==e
3==l
4==l
5==o
Process finished with exit code 0
```

- 代理方式

```java
package com.anthony.util;

import java.util.LinkedHashMap;
import java.util.Map;
import java.util.Set;

/**
 * 线程同步的LRUCache
 * Created by luxuebing on 2019/4/30
 */
public class SynchronizedLRUCache<K, V> {
    private final int CACHE_SIZE;
    private final float DEFAULT_LOAD_FACTOR = 0.75f;
    private final LinkedHashMap<K, V> map;

    public SynchronizedLRUCache(int cacheSize) {
        CACHE_SIZE = cacheSize;
        int capacity = (int) Math.ceil(CACHE_SIZE / DEFAULT_LOAD_FACTOR) + 1;
        map = new LinkedHashMap(capacity, DEFAULT_LOAD_FACTOR, true) {
            @Override
            protected boolean removeEldestEntry(Map.Entry eldest) {
                return size() > CACHE_SIZE;
            }
        };
    }

    public synchronized void put(K key, V value) {
        map.put(key, value);
    }

    public synchronized V get(K key) {
        return map.get(key);
    }

    public synchronized void remove(K key) {
        map.remove(key);
    }

    public synchronized int size() {
        return map.size();
    }

    public synchronized void clear() {
        map.clear();
    }

    public synchronized Set<Map.Entry<K, V>> entrySet() {
        return map.entrySet();
    }

    public synchronized boolean containsKey(K key) {
        return map.containsKey(key);
    }

    @Override
    public String toString() {
        StringBuffer sb = new StringBuffer("[");
        map.forEach((k, v) -> sb.append(k).append("=").append(v).append(","));
        sb.delete(sb.length() - 1, sb.length()).append("]");
        return sb.toString();
    }

    public static void main(String[] args) {
        SynchronizedLRUCache<Object, Object> cache = new SynchronizedLRUCache<>(4){{
            put(1, 1);
            put(2, 2);
            put(3, 3);
            put(4, 4);
            put(5, 5);
        }};
        System.out.println(cache);
    }
}

Console:
[2=2,3=3,4=4,5=5]

Process finished with exit code 0
```