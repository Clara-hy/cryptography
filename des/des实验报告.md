#DES实验报告

----------

##实验目的 
了解DES算法基本工作原理，体会并理解分组密码算法的混淆和扩散概念。了解Sbox工作原理及效果。了解DES的工作模式和填充方式。了解差分攻击的基本原理

----------

##实验题目 
DES算法与差分攻击

----------

##实验原理与理论基础 
#####加密算法的主流程图
![](https://i.imgur.com/dX429vb.jpg)
#####解密算法
解密和加密使用相同的算法。加密和解密唯一不同的是秘钥的次序是相反的。就是说如果每一轮的加密秘钥分别是K1、K2、K3...K16，那么解密秘钥就是K16、K15、K14...K1。为每一轮产生秘钥的算法也是循环的。加密是秘钥循环左移，解密是秘钥循环右移。解密秘钥每次移动的位数是：0、1、2、2、2、2、2、2、1、2、2、2、2、2、2、1。
#####差分分析
《密码学引论》P134

基本原理：通过分析明文对的差分值对密文对的差分值的影响来恢复密钥或密钥的某些位。

定义4-1 设两个二元域上n比特串Y和Y*，称△Y=Y⊕Y*为它们的差分值。

#####差分分布原理
因为Sj盒的输出差分△Sj=(Bj,Bj*)=Sj(Bj)⊕Sj(Bj*)是长度为4的比特串，故共有16种输出差分值。对于具有此输入差分的输入对集合中的每个输入对，可以计算出Sj盒的一个输出差分。共可计算出64个输出差分，它们分布在16个可能的输出差分值上。统计每个可能值的个数，则可得到Sj关于各输入对的输出差分分布。对于分组密码来说，S盒的所有可能的输入对于S盒输出差分值分布的不均匀性，是对分组密码进行差分分析的基础。
#####获得密钥Kj集合的原理
《密码学引论》P138

定理4-1 DES S盒的输入差分与密钥无关

虽然S盒的输入差分与密钥无关，但是S盒的输出差分与密钥相关。

定理4-2 设Ej和Ej*是S盒Sj的两个输入，输入差分△E=Ej⊕Ej*，Sj的输出差分为△Sj，则密钥Kj出现在集合Testj(Ej,Ej*，△Sj)中，即Kj∈Testj(Ej,Ej*，△Sj)。

----------
  
##实验内容
1. 实验DES算法 
2. 通过改变DES算法明文和密文内容观察加密后输出统计结果
3. 实现生成指定差分的明文对，实现对特定差分输入的Sbox差分输出分布，观察 DES S-box 输入差分与密钥无关，输出差分与密钥相关特性。 
4. 实现简单的GUI界面

----------

##实验结果 
######开始界面
![开始界面](https://i.imgur.com/xAwI4MI.png)
######选择界面且改变明文
![选择界面且改变明文](https://i.imgur.com/h2f2fFP.png)
######改变明文的统计数据1
![改变明文的统计数据1](https://i.imgur.com/LKf5EK7.png)
######改变明文的统计数据2
![改变明文的统计数据2](https://i.imgur.com/ARn0aaY.png)
######改变密钥
![改变密钥](https://i.imgur.com/ynYHK9B.png)
######改变密钥的统计数据1
![改变密钥的统计数据1](https://i.imgur.com/rUIlmtS.png)
######改变密钥的统计数据2
![改变密钥的统计数据2](https://i.imgur.com/ZL979DC.png)
######实现表4-1的差分分布
![实现表4-1的差分分布](https://i.imgur.com/cWVzwLF.png)
######实现例4-2的示例1
![实现例4-2的示例1](https://i.imgur.com/kx0WGVV.png)
######实现例4-2的示例2
![实现例4-2的示例2](https://i.imgur.com/TseCOeF.png)
----------

##实验结果分析 
能准确的呈现实现结果

##实验心得
在实现任务4的时候遇到挺多问题的。

1. 书里描述的是根据输出差分即可查表得出答案（任务1显示的那个表），但是任务1的实现方式是直接输出答案，所以在实现任务4的时候要换一种想法：把满足条件的输出差分对应的可能的输入用二维数组装起来。
2. 任务4只实现了输出基于S1盒的密钥集合，由于dev不支持变长数组，所以我以有12个可能的输入的情况为数组最大值，把二维数组初始化为[13][6]，但这就导致了输入没有12那么多的时候，数组的剩余行出现随机数的现象。解决方法是：录入完正确的答案之后，下一行的第一个元素赋一个大于1的值，用来在之后的输出做筛选。
3. dev与vc有些地方不兼容，导致在dev上能运行的，vc却频频出错而且改不了。之后决定抛弃vc。
