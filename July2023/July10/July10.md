# 20230710 High-Performance Analog Circuit Design Lecture 01 -1

### 吴志远，仅供个人复习整理使用

春季课程《高性能模拟集成电路设计》复习笔记整理

# Lecture 1-1

## *对应PPT：课程简介*

电路设计：指标→架构→每个架构下电路的设计（包含电路分析的特性）

<aside>
💡 能不用复杂的电路就不要用复杂的电路设计

</aside>

一套指标不同的人做出来可能有不同的结果。

<aside>
💡 Learning By Doing!

</aside>

在实际设计一套运放之前，可能对Razavi的书理解并不能那么深刻。

## Tools

![Untitled](IMAGE/Untitled.png)

Cadence：电路仿真

（留个坑以后来补，MATLAB的具体使用？）

## Topics

![Untitled](IMAGE/Untitled%201.png)

Gm-id：应对短沟道设计

## *对应PPT： CMOS工艺和长沟道模型*

### 模拟信号链

课程核心focus在放大器上

![Untitled](IMAGE/Untitled%202.png)

信号源（低频：sensor/高频：Antenna）提供一个小信号→放大器放大这个小信号→信号处理（滤波等）→ADC

### IC-分立器件

趋势：分立器件→集成电路：为什么要用集成电路？

![Untitled](IMAGE/Untitled%203.png)

使用分立的器件同样可以搭出优秀的电路，但需要将每个晶体管的作用发挥到极限（受到晶体管数量的限制）

- 分立器件尺寸不受限制，可以做到很广泛的容值阻值等
- 集成电路中器件的绝对精度是不够的，但相对精度很高（0.1%量级）
- 集成电路中的transistor几乎是免费的（单个造价很低），随着数字电路成本进一步降低，将数字电路集成进来辅助模拟部分进行校准等任务

集成电路的材料：用什么样的器件来集成？

![Untitled](IMAGE/Untitled%204.png)

从性能角度看，BJT整体上是好于MOS的→搭了数字IC工艺发展的便车

<aside>
💡 相同结构下，给定电流能产生多大的跨导

</aside>

BiCMOS(BCD)工艺：目前推进至40nm，数模混合性能较为平衡

## 器件

NMOS：

栅未加电压情况下没有导通，形成两个背靠背的二极管

![Untitled](IMAGE/Untitled%205.png)

开始施加栅压，沟道中形成反型层，但此时源漏未施加偏压，电流为0

![Untitled](IMAGE/Untitled%206.png)

源漏偏压加入，沟道内开始流过电流

![Untitled](IMAGE/Untitled%207.png)

线性区公式：

$$
I_{D} = \mu C_{OX}\frac{W}{L}[(V_{GS}-V_{t}-\frac{V_{DS}}{2})] \cdot V_{DS}
$$

一阶I-V特性曲线，当$V_{DS}>V_{GS}-V_{t}$时沟道应该开始Pinch off，上公式未考虑

![Untitled](IMAGE/Untitled%208.png)

<aside>
💡 当沟道开始形成Pinch Off情况下，在一阶角度看电流已经与$V_{DS}$基本无关

</aside>

### 长沟道器件电流方程

![Untitled](IMAGE/Untitled%209.png)

$$
Triode Region: I_{D}=\mu C_{OX}\frac{W}{L}[(V_{GS}-V_{t})-\frac{V_{DS}}{2}]\cdot V_{DS}
$$

$$
Active Region:I_{D}=\mu C_{OX}\frac{W}{L}[(V_{GS}-V_{t})-\frac{(V_{GS}-V_{t})}{2})]\cdot (V_{GS}-V_t)=\frac{1}{2}\mu C_{OX}\frac{W}{L}(V_{GS}-V_t)^2
$$

**线性区：电阻**

**饱和区：压控电流源（VCCS）**

**亚阈值区：$V_{GS}<V_t$**

![Untitled](IMAGE/Untitled%2010.png)

### 模型准确性：

二阶效应导致模型并不准确

长沟道模型可以提供很多电路设计上的“***直觉***”

<aside>
💡 最好的模型是能解决问题的最简单的模型

</aside>

## *对应PPT： CMOS小信号模型*

如何放大一个电压信号？

![Untitled](IMAGE/Untitled%2011.png)

- Razavi：电压→电流→通过一个R变成一个放大的电压
- 直接放大一个电压：两个电压源串接（天然电压放大二倍）
    - 信号→两个电容→叠加两个电容得到2倍电压
    - 信号→电容（固定了$C\cdot V_{in}$的电荷）→改变电容值，在Q一定情况下V会变大
        - 最简单的可变电容→MOS管的栅电容