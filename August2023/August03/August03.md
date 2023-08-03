# 20230803 High-Performance Analog Circuit Design Lecture 06 -1 Diff. Pair

<aside>
💡 The differential pair is the most widely used two-transistor sub-circuit in analog ICs

</aside>

# 1. 差模信号&共模信号

![Untitled](IMAGE/Untitled.png)

![Untitled](IMAGE/Untitled%201.png)

施加一个电压，看两侧电流的差异。差分两侧电压的变化对差分对没有影响，只有变化的信号才会有影响

$$
V_{id}=(V_{ip}-V_{im})
$$

共模电压：夹在信号的中间

$$
V_{ic}=\frac{V_{ip}+V_{im}}{2}
$$

差分对可以避免共模噪声对信号的干扰

![Untitled](IMAGE/Untitled%202.png)

# 2. 大信号传递函数

## 2.1 大信号分析

<aside>
💡 差分对：分电流，输出范围大概在$+-\sqrt{2}V_{ov}$

</aside>

![Untitled](IMAGE/Untitled%203.png)

$$
V_{ip}-V_{gs1}=V_{im}-V_{gs2}\\I_{d1}+I_{d2}=I_{tail}
$$

$$
V_{gs1}=V_t+\sqrt{\frac{2I_{d1}}{\mu C_{ox}\frac{W}{L}}},V_{gs2}=V_t+\sqrt{\frac{2I_{d2}}{\mu C_{ox}\frac{W}{L}}}\\\to I_{od}=I_{d1}-I_{d2}=\frac{1}{2}\mu C_{ox}\frac{W}{L}V_{id}\sqrt{\frac{4I_{tail}}{\mu C_{ox}\frac{W}{L}-V_{id}^2}}
$$

$$
Using: \frac{I_{tail}}{2}=\frac{1}{2}\mu C_{ox}\frac{W}{L}V_{ov}^2\\\frac{I_{od}}{I_{tail}}=\frac{I_{d1}-I_{d2}}{I_{tail}}=\frac{V_{id}}{V_{ov}\sqrt{1-(\frac{V_{id}}{2V_{ov}})^2}}
$$

闭环情况下放大器输入两端是比较接近的，大部分情况下是比较好的差分对的形式

![Untitled](IMAGE/Untitled%204.png)

## 2.2 非线性

差分之后会可以去掉偶次谐波（单端放大器主要的非线性在二阶谐波上）

$$
\frac{I_{od}}{I_{tail}}=(\frac{V_{id}}{V_{ov}})-\frac{1}{8}(\frac{V_{id}}{V_{ov}})^3-...
$$

闭环放大器为什么能提高线性度：尽可能减少了$V_{id}$，提升了差分对的线性度

<aside>
💡 $V_{id}$越小于$V_{ov}$，线性度越好

</aside>

差分对的等效跨导

$$
G_m=\frac{dI_{od}}{dV_{id}}|_{V_id=0}=\frac{I_{tail}}{V_{ov}}
$$

注意差分对两个管子各自的跨导也是

$$
g_{m1,2}=\frac{2I_D}{V_{ov}}=\frac{2\frac{I_{tail}}{2}}{V_{ov}}=\frac{I_{tail}}{V_{ov}}
$$

差分尾电流源是一个小信号地（也没有那么地，在一端输入信号过大的时候这个位置上也还是有信号分量的），使用小信号半电路分析的时候天生就失去了分析非线性的能力，需要分析非线性还是要用之前的电路。

![Untitled](IMAGE/Untitled%205.png)

# 3. 小信号

$$
差模增益：A_{dm}=\frac{V_{od}}{V_{id}}\\ 共模增益：A_{cm}=\frac{V_{oc}}{V_{ic}},差模-共模增益：A_{dm-cm}=\frac{V_{oc}}{V_{id}},\\共模-差模增益 A_{cm-dm}=\frac{V_{od}}{V_{ic}} 
$$

## 3.1 **共模增益：**

画出共模的小信号模型

![Untitled](IMAGE/Untitled%206.png)

当尾电流是理想源的时候：

$$
A_{cm}=0
$$

当尾电流有有限阻抗的时候

$$
A_{cm}=-\frac{g_m}{1+g_m\cdot 2R_{tail}}(R||r_o[1+g_m\cdot2R_{tail}])
$$

## 3.2 **共模抑制比（CMRR）：**与PPT不同

$$
A_{dm-cm}=\frac{V_{oc}}{V_{id}}
$$

输入短接在一起，看输出有多少不想要的东西

<aside>
💡 给共模和差模加一个chop，破坏共模和差模之间混合去机会

</aside>

## 3.3 **电源抑制比（PSRR）：**

PSRR+：电源上噪声的影响

PSRR-：地上噪声的影响

$$
A_+=\frac{V_{od}}{V_{dd}}, A_-=\frac{V_{od}}{V_{ss}}\\PSRR_+=|\frac{A_{dm}}{A_+}|,PSRR_-=|\frac{A_{dm}}{A_-}|
$$

![Untitled](IMAGE/Untitled%207.png)

伪差分：直接把两个单端放在一起，有差分的作用，但没有去除偶次谐波的作用

---

