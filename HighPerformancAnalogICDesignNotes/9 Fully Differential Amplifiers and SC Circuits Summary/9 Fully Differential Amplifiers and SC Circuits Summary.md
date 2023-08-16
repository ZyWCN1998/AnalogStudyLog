# 9. Fully Differential Amplifiers & SC Circuits Summary

### Fully Differential Amplifiers & SC Circuits 内容目录：

1. **全差分电路**
    1. 1.1 全差分电路 
    2. 1.2 负载
    3. 1.3 开关电容
2. **开关电容电路的应用**
    1. 2.1 Switch C的噪声
    2. 2.2 Switch C放大器的噪声
    3. 2.3 进一步完善的小信号模型
3. **OPA与OTA**

<aside>
💡 Corner是给数字电路准备的，对于模拟电路一定要跑蒙特卡洛仿真

</aside>

# 1. 全差分电路

输出共模无法定义，上面的电流镜和下面的电流镜互相争抢电流。

![Untitled](IMAGE/Untitled.png)

引入**共模负反馈**，解决全差分共模电压不确定的问题

检测共模环路，调整电流源的电流

通过一个average电路取出共模电压→通过一个放大器比较我们想要的共模电压→反馈回来调节电流源→最终得到上面电流源和下面电流源匹配的结果

![Untitled](IMAGE/Untitled%201.png)

<aside>
⚠️ 但凡涉及环路，就涉及稳定性问题

</aside>

由于电流镜的管子Rout不一定相同，需要利用共模负反馈实现调整电流

- 上管电流变大，将输出电压往上拽，减小上管的Vgs
- 上管电流变小，将输出电压往下拽，增大上管的Vgs

![Untitled](IMAGE/Untitled%202.png)

## 1.1 全差分电路

- 全差分：有效降低共模干扰与环境coupling，PSRR和CMRR较高，输出摆幅变大，确定的共模电压值。
    - 比如传感器的GND实际上并不是芯片上的GND，只选用单端的运放会出问题
- 单端：设计简单，元件少

![Untitled](IMAGE/Untitled%203.png)

<aside>
💡 信号跨模块时需要额外注意

</aside>

全共模电路差模小信号模型

![Untitled](IMAGE/Untitled%204.png)

## 1.2 负载

RL直接挂在负载端，会显著降低增益。考虑用一个x1的buffer来驱动

![Untitled](IMAGE/Untitled%205.png)

![Untitled](IMAGE/Untitled%206.png)

考虑带一个小电阻的情况，这个buffer是很难实现的

- buffer的输出阻抗要小于0.1倍的$R_L$
- 消耗电压预算，限制了输出摆幅
- 额外的功耗与面积

以LDO为例，运放后接一个大的Pass transistor，被晶体管的大电容严重拉低了带宽

$**\to$用一个x1倍的buffer将二者隔开**

多级运放：人为造一个可以被牺牲掉的增益，将第二级的增益牺牲掉。第二级同时起到了隔离第一级和输出电容电阻的作用。

![Untitled](IMAGE/Untitled%207.png)

## 1.3 开关电容

一个好电路：在能解决问题的情况下最简单的电路

![Untitled](IMAGE/Untitled%208.png)

$$
\Delta q=C(V_1-V_2)\\i_{avg}=\frac{\Delta q}{\Delta t}=\frac{\Delta q}{T}=f\cdot C(V_1-V_2)\\ 
$$

$$
i=\frac{V_1-V_2}{R}\to R_{avg}=\frac{1}{f\cdot C}
$$

# 2. 开关电容电路的应用

- 适配CMOS电路：CMOS电路中最重要的就是开关
- 相比RC有更准的Corner frequency且可以改变：RC在集成电路工艺中无法做到非常精准，且如果需要拓展带宽，RC电路需要更大的C，而SC电路只需要把频率提升10倍即可
- 传输函数完全由电容的比例决定
- 可以实现一个较大的时间常数而不是用大的电阻

R. Gregorian et al., "Switched-Capacitor Circuit Design," Proceedings of the IEEE, Vol. 71, No. 8, August 1983.

<aside>
💡 One of the most significant inventions in the history of ICs

</aside>

![Untitled](IMAGE/Untitled%209.png)

## 2.1 Switch C的噪声

SC本质上还是做了一个电阻，其噪声与一个正常的电阻没有区别

![Untitled](IMAGE/Untitled%2010.png)

本课程中只考虑$\phi 2$阶段的SC电路，而不用担心开关切换问题

![Untitled](IMAGE/Untitled%2011.png)

![Untitled](IMAGE/Untitled%2012.png)

$$
i=v_i\cdot j \omega C_s\\v_o=-i\cdot \frac{1}{j\omega C_f}\\\frac{v_o}{v_i}=-\frac{C_s}{C_f}
$$

<aside>
💡 Switch Cap最终的增益和没有开关的情况实际上是一样的

</aside>

## 2.2 Switch C放大器的噪声

在电路中的单个节点对全频带进行积分，噪声最终和电容的大小成反比

整体的噪声量级由放大器的结构决定

![Untitled](IMAGE/Untitled%2013.png)

# 3. OPA与OTA

### OPA:

- 更加通用的设计
- 理想压控电压源
- 输出阻抗很低（一个OTA+一个x1的buffer）
- 能驱动电容和电阻

### OTA：

- 大部分片上放大器为OTA
- 理想的压控电流源
- 大输出阻抗
- 难以驱动电阻负载
- 使用电容（开关电容）反馈网络
- 能驱动一个电容

![Untitled](IMAGE/Untitled%2014.png)