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
进入`test4`文件夹，运行测试脚本`tb_img_threshold.m`，这个测试脚本会调用img_threshold，测试图片来自于matlab自带的图片，生成的图片会保存在本文件夹。
经验证，该算法的功能正确。<img width="390" height="289" alt="image" src="https://github.com/user-attachments/assets/586cfb50-1746-4ba3-ab4f-72adc9318da7" />


3. **HLS硬件综合**
打开Vivado HLS，导入`hls_code`内源码，配置时钟周期、位宽、优化策略，完成C仿真与综合导出IP。

4. **Zynq工程搭建**
在Vivado中导入生成硬件IP，完成PS-PL互联、引脚配置、时序约束，生成比特流文件。

5. **上板运行测试**
将比特流下载至Zynq开发板，完成数据收发与硬件加速实测，对比软硬件运行效率。

### 性能指标
- 软件运行耗时：xxx ms
- 硬件加速耗时：xxx ms
- 加速比：xx倍
- FPGA资源占用：LUT/FF/BRAM/DSP使用率
- 算法精度损失：定点误差范围

### 核心设计思路
1. 先写软件思维的 MATLAB 算法 → 验证正确 → 再重构 / 转写成硬件思维的代码（hdlcoder）
2. 生成的
3. 架构优化：采用流水线、循环展开、数组分块提升并行计算能力
4. 通信架构：使用AXI-Stream高速数据流完成PS与PL数据交互
5. 数据类型优化：浮点运算转为定点运算，缩减硬件资源开销

### 注意事项
1. HLS代码禁止使用动态内存、递归、大量浮点库函数，保证可综合性
2. 定点量化过程需严格把控精度，避免算法效果大幅下降
3. Zynq板卡型号、时钟频率可根据自身硬件自行修改适配
4. 仿真数据与实测数据存在小幅偏差属正常现象

### 作者信息
- 作者：xiaonian13
- 开发时间：2026.5.21
- 联系方式：1991676257@qq.com

