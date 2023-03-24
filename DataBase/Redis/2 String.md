[TOC]

# String 常用命令

1. 设置值

```cli
set key value [ex seconds] [px milliseconds] [nx|xx]
```

set 命令有几个选项

- ex seconds:为键设置秒级过期时间
- px milliseconds：为键设置毫秒级过期时间
- nx:键必须不存在，才可以设置成功，用于添加
- xx:与nx相反，键必须存在，才可以设置成功，用于更新。
  
除了 set 选项，Redis还提供了setnx和setnx两个命令：它们的作用和ex和nx选项是一样的。

```cli
setex key seconds value
setnx key value
```
setnx可以作为分布式锁的一种实现方案。

2. 获取值

```cli
get key
```

3. 批量设置值

```cli
mset key value [key value]
```

5. 批量获取值

```cli
mget key [key ...]
```
批量操作优点：
有助于提供业务处理效率，但是要注意的是每次批量操作所发送的命令数不是无节制的，如果数量过多可能造成Redis阻塞或者网络拥塞。

6. 计数

```cli
incr key
```

incr 命令用于对值做自增操作，返回结果分为三种情况：

- 值不是整数，返回错误
- 值是整数，返回自增后的结果
- 键不存在，按照值为0自增，返回结果1。

除了incr 命令，Redis 提供了decr（自增）、incrby(自增指定数字)、
decrby(自减指定数字)、incrbyfloat(自增浮点数)：
7. 追加值
