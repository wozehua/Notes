
3.3 Pipeline

3.3.1 Pipeline����
Redis�ͻ���ִ��һ�������Ϊ�����ĸ����̣�
1����������
2�������Ŷ�
3������ִ��
4�����ؽ��
���� 1��+4����Ϊ Round Trip Time (RTT,����ʱ��)��

Redis �ṩ���������������mget,mset�ȣ�,��Ч�ؽ�ԼRTT��


Pipeline����ˮ�ߣ����ơ����ܽ�һ��Redis���������װ��ͨ��һ��RTT�����Redis,�ٽ�����Redis�����ִ�н����˳�򷵻ظ��ͻ��ˡ�
ͼ3-5 ���û��ʹ��Pipelineִ����n���������������Ҫn��RTT��

![û��Pipelineִ��n������ģ��](../Image/û��Pipelineִ��n������ģ��.png)

ͼ3-6 ʹ��Pipelineִ��n���������������Ҫ1��RTT

![ʹ��Pipeline](../Image/ʹ��Pipeline.png)

redis-cli��--pipeѡ��ʵ���Ͼ���ʹ��Pipeline���ƣ��������������set
hello world��incr counter����������װ��

```cli
echo -en '*3\r\n$3\r\nSET\r\n$5\r\nhello\r\n$5\r\nworld\r\n*2\r\n$4\r\nincr\r\
n$7\r\ncounter\r\n' | redis-cli --pipe

```

�󲿷�Redis �ͻ��˶�֧��Pipeline��

- Pipeline ִ���ٶ�һ�������ִ��Ҫ�졣
- �ͻ��˺ͷ���˵�������ʱԽ��Pipeline��Ч��Խ���ԡ�

![Pipeline�ͷ�Pipelineִ��ʱ��Ա�](../Image/��Pipeline��Pipeline��ִ��ʱ��Ա�.png)

3.3.3 ԭ������������Pipeline�Ա�

- ԭ������������ԭ�ӵģ�Pipeline �Ƿ�ԭ�ӵ�
- ԭ������������һ�������Ӧ���key,Pipeline֧�ֶ�����
- ԭ������������Redis�����֧��ʵ�ֵģ���Pipeline��Ҫ����˺Ϳͻ��˵Ĺ�ͬʵ�֡�

>ԭ�Ӳ�������: �����жϵ�һ������һϵ�в���, Ҳ���ǲ��ᱻ�̵߳��Ȼ��ƴ�ϵĲ���, �����ڼ䲻�����κε��������л�(context switch).

3.3.4 ���ʵ��

Pipeline��Ȼ���ã�����ÿ��Pipeline��װ�������������û�н��ƣ�����һ����װPipeline����������һ��������ӿͻ��˵ĵȴ�ʱ�䣬��һ��������һ�����������������Խ�һ�ΰ������������Pipeline��ֳɶ�ν�С��Pipeline����ɡ�

Pipelineֻ�ܲ���һ��Redisʵ�������Ǽ�ʹ�ڷֲ�ʽRedis�����У�Ҳ������Ϊ������������Ҫ�Ż��ֶΡ