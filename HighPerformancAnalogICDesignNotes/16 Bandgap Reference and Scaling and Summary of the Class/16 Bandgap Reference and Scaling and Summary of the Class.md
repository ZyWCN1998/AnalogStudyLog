# 16. Bandgap Reference & Scaling & Summary of the Class

### Bandgap Reference & Scaling & Summary of the Class 内容目录

1. **带隙基准**
    1. 1.1 References
    2. 1.2 核心思路
    3. 1.3 非理想特性
2. **工艺微缩**
3. **Summary of the Class**

# 1. 带隙基准

在片上产生一个高精度的电压基准

## 1.1 References

- R. J. Widlar, "New developments in IC voltage regulators," IEEE J. Solid-State Circuits, pp. 2-7, Feb. 1971.
    - First report, LM309 5V regulator
- • A. P. Brokaw, "A simple three-terminal IC bandgap reference," IEEE J. Solid-State Circuits, pp. 388-393, Dec. 1974.
    - A classic implementation
- C. Palmer and R. Dobkin, "A curvature corrected micropower voltage reference," IEEE Int. Solid-State Conference, pp. 58-59, Feb. 1981.
- G. Nicollini et al., "A CMOS bandgap reference for differential signal processing," IEEE J. Solid-State Circuits, pp. 41-50, Jan. 1991.
    - Offset compensated amplifier
- T.L. Brooks et al., "A low-power differential CMOS bandgap reference," IEEE Int. Solid-State Conf., pp. 248-249, Feb. 1994.
    - Differential output, stacked diodes
- H. Banba et al. "A CMOS bandgap reference circuit with sub-1-V operation," IEEE J. Solid-State Circuits, pp. 670 - 674, May 1999.
- P. Malcovati et al., "Curvature-compensated BiCMOS bandgap with 1-V supply voltage," IEEE J. Solid-State Circuits, pp. 1076-1081, July 2001.

## 1.2 核心思路

利用$kT/q$产生一个随温度正相关的系数

PTAT：与绝对温度变化成正比

利用BJT管子的$V_{BE}$随着温度升高而降低产生一个负温度系数

CTAT：与绝对温度变化成反比

将PTAT与CTAT结合产生一个几乎不随温度变化的电压作为基准

PTAT+CTAT=zero TC

- 高精度的AD转换器的参考电压等

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled.png)

$V_{BE}$

$$
V_{BE}\approx\frac{kT}{q}ln(\frac{I_C}{I_S})\\\approx\frac{kT}{q}ln(\frac{I_C}{I_0}e^{V_{G0}/(kT/q)})\\\approx V_{G0}-\frac{kT}{q}ln(\frac{I_0}{I_C})
$$

$I_0$ is a device parameter, which is (unfortunately) not completely independent of temperature

$V_{G0}$ is the bandgap voltage of silicon "extrapolated to 0°K”

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%201.png)

BandGap电压天然是带一个曲率的

### $V_{BE}$温度系数

对温度求偏导有

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%202.png)

<aside>
💡 大约为2mV每开尔文

</aside>

### PTAT与CTAT加和

利用CMOS实现，需要一个过0的PTAT

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%203.png)

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%204.png)

1比n实现的版图：共质心的匹配

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%205.png)

设计实例

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%206.png)

## 1.3 非理想特性

- 曲线的斜率
    - $I_0$对温度的依赖关系
- offset电压以及运放随温度变化的漂移
- 电阻的不匹配和电阻随温度系数变化
- BJT之间的不匹配以及有限β带来的误差

## $V_{BE}$ Revisited

一个更精确的经验公式，关于$V_{BE}$的表达式为

$$
V_{BE}\approx V_{G0}-\frac{kT}{q}ln(\frac{K_1\cdot T^r}{I_C})
$$

r为工艺参数，一般为3~6

### **Curvature**

实际上的$V_{BE}$并非为一条直线，而是弯曲的曲线，同样会影响加和之后的精度

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%207.png)

### 集电极电流

我们假设集电极的电流是不随温度变化的，但实际上又以下经验公式给出

$$
V_{BE}\approx V_{G0}-\frac{kT}{q}ln(K\frac{T^r}{T^n})
$$

对于理想的PTAT，n=1

重写$V_{BE}$

$$
\frac{dV_{BE}}{dT}\approx \frac{d}{dT}[-\frac{kT}{q}ln(K\frac{T^r}{T^n})]\\\approx -\frac{k}{q}ln(K\frac{T^r}{T^n})-\frac{kT}{q}\frac{K(r-n)T^(r-n-1)}{K\frac{T^r}{T^n}}\\\approx-\frac{k}{q}[ln(K\frac{T^r}{T^n})-(r-n)]\\= -\frac{V_{G0}-V_{BE}+(r-n)\frac{kT}{q}}{T}
$$

<aside>
💡 不同处理高阶温度系数的方法

</aside>

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%208.png)

**80%的电路使用了这种最简单的，没有做补偿的bandgap电路。曲线的补偿可能可以不做，但是运放的offset是一定要想办法解决的**

- chop
- autozero（较少，噪声的混叠）

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%209.png)

对于不同芯片，其offset电压可能不同，不同的bandgap可能需要进行单独调节

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2010.png)

低压（低于1.2V）bandgap

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2011.png)

# 2. 工艺微缩

<aside>
💡 在数字工艺中受益，而在受总噪声限制的模拟电路设计中并没有帮助

</aside>

摩尔定律：商业定律

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2012.png)

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2013.png)

尺度变小，速度变快

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2014.png)

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2015.png)

价钱更低

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2016.png)

赚到钱

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2017.png)

<aside>
💡 40nm, 28nm 既能兼顾数字又能兼顾模拟

</aside>

scaling对模拟电路的获益：更快的晶体管速度

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2018.png)

scaling对模拟电路的伤害：更低的本征增益和电源电压

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2019.png)

<aside>
💡 省成本是最重要的

</aside>

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2020.png)

信号摆幅下降：噪声水平没有下降，但信号的幅度变低了

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2021.png)

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2022.png)

更大的ft：更大的gm/Id选择范围

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2023.png)

<aside>
💡 低功耗设计（过去20年的热点）

</aside>

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2024.png)

### Mismatch

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2025.png)

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2026.png)

对于先进工艺下，除了器件自己决定自己性能，附近的环境也会决定其性能（应力，溅射等）

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2027.png)

对于任何需要成比例的东西：W，L，F完全一样，改M

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2028.png)

# 3. Summary

- $g_m/I_d$设计方法：晶体管模型

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2029.png)

换一个维度来观察晶体管

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2030.png)

- 分析电路的方法（KCL，KVL）

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2031.png)

- 构建模拟电路的元模块

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2032.png)

- 反馈

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2033.png)

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2034.png)

- 带电容的OTA负反馈

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2035.png)

- 噪声

![Untitled](16%20Bandgap%20Reference%20&%20Scaling%20&%20Summary%20of%20the%20Cl%200c9a067c36b346c4ae3e3a00a5715d4c/Untitled%2036.png)