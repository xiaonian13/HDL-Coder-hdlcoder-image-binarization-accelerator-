# HDL-Coder-hdlcoder-image-binarization-accelerator
基于 MATLAB HDL Coder 自动生成的图像二值化硬件 IP 核，在 Vivado 中集成 AXI VIP 完成全套双向读写时序验证，并在 Vitis 2020.2 下基于 XCZU15EG 平台实现裸机驱动参数控制的完整全栈软硬件协同设计项目

### 项目功能
用ZYNQ实现二值化算法的加速

### 开发环境
- 算法仿真：MATLAB R2020b
- 硬件开发：Vivado2020.2 、vitis2020.2
- 开发语言：Matlab脚本、system verilog、c、verilog
- 硬件平台：xczu15eg-ffvb1156-2-i
- 系统环境：Windows11

### 项目目录结构
- matlab_sim      Matlab 算法源码与仿真脚本
- vivado_project  Vivado 工程文件
- vitis_project   vitis 工程文件
- data            测试数据集、输入输出数据
- doc             设计文档、流程图、实验报告
- result          仿真结果、加速性能测试数据
- README.md       项目说明文档

### 使用教程
1. **Matlab算法验证**
进入`test4`文件夹，运行测试脚本`tb_img_threshold.m`，这个测试脚本会调用`img_threshold.m`，测试图片来自于matlab自带的图片，生成的图片会保存在本文件夹。
经验证，该算法的功能正确。
<img width="390" height="289" alt="image" src="https://github.com/user-attachments/assets/586cfb50-1746-4ba3-ab4f-72adc9318da7" />

2. **导出IP核**
使用的是matlab自带的APP hdlcoder,点击hdlcoder
<img width="706" height="369" alt="image" src="https://github.com/user-attachments/assets/558f5584-d18d-4793-a758-80d036bd6138" />
HDL Workflow Advisor：保持不变即可，点击运行
Define Input Types：保持不变即可，点击运行
Fixed-Point Conversion：
<img width="875" height="121" alt="image" src="https://github.com/user-attachments/assets/5293d730-3a3c-4526-bd9e-d41c26d2fe2b" />
Select Code Generation Target：
<img width="655" height="400" alt="image" src="https://github.com/user-attachments/assets/9dc9c2d1-b56e-4a90-8553-347c7b51f149" />
Set Target Interface：
<img width="1304" height="679" alt="image" src="https://github.com/user-attachments/assets/171d6230-8e44-47c3-b706-9c2010924d87" />
HDL Code Generation：改成生成Verilog语言，其他默认，点击运行后生成IP和IP的说明书
<img width="380" height="356" alt="image" src="https://github.com/user-attachments/assets/66e1b6d3-19fc-401a-a2bc-190f5faa9488" />

3. **IP仿真测试与导出硬件**
在Vivado中导入生成硬件IP，完成IP的仿真：
<img width="686" height="306" alt="image" src="https://github.com/user-attachments/assets/7cbd0e76-53a1-4665-9055-13036bc60420" />
仿真通过后，实现PL与PS的互联：
<img width="1225" height="405" alt="3df55c6f-c4be-47b5-87d6-2adbbdd99746" src="https://github.com/user-attachments/assets/fa1ff3da-63da-4a0d-862d-a8e080d831c9" />
最后导出硬件

4. **上板运行测试**
在vitis中将`main.c`代码下载至Zynq开发板，完成数据收发与硬件加速实测。
<img width="546" height="280" alt="image" src="https://github.com/user-attachments/assets/c231fa8e-e52a-4803-93e7-d39506451327" />

### 性能指标
- 软件运行耗时：xxx ms
- 硬件加速耗时：xxx ms
- 加速比：xx倍
- FPGA资源占用：LUT/FF/BRAM/DSP使用率
- 算法精度损失：定点误差范围

### 核心设计思路
1. 先写软件思维的 MATLAB 算法 → 验证正确 → 再重构 / 转写成硬件思维的代码（hdlcoder）
2. 生成的IP核需要做软件和硬件仿真验证
3. 架构优化：采用流水线、循环展开、数组分块提升并行计算能力
4. 通信架构：使用AXI-Stream高速数据流完成PS与PL数据交互
5. 数据类型优化：浮点运算转为定点运算，缩减硬件资源开销

### 作者信息
- 作者：xiaonian13
- 开发时间：2026.5.21
- 联系方式：1991676257@qq.com

