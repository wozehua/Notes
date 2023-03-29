[toc]

# ����

>���ϣ�set������Ҳ���������������ַ���Ԫ�أ������б����Ͳ�һ
�����ǣ������в��������ظ�Ԫ�أ����Ҽ����е�Ԫ��������ģ�����ͨ��
�����±��ȡԪ�ء�
һ�����������Դ洢 2^32^-1��Ԫ�ء�
Redis����֧�ּ����ڵ���ɾ�Ĳ飬ͬʱ��֧�ֶ������ȡ��������
�������

1. �����ڲ���

1.1 ���Ԫ��

```cli
sadd key element [element ...]
```

���ؽ��Ϊ��ӳɹ���Ԫ�ظ���
1.2 ɾ��Ԫ��

```cli
srem key element [element]
```

���ؽ��Ϊ�ɹ�ɾ��Ԫ�ظ���

1.3 ����Ԫ�ظ���

```cli
scard key
```

scard��ʱ�临�Ӷ�ΪO��1���������������������Ԫ�أ�����ֱ����
Redis�ڲ��ı���

1.4 �ж�Ԫ���Ƿ��ڼ�����

```cli
sismember key element
```

�������Ԫ��element�ڼ����ڷ���1����֮����0

1.5 ����Ӽ��Ϸ���ָ��Ԫ�ظ���

```cli
srandmember key [count]
```

[count]�ǿ�ѡ�����������дĬ��Ϊ1��

1.6 �Ӽ����������Ԫ��

```cli
spop key
```

spop�������ԴӼ������������һ��Ԫ��
srandmember��spop��������Ӽ���ѡ��Ԫ�أ����߲�ͬ����spop����
ִ�к�Ԫ�ػ�Ӽ�����ɾ������srandmember���ᡣ

1.7 ��ȡ����Ԫ��

```cli
smembers key
```

��ȡ��������Ԫ�أ����ҷ��ؽ��������ġ�

**ע��**

>smembers��lrange��hgetall�����ڱȽ��ص�������Ԫ�ع��������
��Redis�Ŀ����ԣ���ʱ�����ʹ��sscan�����

2. ���ϼ����

2.1 �������Ͻ���

```cli
sinter key [key ...]
```

2.2 �������ϵĲ���

```cli
sunion key [key ...]
```

2.3 �������ϵĲ

```cli
sdiff key [key ...]
```

����Ĳ���Ե�һ��keyΪ׼

2.4 ����������������Ľ������

```cli
sinterstore destination key [key...]
sunionstore destination key [key...]
sdiffstore  destination key [key...]
```

>���ϼ��������Ԫ�ؽ϶������»�ȽϺ�ʱ������Redis�ṩ������
�������ԭ����+store�������ϼ佻������������Ľ��������
destination key�С�

![���ϳ�������ʱ�临�Ӷ�](Image/���ϳ�������ʱ�临�Ӷ�.png)

# �ڲ�����

������϶���ڲ����������֣�

- intset���������ϣ����������е�Ԫ�ض���������Ԫ�ظ���С��set-max-intset-entries���ã�Ĭ��512����ʱ��Redis��ѡ��intset����Ϊ���ϵ��ڲ�ʵ
�֣��Ӷ������ڴ��ʹ�á�
- hashtable����ϣ���������������޷�����intset������ʱ��Redis��ʹ
��hashtable��Ϊ���ϵ��ڲ�ʵ�֡�

1����Ԫ�ظ��������Ҷ�Ϊ����ʱ���ڲ�����Ϊintset��
2.1����Ԫ�ظ�������512�����ڲ������Ϊhashtable��
2.2)��ĳ��Ԫ�ز�Ϊ����ʱ���ڲ�����Ҳ���Ϊhashtable

# ʹ�ó���

>�������ͱȽϵ��͵�ʹ�ó����Ǳ�ǩ��tag����

(1) ���û���ӱ�ǩ

```cli
sadd u:1:tags tag1 tag2 tag3
sadd user:2:tags tag2 tag3 tag5
...
sadd user:k:tags tag1 tag2 tag4
```

(2) ����ǩ����û�

```cli
sadd tag1:users user:1 user:3
sadd tag2:users user:1 user:2 user:3
...
sadd tagk:users user:1 user:2
...
```

�û��ͱ�ǩ�Ĺ�ϵά��Ӧ����һ��������ִ�У���ֹ��������ʧ����ɵ����ݲ�һ�£��й���ν������������һ������.

**������ʾ**

�������͵�Ӧ�ó���ͨ��Ϊ���¼��֣�
��sadd=Tagging����ǩ��
��spop/srandmember=Random item�����������������齱��
��sadd+sinter=Social Graph���罻����
