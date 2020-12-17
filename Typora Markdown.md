#  Typora Markdown

### 1.#代表标题

### 2. ~~删除线~~

### 3. *斜体*

### 4. **加粗**

### 5.***斜体加粗***

### 6. <u>下划线</u>(command + u快捷键)

### 7.高亮(==需勾选扩展语法==)

### 8.下标(==需勾选扩展语法==)  H~2~O~2~

### 9.上标(==需勾选扩展语法==) m^2^

### 10. 表情符号

:smile::laughing::cry::100:

### 11.表格(command + option + t快捷捷)

| name | price | tag |
| :---- | :-----: | ----: |
| aaaa | 10    | h |

### 12. 引用

> 不知妻美刘强东
>
> >  

### 13. 无序列表

* 村
* 长

### 14.有序列表

1. 村
2. 长

### 15. 代码

####15.1 代码块

~~~markdown
```语言名称
~~~

#### 15.2 行内代码

` java` `c` `JavaScript`

#### 15.3 转换规则

### 16.分割线

***

-----

### 17.跳转

#### 17.1 外部超链接

[百度]( http://www.baidu.com)

#### 17.2 内部超链接(Only Typora support)

[我想跳转](#20.饼图(Pie))

#### 17.3 自动链接

<http://www.baidu.com>

### 18. 图片

#### 18.1 网上图片

![cat](https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1605574212823&di=070c8b2348a822705c7c11f191defdd7&imgtype=0&src=http%3A%2F%2Fa0.att.hudong.com%2F30%2F29%2F01300000201438121627296084016.jpg)



#### 18.2 本地图片

![本地](/Users/brodyliao/Documents/keyboard value1.jpeg)



### 19 Markdown画图(==需勾选扩展语法==)

| 用词 | 含义     |
| ---- | -------- |
| TB   | 从上到下 |
| BT   | 从下到上 |
| RL   | 从右到左 |
| LR   | 从左到右 |

> T = Top, B = Bottom,  L = Left,  R = Right

```mermaid
graph TB;
 	A-->B
	B-->C
  C-->A
```

```mermaid
graph LR;
 	A-->B
	B-->C
  C-->A
```

#### 19.1 流程图常用的符号及含义

| 表述       | 说明         | 含义                                               |
| ---------- | ------------ | -------------------------------------------------- |
| id[文字]   | 矩形节点     | 表示过程, 也就是整个流程中的一个环节               |
| id(文字)   | 圆角矩形节点 | 表示开始和结束                                     |
| id((文字)) | 圆形节点     | 表示连接,为避免流程过程过长或交叉,可将流程切开成对 |
| id{文字}   | 菱形节点     | 表示判断和决策                                     |
| id> 文字]  | 右向旗帜节点 |                                                    |

~~~ mermaid
graph TB;
 	A
 	B(圆角节点)
 	C[矩形节点]
 	D((圆形节点))
 	E{菱形节点}
 	F>右向旗帜节点]
~~~

``` mermaid
graph TB;
	begin(出门) --> buy(买炸鸡)
	buy --> IsRemaining(还有没有炸鸡)
	IsRemaining --> |有|happy(买完炸鸡开心) --> goBack(回家)
	IsRemaining --没有--> sad[伤心] --> goBack(回家)
	
```

#### 19.2 连线

```mermaid
graph TB;
	A1-->B1
	A2---B2
	A3--text---B3
	A4--text-->B4
	A5-.-B5
	A6-.->B6
	A7-.text.-B7
	A8-.text.->B8
	A9===B9
	A10==>B10
	A11==text===B11
	A12==text==>B12
	
	
	
	
	
```

#### 19.3 子表图



``` mermaid
graph TB;
	subgraph 买炸鸡前
		begin(出门) --> buy(买炸鸡)
	end
	buy --> IsRemaining(还有没有炸鸡)
	IsRemaining --> |有|happy(买完炸鸡开心) --> goBack(回家)
	IsRemaining --没有--> sad[伤心] --> goBack(回家)
```

#### 19.4 序列图

~~~ mermaid
sequenceDiagram
	Title:买炸鸡
	Brody->>炸鸡店小姐姐:还有炸鸡吗?
	炸鸡店小姐姐-->> Brody:没有,要现炸
~~~





#### 19.4 参与者

~~~ mermaid
sequenceDiagram
	participant Liao
	participant lcj
	participant bbliao
	
~~~

#### 19.5 消息线



| 类型 | 描述                       |
| ---- | -------------------------- |
| ->   | 无箭头的实线               |
| -->  | 无箭头的虚线               |
| ->>  | 有箭头的实线(主动发现消息) |
| -->> | 有箭头的虚线(响应)         |
| -x   | 末端为叉的实线(表示异步)   |
| --x  | 末端为叉的虚线(表示异步)   |

#### 19.6 处理中激活框

~~~ mermaid
sequenceDiagram
	participant B as Brody
	participant seller as 炸鸡店小姐姐
	B ->> seller: 还有炸鸡吗?
	seller -->> B:没有,要现炸
	B -x +seller: 给我炸
	seller -->> -B:炸好了
~~~

#### 19.7 注解

| 表述     | 含义                      |
| -------- | ------------------------- |
| right of | 右则                      |
| left of  | 左则                      |
| over     | 在当中,可以横跨多个参与者 |



``` mermaid
sequenceDiagram
	participant B as Brody
	participant seller as 炸鸡店小姐姐
	Note over B,seller : 热爱炸鸡
	Note left of B : 男
	Note right of seller : 女
	B ->> seller: 还有炸鸡吗?
	seller -->> B:没有,要现炸
	B -x +seller: 给我炸
	seller -->> -B:炸好了
	
