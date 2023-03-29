[TOC]

# ����

>���򼯺ϲ������ظ���Ա�����򼯺��е�Ԫ�ؿ������򡣵��Ǻ��б�ʹ�������±���Ϊ�������ݲ�ͬ���ǣ�����ÿ��Ԫ������һ��������score����Ϊ��������ݡ�
>���򼯺Ϻ����Ԫ�ز����ظ�������score�����ظ���

![�б����Ϻ����򼯺����ߵ���ͬ��](../Image/�б����Ϻ����򼯺����ߵ���ͬ��.png)


# ����

1. ������
��1����ӳ�Ա

```cli
zadd key score memeber [score memeber ...]
```

�й�zadd������������Ҫע�⣺

- zadd ���������nx��xx��ch��incr �ĸ�ѡ�
  - nx:member���벻���ڣ��ſ������óɹ���������ӡ�
  - xx:member������ڣ��ſ������óɹ������ڸ��¡�
  - ch:���ش˴β��������򼯺�Ԫ�غͷ��������仯�ĸ���
  - incr:��score�����ӣ��൱�ں�����ܵ�zincrby��
- ���򼯺���ȼ����ṩ�������ֶΣ���Ҳ�д��ۣ�zadd��ʱ�临�Ӷ�ΪO(log(n)),sadd��ʱ�临�Ӷ�ΪO(1).

(2) �����Ա����

```cli
zcard key
```

(3) ����ĳ����Ա�ķ���

```cli
zscore key member
```

(4) �����Ա������

```cli
zrank key member
zrevrank key member

```

zrank�Ǵӷ����ӵ͵��߷���������zrevrank�Ӹߵ��׷���������
(������0��ʼ����)

��5�� ɾ����Ա

```cli
zrem key member [member ...]
```

��6�����ӳ�Ա�ķ���

```cli
zincrby key increment member
```

(7) ����ָ��������Χ�ĳ�Ա

```cli
zrange key start end [withscores]
zrevrange key start end [withscores]
```

���򼯺��ǰ��շ�ֵ�����ģ�zrange �Ǵӵ͵��߷��أ�zrevrange�Ӹߵ��ͷ��ء��������withscoreѡ�ͬʱ�᷵�س�Ա�ķ�����

(8) ����ָ��������Χ�ĳ�Ա

```cli
zrangebyscore key min max [withscores] [limit offset count]
zrevrangebyscore key max min [withscores] [limit offset count]
```

����zrangebyscore ���շ����ӵ͵��߷��أ�zrevrangebyscore�Ӹߵ��ͷ��ء� withscoresѡ���ͬʱ����ÿ����Ա�ķ�����[limit offset count] ѡ����������������ʼλ�ú͸�����

ͬʱ min��max ��֧�ֿ����䣨С���ţ��ͱ����䣨�����ţ���-inf ��+inf�ֱ��������С�����޴�

(9) ����ָ��������Χ��Ա����

```cli
zcount key min max
```

(10)ɾ��ָ�������ڵ�����Ԫ��

```cli
zremrangebyrank key start end
```

(11) ɾ��ָ��������Χ�ĳ�Ա

```cli
zremrangebysocre key min max
```

2. ���ϼ�Ĳ���

(1)����

```cli
zinterstore destination numkeys key [key ...] [weights weight [weight] [aggregate sum|min|max]
```

�����������϶࣬����۱ʽ���˵����

- destination: �������������浽�����
- numkeys:��Ҫ������������ĸ���
- key[key ...]:��Ҫ����������ļ���
- weights weight[weight...]��ÿ������Ȩ�أ�������������ʱ��ÿ������
��ÿ��member�Ὣ�Լ������������Ȩ�أ�ÿ������Ȩ��Ĭ����1��
- aggregate sum|min|max�������Ա�����󣬷�ֵ���԰���sum���ͣ���
min����Сֵ����max�����ֵ�������ܣ�Ĭ��ֵ��sum��

��user��ranking��2��Ȩ�ر�Ϊ0.5�����Ҿۺ�Ч��ʹ��max������
ִ�����²�����

```cli
zinterstore user:ranking:1_inter_2 2 user:ranking:1
user:ranking:2 weights 1 0.5 aggregate max
```

(2)����

```cli
zunionstore desctination numkeys key [key ...] [weight weight [weight ...]] [aggregate sum|min|max]
```

![���򼯺������ʱ�临�Ӷ�](../Image/���򼯺������ʱ�临�Ӷ�.png)

# �ڲ�����

���򼯺����͵��ڲ����������֣�

- ziplist(ѹ���б�)���°��Ѿ����listpack����
�����򼯺ϵ�Ԫ�ظ���С��zset-max-ziplistentries���ã�Ĭ��128������ͬʱÿ��Ԫ�ص�ֵ��С��zset-max-ziplist-value��
�ã�Ĭ��64�ֽڣ�ʱ��Redis����ziplist����Ϊ���򼯺ϵ��ڲ�ʵ�֣�ziplist
������Ч�����ڴ��ʹ�á�

- skiplist(��Ծ��)��
��ziplist����������ʱ�����򼯺ϻ�ʹ��skiplist��
Ϊ�ڲ�ʵ�֣���Ϊ��ʱziplist�Ķ�дЧ�ʻ��½���

# ʹ�ó���

>���򼯺ϱȽϵ��͵�ʹ�ó����������а�ϵͳ��

��1������û�����

```cli
zadd user:ranking:20160315 score member
```

(2)ȡ���û�����

```cli
zincrby user:ranking:20160315  increment member
```

(3) չʾ��ȡ��������ʮ���û�

```cli
zrevrangebyrank user:ranking:20160315 0 9 withscores
```

(4)չʾ�û���Ϣ�Լ��û�����

```cli
hgetall user:info:tom
zscore user:ranking:20160315 mike
zrank user:ranking:20160315 mike
```
