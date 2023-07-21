# 20230714 High-Performance Analog Circuit Design Lecture 01 Summary

### 吴志远，仅供个人复习整理使用

春季课程《高性能模拟集成电路设计》复习笔记整理

### Lecture1内容目录：

1. 课程总览
2. 长沟道器件
    1. 2.1. MOS导通过程
    2. 2.2. 长沟道器件电流方程
    3. 2.3. CMOS小信号模型
3. 小信号分析
    1. 3.1 小信号模型建立过程
    2. 3.2 一阶小信号模型
    3. 3.3 关键测试指标
4. 功耗-速度trade off
    1. 4.1 晶体管指标
5. 附：通过Cadence Virtuoso查看晶体管特性

# Lecture 1

<aside>
💡 Learning By Doing!

</aside>

## *对应PPT：课程简介/CMOS工艺和长沟道模型/CMOS小信号模型*

# 1. 课程总览

电路设计：指标→架构→每个架构下电路的设计（包含电路分析的特性）

<aside>
💡 能不用复杂的电路就不要用复杂的电路设计

</aside>

一套指标不同的人做出来可能有不同的结果。

在实际设计一套运放之前，可能对Razavi的书理解并不能那么深刻。

## Tools

![Untitled](IMAGE/Untitled.png)

Cadence：电路仿真

（留个坑以后来补，MATLAB的具体使用？）

## Topics

![Untitled](IMAGE/Untitled%201.png)

Gm-id：应对短沟道设计

### 模拟信号链

课程核心focus在放大器上

![Untitled](IMAGE/Untitled%202.png)

信号源（低频：sensor/高频：Antenna）提供一个小信号→放大器放大这个小信号→信号处理（滤波等）→ADC

### 分立器件与集成电路

过去IC发展趋势：分立器件→集成电路：为什么要用集成电路？

![Untitled](IMAGE/Untitled%203.png)

使用分立的器件**同样可以搭出优秀的电路**，但需要将每个晶体管的作用发挥到极限（受到晶体管数量的限制）

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

# 2. 长沟道器件

## 2.1 MOS导通过程

NMOS：

栅未加电压情况下没有导通，形成两个背靠背的二极管

![Untitled](IMAGE/Untitled%205.png)

开始施加栅压，沟道中形成反型层，但此时源漏未施加偏压，电流为0

![Untitled](IMAGE/Untitled%206.png)

源漏偏压加入，沟道内开始流过电流

![Untitled](IMAGE/Untitled%207.png)

## 2.2 长沟道器件电流方程

**线性区公式：**

$$
I_{D} = \mu C_{OX}\frac{W}{L}[(V_{GS}-V_{t}-\frac{V_{DS}}{2})] \cdot V_{DS}
$$

一阶I-V特性曲线，当$V_{DS}>V_{GS}-V_{t}$时沟道应该开始Pinch off，上公式未考虑

![Untitled](IMAGE/Untitled%208.png)

<aside>
💡 当沟道开始形成Pinch Off情况下，在一阶角度看电流已经与$V_{DS}$基本无关

</aside>

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

## 2.3 **CMOS小信号模型

如何放大一个电压信号？

- 直接放大一个电压：两个电压源串接（天然电压放大二倍）
    - 信号→两个电容→叠加两个电容得到2倍电压
    - 信号→电容（固定了$C\cdot V_{in}$的电荷）→改变电容值，在Q一定情况下V会变大
        - 最简单的可变电容→MOS管的栅电容
- Razavi：**电压→电流→通过一个R变成一个放大的电压**

![Untitled](IMAGE/Untitled%2011.png)

**电压→电流→电压**

$g_m\cdot R > 1$→电压放大，可以在中间倍增电流，即

电压→电流→放大电流→电压

Common source单管电路：

![Untitled](IMAGE/Untitled%2012.png)

关断区→饱和区→线性区

<aside>
💡 只在一个特定的偏置范围起作用

</aside>

如何产生偏置？→后续（待填坑）

![Untitled](IMAGE/Untitled%2013.png)

# 3. 小信号分析

在Vov（偏置）的基础上，添加一个**小信号**的**微扰**

输出的$\Delta V_O$与输入小信号$\Delta V_{i}$之间的关系：

$$
V_{O}+\Delta V_{O} = V_{DD}-\frac{1}{2}\mu C_{OX}\frac{W}{L}(V_{OV}+\Delta V_{i})^2 \cdot R
$$

$$
\Delta V_{O} = -\frac{1}{2}\mu\ C_{OX}\frac{W}{L}R\cdot [(V_{OV}+\Delta V_{i})^2-V_{OV}^2]
$$

