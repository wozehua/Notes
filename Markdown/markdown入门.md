# markdown 入门

## VS Code插件

1. Markdow Preview Enhanced


## markdow 语法

# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

#号和文本之间加入空格才能有标题效果。
每写完一个段落要隔一行空行

**重点加粗**

*斜体*

***加粗斜体***

~~删除线~~

---

列表:
* 无序列表
  * 嵌套列表
  * 嵌套列表
* 无序列表
* 无序列表
1. 有序列表
    1. 嵌套有序列表
    2. 嵌套有序列表
2. 有序列表
3. 有序列表

---
引用文本：
> 引用别人说的话
> 就这样

---
代码块

~~~go
package main

func main(){

}
~~~

~~~c#
namespace test.TestDemo

Class Test
{
    static void Main(object args)
    {
        Console.WriteLine("Hello, Worlds!")
    }
}
~~~

---

[超链接](https://www.baidu.com)

![图片地址](https://i1.hdslb.com/bfs/face/44fcc769a771ca39ee783d209e48356c8688ecbf.jpg@160w_160h_1c_1s.webp)

---

 表格

| 表头 | 表头 |
| ---- | ---- |
| 内容 | 内容 |
| 内容 | 内容 |
| >    | 内容 |
| | 内容|


| 表头 | 表头 |
| ---- | ---- |
| 内容 | 内容 |
| >    | 内容 |

行内公示
$x^2+y^2=1 $

公示块
$$
\begin{cases}
    x=\rho\cos\theta\\
    y=\rho\sin\theta
\end{cases}
$$

上标
$ x^2 +y^2=1$

下标
$ x_1 +y_1=1 $ 

分式

较小的行内分数 $\frac{1}{2}$

展示型的分式 $\displaystyle\frac{x+1}{x-1} $

根式

开平方 $\sqrt{2}$

开$n$次方 $\sqrt[n]{2}$

累加
$\sum_{k=1}^n\frac{1}{k} \quad \displaystyle\sum_{k=1}^n\frac{1}{k}$

累乘
$\prod_{k=1}^n\frac{1}{k} \quad \displaystyle\sum_{k=1}^n\frac{1}{k}$

积分
$\displaystyle \int_0^1x{\rm d}x \quad \iint_{D_{xy}} \quad \iiint_{\Omega_{xyz}}$


----

注释
<!-- 你看不见我-->

分割线
三条恒线(或更多的横线)表示分割线

以下为 markdown Preview Enhanced扩展功能
==高亮==

任务列表

- [x] 已完成事项
- [x] 已完成事项
- [ ] 未完成事项




