[TOC]

# ����

>��ϣ������ָ��ֵ��������һ����ֵ�Խṹ��
>����value={{field1��value1}��...{fieldN��valueN}}

![3](Image/��ϣ���ַ����Ա�.png)

# ����

1. ����ֵ

```cli
hset key field value
```

���óɹ��᷵��1����֮�᷵��0
Redis �ṩ�� hsetnx������ǵĹ�ϵ���� set��setnx����һ����ֻ�����������ɼ����field��

2. ��ȡֵ

```cli
hget key field
```

�������field�����ڣ��᷵��nil;

3. ɾ�� field

```cli
 hdel key field [field ...]
```

hdel ��ɾ��һ������ field�����ؽ��Ϊ�ɹ�ɾ��field�ĸ�����

4. ����field����

```cli
hlen key
```

6. �������û��ȡ field-value

```cli
hmget key field [field ...]
hmset key field value [field value]
```

>hmset �� hmget �ֱ����������úͻ�ȡ field-value, hmset ��Ҫ�Ĳ�����key �Ͷ��field-value, hmget ��Ҫ�Ĳ����� key�Ͷ��field.

8. �ж� field�Ƿ����

```cli
hexists key field
```

>���ڷ��ؽ��1��������ʱ����0��

10. ��ȡ���� field

```cli
hkeys key
```

>hkeys ����Ӧ�ý�hfields ��Ϊǡ����������ָ����ϣ�����е�fields

12. ��ȡ����value

```cli
hvals key
```

14. ��ȡ���е�field-value

```cli
hgetall key
```

**ע��**
>��ʹ��hgetallʱ�������ϣԪ�ظ����Ƚ϶࣬���������Redis�Ŀ��ܡ�
>���������Աֻ��Ҫ��ȡ����field,����ʹ��hmget��
>���һ��Ҫ��ȡȫ�� field-value,����ʹ��hscan���������ὥ��ʽ������ϣ���͡�

16. hincrby hincrbyfloat

```cli
hincrby key field
hincrbyfloat key field
```

>hincrby��hincrbyfloat������incrby��incrbyfloat����һ�����������ǵ���������filed��

18. ����value���ַ�������

```cli
hstrlen key field
```

20. ��ϣ���������ʱ�临�Ӷ�
![��ϣ���������ʱ�临�Ӷ�](Image/��ϣ���������ʱ�临�Ӷ�.png)

# �ڲ�����

- ziplist(ѹ���б�)��

>����ϣ����Ԫ��С�� hash-max-ziplist-entries���ã�Ĭ��512����ͬʱ����ָ��С��hash-max-ziplist-value ���ã�Ĭ��64���ֽڣ�ʱ��Redis��ʹ��ziplist��Ϊ��ϣ���ڲ�ʵ�֡���ziplistʹ�ø��ӽ��յĽṹʵ�ֶ��Ԫ�ص������洢�������ڽ�ʡ�ڴ淽���hashtable�������㡣

- listpack(�����б�)

>����Ǵ�ziplist->quicklist->listpack һ�����ݱ��
>�����ص������һ���������ڴ�ռ������յر������ݣ�ͬʱΪ�˽�ʡ�ڴ�ռ䣬listpack �б���ʹ���˶��ֱ��뷽ʽ������ʾ��ͬ���ȵ����ݣ���Щ���ݰ����������ַ�����

- hashtable(��ϣ��)

>����ϣ�����޷�����ziplist������ʱ��Redis��ʹ
��hashtable��Ϊ��ϣ���ڲ�ʵ�֣���Ϊ��ʱziplist�Ķ�дЧ�ʻ��½�����
hashtable�Ķ�дʱ�临�Ӷ�ΪO��1����

# ʹ�ó���

��ϵ�����ݱ��¼�������û���Ϣ
![ʹ�ù�ϣ���ͻ����û���Ϣ](Image/��ϣ���ͻ����û���Ϣ.png)
**ע��**

- ��ϣ������ϡ��ģ�����ϵ�����ݿ�����ȫ�ṹ���ģ������ϣ����
ÿ���������в�ͬ��field������ϵ�����ݿ�һ������µ��У������ж�ҪΪ
������ֵ����ʹΪNULL����

- ��ϵ�����ݿ���������ӵĹ�ϵ��ѯ����Redisȥģ���ϵ�͸��Ӳ�ѯ
�������ѣ�ά���ɱ��ߡ�

**���ַ��������û���Ϣ**

1. ԭ���ַ������� ��String��

```cli
set u:1:name tom
set u:1:age 23
set u:1:city fuzhou
```

�ŵ㣺��ֱ�ۣ�ÿ�����Զ�֧�ָ��²���
ȱ�㣺ռ�ù���ļ����ڴ�ռ���ʽϴ�ͬʱ�û���Ϣ�ھ��ԱȽϲ���Դ��ַ���һ�㲻������������ʹ�á�

2. ���л��ַ������� (���û���Ϣ���л�����һ��������)

```cli
set u:1 serialize(userinfo)
```

�ŵ㣺�򻯱�̣���������ʹ�����л������ύ�ڴ��ʹ����
ȱ�㣺���л��ͷ����л���һ���Ŀ����£�ͬʱÿ�θ������Զ���Ҫ��ȫ������ȡ�����з����л������º������л���Redis�С�

3. ��ϣ���ͣ�ÿ���û�����ʹ��һ��field-value,����ֻ��һ�������档

```cli
hmset u:1 name tom age 13 city fuzhou 
```

�ŵ㣺 ��ֱ�ۣ����ʹ�ú�����Լ����ڴ�ռ��ʹ�á�
ȱ�㣺Ҫ���ƹ�ϣ��listpack��hashtable�����ڲ������ת����hashtable �����ĸ����ڴ档