化简得到

$$
\Delta V_{O}=-\frac{2I_{D}}{V_{OV}}\cdot R\cdot \Delta V_{i}[1+\frac{\Delta V_{i}}{2V_{OV}}]
$$

小信号有$\Delta V_{i}<<2V_{OV}$

$$
\Delta V_{O}=-\frac{2I_D}{V_{OV}}\cdot R \cdot \Delta V_i
$$

<aside>
💡 本质上说，实际上$\frac{\Delta V_i}{2V_{OV}}$实际上是一直存在的，当不满足近似条件时，一定会产生**非线性**

</aside>

开环放大器→输入输出曲线落在一个非线性的曲线上

小信号：对一个曲线做切线，切线斜率即为小信号增益

![Untitled](IMAGE/Untitled%2014.png)

## 3.1 小信号模型建立过程

### 首先把$g_m$弄出来

利用一个VCCS给$g_m$建模（小信号模型的第一个元件），线性区同理

![Untitled](IMAGE/Untitled%2015.png)

$g_m$即为$I_D$对$V_{GS}$的偏导

$$
I_{D}=\frac{1}{2}\mu C_{OX}\frac{W}{L} (V_{GS}-V_t)^2
$$

$$
g_{m} = \frac{i_d}{v_{gs}}=\frac{\partial I_D}{\partial V_{GS}} = \frac{1}{2} \mu C_{OX}\frac{W}{L}(V_{GS}-V_{t})=\frac{2I_D}{V_{OV}}
$$

### 然后加入非理想特性

![Untitled](IMAGE/Untitled%2016.png)

$$
I_D = \frac{1}{2} \mu C_{OX}\frac{W}{L} (V_GS-V_t)^2(1+\lambda V_{DS})
$$

理想：前段是一个抛物线，饱和后是一个和$V_{DS}$无关的平线

实际：饱和后与$V_{DS}$仍然是相关的→小信号的有限输出阻抗

### 小信号输出阻抗建模

![Untitled](IMAGE/Untitled%2017.png)

以小信号模型为前提条件，将其有限的**输出阻抗**建模为一个随工作点变化的输出电阻

$$
g_{ds}=\frac{dI_D}{d V_{DS}}=\frac{d}{dV_{DS}}[\frac{1}{2}\mu C_{OX} \frac{W}{L}(V_{GS}-V_t)^2(1+\lambda V_{DS})]
$$

$$
g_{ds} = \frac{\lambda I_D}{1+\lambda V_{DS}} \approx \lambda I_D
$$

### 输入电容

有了$g_m$和输出阻抗之后，下一步考虑把输入电容添加进来$C_{GS}$

![Untitled](IMAGE/Untitled%2018.png)

<aside>
💡 不同的工作区，输入电容不同

</aside>

**线性区**

沟道里的电荷是一直形成的，S与D是一直联通的，也就是栅和channel形成了一个电容。

此时G和S和G和D形成的电容是相同的，衬底电容是可以**忽略**的。

![Untitled](IMAGE/Untitled%2019.png)

$$
C_{GC} = WL \frac{\epsilon_{OX}}{t_{OX}} = WLC_{ox}
$$

$$
C_{GS} = C_{GD} = \frac{1}{2}C_{GC}
$$

**饱和区**

沟道形成了pinch-off，大部分电荷在S端，D端电容约为0

$$
C_{GS} = \frac{2}{3} WLC_{ox}, C_{GD} \approx0
$$

**截止区**

没有电荷，栅与耗尽的沟道形成的电容与衬底电容串联，形成一个整体上更小的电容

![Untitled](IMAGE/Untitled%2020.png)

施加一个大的负栅压则电容重新近似等于$C_{GC}$

<aside>
💡 总结电容分布如下

</aside>

![Untitled](IMAGE/Untitled%2021.png)

## 3.2 一阶小信号模型

一般希望工作在饱和区，由以上分析得到了小信号模型如下

![Untitled](IMAGE/Untitled%2022.png)

用建立的小信号模型分析电路，可以得到一个如下图的常见setup

输入信号，源阻抗，输出负载等（偏置只是用来产生晶体管的gm到底有多大）

![Untitled](IMAGE/Untitled%2023.png)

写出输入到输出的传递函数：

$$
H(S) = \frac{V_O(s)}{V_i(s)} = -g_mR\cdot\frac{1}{1+sR_iC_{GS}}
$$

## 3.3 关键测试指标

- DC增益
    - 低频下的增益：$A_{DC} = -g_mR$
- 带宽
    - 小的栅电容带来最大的带宽：$f_{-3dB} = \frac{1}{2\pi}\frac{R_i}{C_{GS}}$
- 功耗
    - 小的漏端电流带来最小化的功耗：$P = V_{DD}\cdot I_D$

# 4. 功耗-速度trade off

What we really want from our MOS transistor

- Some $g_m$without investing much current $I_D$.
- Some $g_m$without introducing large $C_{GS}$.

<aside>
💡 在放大器中希望有大的gm，小的Cgs以及小的电流

</aside>

使用以下两个指标来衡量功耗与速度：

$$
\frac{g_m}{I_D}, \frac{g_m}{C_{GS}}
$$

从长沟道器件模型出发

$$
\frac{g_m}{I_d} = \frac{2}{V_{OV}}
$$

$$
\frac{g_m}{C_{GS}}=\frac{3}{2}\frac{\mu V_{OV}}{L^2}
$$

<aside>
💡 $V_{OV}$ is the "knob" that trades power efficiency gm/ID for speed gm/Cgs

</aside>

与速度相关：更大的Vov

与能耗相关：更小的Vov

把两个数乘一下，看看能不能得到一个sweet point

利用长沟道模型得到速度与能效乘积

$$
\frac{g_m}{I_D}\cdot \frac{g_m}{C_{GS}} = \frac{3\mu}{L^2}
$$

<aside>
💡 想获得更大的乘积只能继续减小L，即沟道长度

</aside>

**减小沟道长度→摩尔定律**

可以通过摩尔定律来观察沟道缩减的规律，我们需要探索如何更好的针对工艺特性做优化：

![Untitled](IMAGE/Untitled%2024.png)

可以做的两类事情：

- 在功耗不变的基础上提升速度
- 在速度被某些标准限制的前提下降低功耗

## 4.1 晶体管指标

### Transit Frequency: $\omega _t$

电流开始不再放大的效果，即晶体管失去放大作用的频率

The transit frequency of a transistor is defined as the frequency where the magnitude of
the common source current gain is equal to 1.

![Untitled](IMAGE/Untitled%2025.png)

$$
\omega_T = \frac {g_m} {C_{GS}} = \frac{3}{2}\frac{\mu V_{OV}}{L^2}
$$

### Intrinsic Gain

在负载$R_L$无穷大的情况下能提供的增益，即自己的$r_o$决定的

With $R_L$→ $\infin$, the basic common source stage achieves its maximum possible voltage gain or "intrinsic gain".

$$
|A_{DC}| = g_m R = g_m(R_L||R_o)
$$

$$
|A_{DC, max}| = g_mr_o=\frac{g_m}{g_{ds}}\approx\frac{1}{\lambda} \frac{g_m}{I_d}=\frac{2}{\lambda V_{OV}}
$$

<aside>
💡 尺寸都确定了如何得到更高增益？降低过驱动电压到亚阈值区

</aside>

![Untitled](IMAGE/Untitled%2026.png)

# 附：通过Cadence Virtuoso查看晶体管特性

Step1. 建立一个DC仿真的电路图，可以如下图所示，画完之后点击save and check，不报warning和error为准

![Untitled](IMAGE/Untitled%2027.png)

注意管子选择nmosmvt2v，模型更完整一些

![Untitled](IMAGE/Untitled%2028.png)

Step2. Launch→ ADE L，打开ADE L界面，在Variables选择Copy from cellview将变量读入，并赋初始值。

![Untitled](IMAGE/Untitled%2029.png)

在Analysis处右键，点击Edit添加一个DC仿真

![Untitled](IMAGE/Untitled%2030.png)

![Untitled](IMAGE/Untitled%2031.png)

<aside>
💡 注意一定要勾选Save DC Operating Point

</aside>

Step3. 运行一次仿真，如果仿真没有跑起来可以检查下工艺库路径是否正确等

![Untitled](IMAGE/Untitled%2032.png)

Step4. 成功运行一次之后选择Tools→Calculator

![Untitled](IMAGE/Untitled%2033.png)

![Untitled](IMAGE/Untitled%2034.png)

点击OS，之后选择器件，会出现一个小的对话框，点击下拉菜单即可选择需要查看的内容

![Untitled](IMAGE/Untitled%2035.png)

![Untitled](IMAGE/Untitled%2036.png)

Step5. 点击需要查看的内容，会出现在计算器中，可以在计算器内进行一些运算得到最终需要的表达式，也可以直接按齿轮键送回Output中