```

#### 19.8 循环

``` mermaid
sequenceDiagram
	participant B as Brody
	participant seller as 炸鸡店小姐姐
	B ->> seller: 还有炸鸡吗?
	seller -->> B:没有,要现炸
	B -x +seller: 给我炸
	loop 三分钟一次
		B ->> seller: 我的炸鸡好了吗?
		seller -->> B: 正在炸
	end
	seller -->> -B:炸好了
```

### 19.9 选择( alt)

```mermaid
sequenceDiagram
	participant B as Brody
	participant seller as 炸鸡店小姐姐
	B ->> seller: 现在有多少只炸鸡?
	seller -->> B:可卖的炸鸡数
	alt 可卖的炸鸡数 > 3
		B ->> seller : 买三只
	else 1 < 可卖的炸鸡数 < 3
	 B ->> seller : 有多少买多少
	else 可卖的炸鸡数 < 1
		B ->> seller : 那我明天再来
	end
	seller -->> B : 欢迎下次光临
```

#### 19.10 选项( opt)

```mermaid
sequenceDiagram
	participant B as Brody
	participant seller as 炸鸡店小姐姐
	B ->> seller: 买炸鸡
	opt 全部卖完了
		seller -->> B : 下次再来
	end
```



#### 19.11 并行( par)

```mermaid
sequenceDiagram
	participant B as Brody
	participant seller as 炸鸡店小姐姐
	B ->> seller: 一只炸鸡,一杯可乐
	par 并行执行
		seller -->> seller : 炸鸡
	and 
		seller -->> seller : 装可乐
	end
	seller -->> B : 您的东西好了
```

### 20.饼图(Pie)

~~~ mermaid
pie
	title Pie Chart
	"Dogs": 386
	"Cats": 85
	"Rates": 150
~~~

### 21.甘特图(gantt)

```mermaid
%% Example with selection of syntaxes
        gantt
        dateFormat  YYYY-MM-DD
        title Adding GANTT diagram functionality to mermaid

        section A section
        Completed task            :done,    des1, 2014-01-06,2014-01-08
        Active task               :active,  des2, 2014-01-09, 3d
        Future task               :         des3, after des2, 5d
        Future task2               :         des4, after des3, 5d

        section Critical tasks
        Completed task in the critical line :crit, done, 2014-01-06,24h
        Implement parser and jison          :crit, done, after des1, 2d
        Create tests for parser             :crit, active, 3d
        Future task in critical line        :crit, 5d
        Create tests for renderer           :2d
        Add to mermaid                      :1d

        section Documentation
        Describe gantt syntax               :active, a1, after des1, 3d
        Add gantt diagram to demo page      :after a1  , 20h
        Add another diagram to demo page    :doc1, after a1  , 48h

        section Last section
        Describe gantt syntax               :after doc1, 3d
        Add gantt diagram to demo page      : 20h
        Add another diagram to demo page    : 48h
```

###  

### 22.类图( class)

```mermaid
classDiagram
      Animal <|-- Duck
      Animal <|-- Fish
      Animal <|-- Zebra
      Animal : +int age
      Animal : +String gender
      Animal: +isMammal()
      Animal: +mate()
      class Duck{
          +String beakColor
          +swim()
          +quack()
      }
      class Fish{
          -int sizeInFeet
          -canEat()
      }
      class Zebra{
          +bool is_wild
          +run()
      }
```

### 23.状态(state)

```mermaid
stateDiagram
    [*] --> Still
    Still --> [*]

    Still --> Moving
    Moving --> Still
    Moving --> Crash
    Crash --> [*]
```

### 24.流程图(flow)

```mermaid
graph LR
A[Hard edge] -->B(Round edge)
    B --> C{Decision}
    C -->|One| D[Result one]
    C -->|Two| E[Result two]
```

```flow
st=>start: Start
op=>operation: Your Operation
cond=>condition: Yes or No?
e=>end

st->op->cond
cond(yes)->e
cond(no)->op
```

### 25.数学与学术功能

#### 25.1 数学块

$$
\begin{align*}
y = y(x,t) &= A e^{i\theta} \\
&= A (\cos \theta + i \sin \theta) \\
&= A (\cos(kx - \omega t) + i \sin(kx - \omega t)) \\
&= A\cos(kx - \omega t) + i A\sin(kx - \omega t)  \\
&= A\cos \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big) + i A\sin \Big(\frac{2\pi}{\lambda}x - \frac{2\pi v}{\lambda} t \Big)  \\
&= A\cos \frac{2\pi}{\lambda} (x - v t) + i A\sin \frac{2\pi}{\lambda} (x - v t)
\end{align*}
$$

#### 25.2 行内数学

$\lim_{x \to \infty } \exp(-x) = 0$



#### 25.3 化学公式

$\ce{CH4 + 2 $\left( \ce{O2 + 79/21 N2} \right)$}$

#### 25.4 数学



Here is a labeled equation:

$$
x+1\over\sqrt{1-x^2}\label{ref1}\tag{1}
$$

This is a reference : $\ref{ref1}$



