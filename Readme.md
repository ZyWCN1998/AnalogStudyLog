# 0. ReadMe

## 1. Introduction

因为刚开课的时候自己刷拉扎维刷的太慢了，以至于不是很能跟得上课堂内容。在6月刷完拉扎维前十章&搭了一个非常简单的二级（五管+CS）放大器之后，重新听课有了很多新的收货和体会。

恰逢师兄毕业了，工作压力大起来了，没有那么多成块的时间了。于是决定每天至少拿出1h学习模拟电路的知识，并把每天学习记录或调试内容在此。

## 2. Outline

### 文件列表

```bash

<AnalogStudyLog> (root)
|
+- July2023 (#dir for every mounth's dotes)
|  |
|  + July* (#dir for everyday notes)
|				| IMAGE (#Image file for markdown)
|				| July*.md (#everday study note or debug log)
|  ...
+- Readme.md (#this file)
```

这里 👇列出的是目前在进行的，以后会搞的或者以前搞了还没整理的暂时不放

- **课程Project：二级运放设计**
    - [x]  gm-Id查找表建立
    - [ ]  运放Sizing
    - [ ]  CMFB设计
    - [ ]  DC Sweep
    - [ ]  DC Analysis
    - [ ]  Stability (stb) Analysis
    - [ ]  AC Analysis
    - [ ]  Transient Analysis
    - [ ]  Noise Analysis
    - [ ]  PVT
- **春季课《高性能模拟集成电路设计》**
    - [x]  0. class intro
    - [x]  1. long channel model (7.14)
    - [x]  2. small signal model (7.14)
    - [x]  3. gm-id intro (7.20)
    - [x]  4. gm-id based design (7.20)
    - [x]  5. extrinsic capacitance (7.21)
    - [x]  6. miller approx (7.28)
    - [x]  7. noise (7.25)
    - [x]  8. backgate and common gate (7.31)
    - [x]  9. common drain（8.2）
    - [x]  10. diff pair（8.3）
    - [x]  11. current mirror and offset（8.3）
    - [x]  12. OTA and CS circuit（8.5）
    - [x]  13. process variation and feedback intro（8.6）
    - [x]  14. feedback and stability analysis（8.7）
    - [x]  15. two-stage ota（8.8）
    - [x]  16. frequency compensation and noise（8.8）
    - [x]  17. OTA design consideration（8.9）
    - [x]  18. step response（8.9）
    - [x]  19. slew（8.10）
    - [x]  20. blackman, cmfb, ota variation（8.11）
    - [x]  21. output stage（8.12）
    - [x]  22. bias（8.15）
    - [x]  23. bandgap reference（8.16）
    - [x]  24. technology scaling（8.16）
    - [x]  25. summary（8.16）

这里👇列出的是之前上课手写的笔记（还未来得及整理），Github无法上传大于50M文件

- **Razavi: Electronic II**
    - [(391) Razavi Electronics 1, Lec 1, Intro., Charge Carriers, Doping - YouTube](https://www.youtube.com/watch?v=yQDfVJzEymI&list=PLyYrySVqmyVPzvVlPW-TTzHhNWg1J_0LU)
- **西交Razavi: Design of Analog CMOS Integrated Circuits, chapter 1~10**
    - [【西安交通大学】集成电路设计 模拟CMOS XJTU_张鸿教授（对应Razavi 1-10章）_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1SK4y1N7wN/?spm_id_from=333.337.search-card.all.click&vd_source=8fd5b7e6e559a203f9156dfb7271544f)
- **Signal & system: Alan Oppenheim**
    - [(391) Lecture 2, Signals and Systems: Part 1 | MIT RES.6.007 Signals and Systems, Spring 2011 - YouTube](https://www.youtube.com/watch?v=6xaaeop7gJ8&list=PLADC1A1B7FA7FF7B6)

## 3. 工作记录

记录按周更新备份，每天的更新在腾讯文档，此处主要做备份

| 日期 | 总时长 | 计划任务 | 卡了一段时间的bug或想法 | 备注（当天硕士专业主要工作） |
| --- | --- | --- | --- | --- |
| 7.10 | 1h | lecture01-1 | 暂无 | 量子点样品托PCB绘制 |
| 7.11 | 1h | lecture01-2 | 暂无 | PCB仿真（20G） |
| 7.12 | 1h | lecture01-3 | 暂无 | 会议PPT制作 |
| 7.13 | 1.5h | lecture01-3 | ADE-L保存仿真状态 | 赶火车，去上海参会 |
| 7.14 | 2h | Summary of long channel Model | 暂无 | 参会，准备报告pre |
| 7.15 | 1.5h | lecture02-1 | 暂无 | 参会，准备报告pre |
| 7.16 | 2h | lecture02-2 | 暂无 | 参会，做报告 |
| 7.17 | 1.5h | lecture02-3 | 暂无 | 返程，上海→北京 |
| 7.18 | 2h | lecture03-1 | 暂无 | 休息了一天 |
| 7.19 | 1h | lecture03-2 | 暂无 | 休息了一天 |
| 7.20 | 2h | Summary of gm-Id | 多仿几种不同的Vds看一下 | 总结上次指栅器件数据，准备汇报 |
| 7.21 | 2h | Summary of ext. cap. | 之前没特意仿过电容，应该仿一下电容看一下 | 与老板meeting，准备写低温滤波器的专利 |
| 7.22 | 1h | lecture03-2 noise. | TIA的输入应该是电压源还是电流源占主导？ | 低温滤波器的专利写作 |
| 7.23 | 1.5h | lecture03-3 | 暂无 | 专利图绘制 |
| 7.24 | 1h | lecture04-1 | 阻容感的自由度？ | 与老板meeting，修改专利 |
| 7.25 | 1.5h | Summary of noise | 暂无 | 接着修改专利，研究北大的专利申请流程，帮北京量子院修改了一版低温样品托 |
| 7.26 | 1h | lecture04-2 | 暂无 | 修改样品托PCB，热沉，采购元器件。写第二个Switch box的专利 |
| 7.27 | 1.5h | lecture04-3 | ZVTC应该多找几道例题做下 | 继续写第二个Switch box的专利 |
| 7.28 | 1.5h | Summary of Miller | 暂无 | 与老板meeting，递交第二个专利 |
| 7.29 | 1h | lecture05-1 | 自己仿真下gmb/gm试试 | 第一个专利上系统走流程，帮量子院仿真修改之后PCB的S21 |
| 7.30 | 1.5h | lecture05-2 | 拉扎维里面的从这个node看进去该如何理解（加一个测试电压/电流源？） | 准备帮量子院修改的PCB的加工文件，合同，走财务流程。继续改第二个专利 |
| 7.31 | 2h | Summary of backgate & CG | 暂无 | 北京市终于出面上项目的指南了，开始接着写之前的本子。修改第二个专利 |