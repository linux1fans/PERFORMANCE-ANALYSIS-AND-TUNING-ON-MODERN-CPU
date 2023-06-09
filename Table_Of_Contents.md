# 目录

## 目录                           
### 1 引言
#### 1.1 为什么我们仍然需要性能调优？
#### 1.2 谁需要性能调优？
#### 1.3 什么是性能分析？
#### 1.4 本书讨论的内容是什么？
#### 1.5 本书中没有涉及的内容是什么？
#### 1.6 章节总结

## 第一部分. 在现代CPU上进行性能分析
### 2 性能测量
#### 2.1 现代系统中的噪声
#### 2.2 在生产环境中进行性能测量
#### 2.3 自动检测性能回归
#### 2.4 手动性能测试
#### 2.5 软件和硬件计时器
#### 2.6 微基准测试
#### 2.7 章节总结

### 3 CPU微架构
#### 3.1 指令集架构
#### 3.2 流水线技术
#### 3.3 利用指令级并行性（ILP）
##### 3.3.1 OOO执行
##### 3.3.2 超标量引擎和VLIW
##### 3.3.3 预测执行
#### 3.4 利用线程级并行性
##### 3.4.1 同时多线程
#### 3.5 内存层次结构
##### 3.5.1 缓存层次结构
###### 3.5.1.1 缓存中的数据放置
###### 3.5.1.2 在缓存中查找数据
###### 3.5.1.3 处理缺失
###### 3.5.1.4 处理写操作
###### 3.5.1.5 其他缓存优化技术
##### 3.5.2 主存
#### 3.6 虚拟内存
#### 3.7 SIMD多处理器
#### 3.8 现代CPU设计
##### 3.8.1 CPU前端
##### 3.8.2 CPU后端
#### 3.9 性能监控单元
##### 3.9.1 性能监控计数器

### 4 性能分析中的术语和指标
#### 4.1 已退役指令 vs. 已执行指令
#### 4.2 CPU 利用率
#### 4.3 CPI & IPC
#### 4.4 UOPs（微操作）
#### 4.5 流水线槽位
#### 4.6 核心 vs. 参考周期
#### 4.7 缓存缺失
#### 4.8 预测错误的分支

### 5 性能分析方法
#### 5.1 代码插桩
#### 5.2 跟踪
#### 5.3 工作负载特征
##### 5.3.1 计数性能事件
##### 5.3.2 手动收集性能计数器
##### 5.3.3 多路复用和缩放事件
#### 5.4 抽样
##### 5.4.1 用户模式和基于硬件事件的抽样
##### 5.4.2 寻找热点
##### 5.4.3 收集调用堆栈
##### 5.4.4 火焰图
#### 5.5 Roofline 性能模型
#### 5.6 静态性能分析
##### 5.6.1 静态 vs. 动态分析器
#### 5.7 编译器优化报告
#### 5.8 章节总结

### 6 用于性能分析的 CPU 特性
#### 6.1 自上而下微架构分析
##### 6.1.1 Intel® VTune™ Profiler 中的 TMA
##### 6.1.2 Linux Perf 中的 TMA
##### 6.1.3 步骤1：确定瓶颈
##### 6.1.4 步骤2：定位代码位置
##### 6.1.5 步骤3：解决问题
##### 6.1.6 总结
#### 6.2 最后分支记录
##### 6.2.1 收集 LBR 堆栈
##### 6.2.2 捕获调用图
##### 6.2.3 标识热点分支
##### 6.2.4 分析分支错误率
##### 6.2.5 机器代码的精确定时
##### 6.2.6 估算分支结果概率
##### 6.2.7 其他用途
#### 6.3 基于处理器事件的抽样
##### 6.3.1 精确事件
##### 6.3.2 降低抽样开销
##### 6.3.3 分析内存访问 
### 6.4 Intel 处理器追踪
#### 6.4.1 工作流程 
#### 6.4.2 时间包 
#### 6.4.3 收集和解码追踪数据 
#### 6.4.4 用途 
#### 6.4.5 磁盘空间和解码时间
### 6.5 章节总结

## Part2. 用于 CPU 的源代码调优 100
### 7 CPU 前端优化 103
#### 7.1 机器代码布局
#### 7.2 基本块
#### 7.3 基本块放置
#### 7.4 基本块对齐
#### 7.5 函数拆分
#### 7.6 函数分组
#### 7.7 基于配置文件的优化
#### 7.8 为ITLB进行优化
#### 7.9 章节总结
### 8 CPU后端优化
#### 8.1 内存受限
##### 8.1.1 缓存友好的数据结构
###### 8.1.1.1 顺序访问数据
###### 8.1.1.2 使用适当的容器
###### 8.1.1.3 数据打包
###### 8.1.1.4 对齐和填充
###### 8.1.1.5 动态内存分配
###### 8.1.1.6 为内存层次结构调优代码
##### 8.1.2 显式内存预取
##### 8.1.3 为DTLB进行优化
###### 8.1.3.1 显式巨页
###### 8.1.3.2 透明巨页
###### 8.1.3.3 显式 vs. 透明巨页
#### 8.2 核心受限
##### 8.2.1 内联函数
##### 8.2.2 循环优化
###### 8.2.2.1 低级优化
###### 8.2.2.2 高级优化
###### 8.2.2.3 发现循环优化机会
###### 8.2.2.4 使用循环优化框架
##### 8.2.3 向量化
###### 8.2.3.1 编译器自动向量化
###### 8.2.3.2 发现向量化机会
###### 8.2.3.3 向量化是非法的
###### 8.2.3.4 向量化没有好处
###### 8.2.3.5 循环向量化但使用标量版本
###### 8.2.3.6 循环向量化方式不佳
###### 8.2.3.7 使用具有显式向量化的语言
#### 8.3 章节总结
### 9 优化错误的预测
#### 9.1 用查找表替换分支
#### 9.2 用预测替换分支
#### 9.3 章节总结
### 10 其他调优领域
#### 10.1 编译时计算
#### 10.2 编译器内嵌函数
#### 10.3 缓存预热
#### 10.4 检测慢速浮点运算
#### 10.5 系统调优
### 11 优化多线程应用程序
#### 11.1 性能扩展和开销
#### 11.2 并行效率度量
##### 11.2.1 有效CPU利用率
##### 11.2.2 线程数
##### 11.2.3 等待时间
##### 11.2.4 自旋时间
#### 11.3 使用Intel VTune Profiler进行分析
##### 11.3.1 查找昂贵的锁
##### 11.3.2 平台视图
#### 11.4 使用Linux Perf进行分析
##### 11.4.1 查找昂贵的锁
#### 11.5 使用Coz进行分析
#### 11.6 使用eBPF和GAPP进行分析
#### 11.7 检测一致性问题
##### 11.7.1 缓存一致性协议
##### 11.7.2 真共享
##### 11.7.3 伪共享
#### 11.8 章节总结
## 结语
## 术语表
## 参考文献
## 附录A. 减少测量噪声
## 附录B. LLVM向量化器
``
