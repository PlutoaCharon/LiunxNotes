## 项目

本项目是实验室的一个`简历招聘推荐系统`, 是由Python进行各大网站的爬取将数据存入到Mysql中, 然后使用Hadoop的MapReduce进行数据统计, HIve进行数据存储, 最后使用Django+pyecharts进行数据可视化, 当时还想可以使用机器学习构建模型形成预测, 但是自己只是准备了GPU的实验环境, 只有跑几个TensorFlow的Demo

### [爬取疫情数据，以django+pyecharts实现数据可视化web网页](https://www.cnblogs.com/byadmin/p/12303768.html)

### [pyecharts](https://pyecharts.org/#/zh-cn/quickstart)

## 

### [基于Facenet与MTCNN的人脸识别](https://blog.csdn.net/qq_43442524/article/details/101374261)

### [在Ubuntu的Anaconda环境下创建深度学习环境](https://blog.csdn.net/qq_43442524/article/details/101372346)

### [WindowsServer2016 Anaconda下TensorFlow-GPU环境搭建详细教程（包含CUDA+cuDNN安装过程）](https://blog.csdn.net/qq_43442524/article/details/103038214)

- CUDA（Compute Unified Device Architecture），是NVIDIA推出的运算平台。
- cuDNN 专门针对Deep Learning框架设计的一套GPU计算加速方案。

## 比赛

全国高校大数据能力提升大赛总决赛“联想杯”与第二届“全国大学生大数据技能竞赛”总决赛 都使用到了Python爬虫作为前期的数据采集

用到的Python库

- Python3
- xpath
- etree
- selenium
- BeautifulSoup
- requests
- os
- io
- re

### [Python使用BeautifulSoup与selenium爬取Boos直聘](https://blog.csdn.net/qq_43442524/article/details/101932179)

全国高校大数据能力提升大赛总决赛“联想杯”

- 进行数据爬取
- 将爬取的数据文件导入到mysql中
- 使用sqoop将mysql数据导入HIve中
- 编写MapReduce进行HDFS的词频统计
- 机器学习模型

### MapReduce

https://www.jianshu.com/p/6b6a42a0740c

在Hadoop2.x的版本中，文件块的默认大小是128M，老版本中默认是64M；

寻址时间：HDFS中找到目标文件块（block）所需要的时间。

**原理：**

文件块越大，寻址时间越短，但磁盘传输时间越长；

文件块越小，寻址时间越长，但磁盘传输时间越短。

https://blog.csdn.net/maketubu7/article/details/80784680?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase

[https://blog.csdn.net/qq_43442524/article/details/100077126?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522158917065819726867843219%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=158917065819726867843219&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v25-3-100077126.nonecase&utm_term=hadoop](https://blog.csdn.net/qq_43442524/article/details/100077126?ops_request_misc=%7B%22request%5Fid%22%3A%22158917065819726867843219%22%2C%22scm%22%3A%2220140713.130102334.pc%5Fblog.%22%7D&request_id=158917065819726867843219&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_v2~rank_v25-3-100077126.nonecase&utm_term=hadoop)