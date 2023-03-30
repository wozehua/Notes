
[toc]

# ����

>Redis �ṩ��redis-cli��redis-server��redis-benchmark��shell���ߡ�

1. -r

-r(repeat) ѡ���������ִ�ж�Ρ����������������ִ������ping
���

```cli
redis-cli -r 3 ping
```

2. -i

-i��interval��ѡ�����ÿ������ִ��һ���������-iѡ������-rѡ��һ��ʹ�ã�����Ĳ�����ÿ��1��ִ��һ��ping���һ��ִ��5�Σ�

```cli
redis-cli -r 5 -i 1 ping
```

ע��-i�ĵ�λ���룬��֧�ֺ���Ϊ��λ�������������ÿ��10����ִ��һ�Σ�������-i 0.01�����磺

```cli
redis-cli -r 5 -i 0.01 ping
```

����-r��-iѡ�ÿ��1������ڴ��ʹ������һ�����100�Σ�

```cli
redis-cli -r 100 -i 1 info | grep used_memory_human
```

3.  -x

-xѡ�����ӱ�׼���루stdin����ȡ������Ϊredis-cli�����һ����������������Ĳ����Ὣ�ַ���world��Ϊset hello��ֵ��

```cli
echo "world" | redis-cli -x set hello
```

4.  -c

-c��cluster��ѡ��������Redis Cluster�ڵ�ʱ��Ҫʹ�õģ�-cѡ����Է�ֹmoved��ask�쳣.

5.  -a

���Redis���������룬������-a��auth��ѡ��������ѡ��Ͳ���Ҫ�ֶ�����auth���

6.  --scan �� --pattern

--scanѡ���--patternѡ������ɨ��ָ��ģʽ�ļ����൱��ʹ��scan���

7.  --slave

--slaveѡ���ǰѵ�ǰ�ͻ���ģ��ɵ�ǰRedis�ڵ�Ĵӽڵ㣬����������ȡ��ǰRedis�ڵ�ĸ��²�����

```cli
redis-cli --slave
```
![slave����](../Image/slave����.png)

8. --rdb

--rdbѡ�������Redisʵ�����ɲ�����RDB�־û��ļ��������ڱ��ء���ʹ�������־û��ļ��Ķ��ڱ��ݡ�

9. --pipe

--pipeѡ�����ڽ������װ��Redisͨ��Э�鶨������ݸ�ʽ���������͸�Redisִ�С�

10. --bigkeys

--bigkeysѡ��ʹ��scan�����Redis�ļ����в����������ҵ��ڴ�ռ�ñȽϴ�ļ�ֵ����Щ��������ϵͳ��ƿ����

11. --eval

--evalѡ������ִ��ָ��Lua�ű�

12. --latency

latency������ѡ��ֱ���--latency--latency-history��--latency-dist�����Ƕ����Լ�������ӳ٣�����Redis�Ŀ�������ά�ǳ��а�����

(1) --latency
��ѡ����Բ��Կͻ��˵�Ŀ��Redis�������ӳ١�

```cli
redis-cli -h {machineB} --latency

```

```cli
redis-cli -h {machineB} --latency
```

���Կ����ͻ���A���ھ���Redis�Ƚ�Զ��ƽ�������ӳٻ���΢��һЩ��

(2) --latency-history
--latency��ִ�н��ֻ��һ����������Է�ʱ�ε���ʽ�˽��ӳ���Ϣ������ʹ��--latency-historyѡ�

```cli
redis-cli -h 10.10.xx.xx --latency-history
```
���Կ�����ʱ��Ϣÿ15�����һ�Σ�����ͨ��-i�������Ƽ��ʱ�䡣

(3)--latency-dist

��ѡ���ʹ��ͳ��ͼ�����ʽ�ӿ���̨����ӳ�ͳ����Ϣ��

13. --stat

--statѡ�����ʵʱ��ȡRedis����Ҫͳ����Ϣ����Ȼinfo�����е�ͳ����Ϣ��ȫ��������ʵʱ����һЩ���������ݣ�����requests������Redis����ά������һ�������ġ�

```cli
redis-cli --stat
```

14. --raw��--no-raw

--no-rawѡ����Ҫ������ķ��ؽ��������ԭʼ�ĸ�ʽ��--rawǡǡ�෴�����ظ�ʽ����Ľ����

```cli
redis-cli set hello "���"
```

```cli
redis-cli --raw get hello
```

3.2.2 redis-server���

redis-server��������Redis�⣬����һ��--test-memoryѡ�redis-server--test-memory����������⵱ǰ����ϵͳ�ܷ��ȶ��ط���ָ���������ڴ��Redis��ͨ�����ּ�������Ч������Ϊ�ڴ��������Redis������

������⵱ǰϵͳ�ܹ��ṩ1G���ڴ��Redis��

```cli
redis-server --test-memory 1024
```

�����ڴ����ʱ��Ƚϳ��������passed this testʱ˵���ڴ�����ϣ�������ʾ--test-memoryֻ�Ǽ򵥼�⣬��������ɿ���ʹ�ø���רҵ���ڴ��⹤�ߣ�

3.2.3 redis-benchmark���

redis-benchmark����ΪRedis����׼���ܲ��ԡ�

1.-c
-c(clients)ѡ�����ͻ��˵Ĳ���������Ĭ����50����
2.-n(requests)
-n(num)ѡ�����ͻ�������������Ĭ����100000����
3.-q
-qѡ�������ʾredis-benchmark��requests per second��Ϣ��
4.-r
��һ���յ�Redis��ִ����redis-benchmark�ᷢ��ֻ��3������
�������Redis�������ļ�������ִ��ʹ��-r��random��ѡ�������Redis�����������ļ���

```cli
redis-benchmark -c 100 -n 20000 -r 10000
```

5. -p

-Pѡ�����ÿ������pipeline����������Ĭ��Ϊ1����

6. -k<boolean>

-kѡ�����ͻ����Ƿ�ʹ��keepalive��1Ϊʹ�ã�0Ϊ��ʹ�ã�Ĭ��ֵΪ1��

7. -t
-tѡ����Զ�ָ��������л�׼���ԡ�

8. --csv
--csv ѡ��Ὣ�������csv��������������������

```cli
redis-benchmark -t get,set --csv
```