# Current mirror and offset

# 1. 电流镜

![Untitled](IMAGE/Untitled%208.png)

把基准的电流复制过来

- 准确
- 大的阻抗和小的电容
- 不要占太多电压空间

![Untitled](IMAGE/Untitled%209.png)

两个晶体管的L相同，靠W不同实现比例，但实际上比较困难，比如实际上的晶体管如图

![Untitled](IMAGE/Untitled%2010.png)

<aside>
💡 要把W和L都定成一样的，只修改Multipler

</aside>

![Untitled](IMAGE/Untitled%2011.png)

$$
\Delta I=I_1-I_2\approx\frac{V_1-V_2}{r_o}=\frac{\Delta V}{r}
$$

## 输出阻抗

实际上保证只改M的情况下，也只是保证了gm是准确的比例关系，但$r_o$并不是一样的，如右上图

- 尽可能的提高输出阻抗，保证输出的时候gm是占主导地位的→**L做大**
- 想办法让两个电压相近

随着Vds越大，输出阻抗越大；随着L越大，输出阻抗越大

![Untitled](IMAGE/Untitled%2012.png)

![Untitled](IMAGE/Untitled%2013.png)

为了腾出更多的电压空间，尽量在较小的Vds范围下使用，这时可以发现**输出阻抗随着L变化也不大**

### 进一步提高输出阻抗

加一个cascode管，提高输出阻抗，减少ro带来的影响

![Untitled](IMAGE/Untitled%2014.png)

![Untitled](IMAGE/Untitled%2015.png)

<aside>
💡 这种偏置占了较多的电压空间（两个Vov和一个Vth）

</aside>

### 低电压电流镜

电压空间为两个Vov

![Untitled](IMAGE/Untitled%2016.png)

如何保证一个Vbmagic？

![Untitled](IMAGE/Untitled%2017.png)

![Untitled](IMAGE/Untitled%2018.png)

![Untitled](IMAGE/Untitled%2019.png)

<aside>
💡 需要用同种类型的管子来做一个不同的偏置→Track Corner

</aside>

1. 先估计电压大小范围
2. 再用相同类型的晶体管造一个battery
3. 仿真验证

![Untitled](IMAGE/Untitled%2020.png)

<aside>
💡 电流镜比例差别不要太大：10~20

</aside>

## 电容耦合

在电流镜上挂一个MOS电容，来起到滤波的作用

![Untitled](IMAGE/Untitled%2021.png)

# 2. 失配

Layout中导致失配的因素：

- WPE：尽量不要放在边界

![Untitled](IMAGE/Untitled%2022.png)

- 应力

![Untitled](IMAGE/Untitled%2023.png)

- IR Drop

![Untitled](IMAGE/Untitled%2024.png)

<aside>
💡 版图上的位置尽量一模一样且比较接近

</aside>

## 2.2 随机失配

![Untitled](IMAGE/Untitled%2010.png)

由于制造导致的失配，比如上图，建模到

- 阈值电压的变化
- 工艺参数β的变化

$$
\sigma_{\Delta V_t}=\frac{A_{V_t}}{\sqrt{WL}}, \sigma_{\frac{\Delta \beta}{\beta}}=\frac{A_{\beta}}{\sqrt{WL}}
$$

$A_{Vt}和A_{\beta}$可以通过PDK的datasheet查到

- In 0.18µm technology: $A_{Vt}$ ≅ 5mV-µm,  $A_{\beta}$ ≅ 1%-µm
    - $A_{Vt}$ tends to scale down with technology, roughly proportional to
    gate oxide thickness
    - $A_{\beta}$ has remained roughly constant with scaling

阈值电压的失配一般占主导作用

以一个W=10μm，L=0.18μm的晶体管为例

$$
\sigma_{\Delta V_t}=\frac{5mV}{\sqrt{1.8}}=3.7mV, \sigma_{\frac{\Delta \beta}{\beta}}=\frac{1\%}{\sqrt{1.8}}=0.75\%
$$

![Untitled](IMAGE/Untitled%2025.png)

$$
\Delta I=I_1-I_2\approx -g_m\Delta V_t+I_1\frac{\Delta \beta}{\beta}\\\frac{\Delta I}{I_1}\approx -\frac{g_m}{I_1}\Delta V_t +\frac{\Delta \beta}{\beta}
$$

W=10μm，L=0.18μm，gm/Id=10S/A 

$$
\sigma_\frac{\Delta I}{I} = \sqrt{(10\frac{S}{A}\cdot 3.7mV)^2+(0.75\%)^2}=\sqrt{(3.7\%)^2+(0.75\%)^2}=3.8\%
$$

More accurate model see Colin McAndrew’s JSSC 2003 paper
– [https://www.youtube.com/watch?v=0vtV-PRkuU4](https://www.youtube.com/watch?v=0vtV-PRkuU4)

# 3. 总结

没有必要在仿真的时候调的非常准

![Untitled](IMAGE/Untitled%2026.png)

<aside>
💡 尽可能让电流源部分做的紧凑，并走一根电流线出去

</aside>

![Untitled](IMAGE/Untitled%2027.png)

送一根长的电流线，不要送长的电压线（IR Drop）