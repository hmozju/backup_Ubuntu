# 伪随机数和随机数种子

>虽然计算机很擅长做精确计算，但是它们处理随机事件时非常不靠谱。

* ***解决方法:*** 
大多数随机数算法都努力创造一种呈均匀分布且难以预测的数据序列，但是在算法初始化阶段都需要提供随机数“种子(random seed)”。而完全相同的种子每次将产生同样的“随机”数序列，因此我们用系统时间作为随机数序列生成的起点。这样做会让程序运行时更具有随机性。

Python的伪随机数(pseudorandom number)生成器用的是[梅森旋转(Mersenne Twister)算法](https://en.wikipedia.org/wiki/Mersenne_Twister),它产生的随机数很难预测且呈均匀分布，就是有点耗费CPU资源，真正好的随机数可不便宜！

Python里产生伪随机数种子的代码：
```python
#!/usr/bin/env python
-*- coding: utf-8 -*-

import datetime
import random

random.seed(datetime.datetime.now())

#  0-9中产生一个随机整数

random.randint(0,9)
```