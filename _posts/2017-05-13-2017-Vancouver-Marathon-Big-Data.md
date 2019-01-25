---
layout:     post
title:      2017 Vancouver Marathon "Big Data"
subtitle:   2017温哥华马拉松“大数据”
date:       2017-05-13
author:     Ama
header-img: img/post-bg-van.jpg
catalog: true
tags:
    - Python
    - Crawler
    - Fitness
    - Marathon
---

## 温哥华马拉松简介

温哥华马拉松始于1972年，是加拿大第二大马拉松赛事，历史悠久，赛道风景优美，再加上极棒的赛事组织。《福布斯》杂志授予它“全球十佳马拉松”，CNN称它为“世界上最值得参加的马拉松”之一。

我的首马回忆详见：[70天，从十公里到全马](amathlover.com/2017/05/11/70-Days-From-10K-to-Full-Marathon/)

<img src="http://wx4.sinaimg.cn/large/007BDy7nly1fziwp7snd4j30rs0kujw4.jpg"  style="zoom:60%">


今年，共有4696人报名参加全程马拉松（42.2km），其中男性2829人，女性1866人。实际有成绩的3577人，其中男性2184人，女性1392人（ps: 若干人未填性别）。和国内动不动就几万人抽签相比，人数太少了。


|-- |Total|Male|Female|
|:--:|:--:|:--:|:--:|
|报名|4969|2829|1866|
|实际参赛|3649|2222|1426|
|有成绩|3577|2184|1392|


## 爬虫说明
爬取的网址，即赛事结果查询网址：http://www.sportstats.ca/display-results.xhtml?raceid=44620 

在爬取快要结束时，网站突然更新了，管理员把所有未参加比赛的选手信息全删了，于是这次统计只漏了未参赛选手中的83人。

- 可抓取的选手个人信息
每位选手的姓名（Name），总排名（Overall Place），号码（BIB），年龄分类（Category），性别（Gender），城市（City），省份（Province），国家或地区（Country），同性别排名（Gender Place），年龄分类排名（Category Place），团队名称（Team Name）。以上全部爬下。

- 可抓取的选手比赛成绩信息
每位选手的分段成绩，枪声成绩和芯片纪录的成绩。这里，我只爬取每个分段的配速（Pace），枪声成绩配速（Gun Time Pace）和芯片成绩配速（Chip Time Pace），芯片成绩为选手真实成绩。当时忘了抓总时长，不过也不麻烦，用总配速乘以总路程就可以了，与实际时长稍有误差，但影响不大。有空再把chip time爬下来更新。（2019/01/25注：这个坑一直没填上，sorry）

## 分析与讨论
### 1 国家地区人数分布

举办地在加拿大温哥华，自然本国和美国的选手最多，同时还吸引了52个国家或地区的选手报名，实际参赛者来自其中44个国家或地区，中国来的也不少，谷歌搜出好多温哥华马拉松几日游的旅行团信息。

肯尼亚共五人参加，但包揽第1，3，4，10名，一位选手没成绩。来自美国的选手得了第2，来自加拿大的选手包揽第5~9名，来自中国香港的一位30+选手位列第20名，也很不错。

![countries](http://wx2.sinaimg.cn/large/007BDy7nly1fziwplxzhrj314z0jj78c.jpg)

<img src="http://wx4.sinaimg.cn/large/007BDy7nly1fzixbjznd1j30l10eamz6.jpg" style="zoom:70%">

### 2 年龄分布
这里，采取上海马拉松直通资格作为精英选手评判标准：男子全程为3小时25分以内、女子全程为3小时45分以内。

可以看出，报名选手中，以25岁到50岁为主，精英多在30-34岁男性、25-34岁女性中诞生。

![Age-registered](http://wx4.sinaimg.cn/large/007BDy7nly1fziwr2u5uuj30fx0cimxv.jpg)

![Age-elites](http://wx3.sinaimg.cn/large/007BDy7nly1fziwr84ninj30fx0cimxq.jpg)


注1：19- 为19岁以下的选手，官网只有年龄分类，没有具体年龄。
注2：男子和女子的百分比分别计算，即同性别中各年龄段人数百分比之和为1，请勿进行男女性别之间对比。

### 3 各年龄段前10%选手完赛时长与年龄关系图
为方便绘图，这里采用各年龄段中间值代替年龄段，比如，22代替20-24，27代替25-29，以此类推，19岁以下用18代替。

形状很有趣，以32，即30-34年龄段为最佳，之后向两边递减。

![time+age](http://wx1.sinaimg.cn/large/007BDy7nly1fziwqybc1yj30ku0chmxu.jpg)

样本太少，如果样本数够多，可以得到更清晰的两个尾巴，下图是来自Financial Times对2014年Boston马拉松对各年龄段前10%完赛选手的分析，A tale of two tails。

![a tale of two tails](http://wx3.sinaimg.cn/large/007BDy7nly1fziws922y6j30im0ajtfv.jpg)

来源：http://visualoop.com/infographics/marathon-data-show-gender-patterns-in-runners-performance

### 4 全马总时长直方图
男子全马比赛成绩与人数的关系，横坐标完赛时间（净成绩），纵坐标完赛人数。横坐标的刻度值表示以该数值为上限的五分钟区间，如240表示在完赛时间在3:55-4:00之间的选手数量。所有选手成绩接近非标准的正态分布，在4:15左右完赛的选手最多。注意两个明显高于左右两边人数的时间段：3:55-4:00以及4:25-4:30，说明选手给自己设定目标一般为30min的整数倍，如4:00或4:30，并争取赶在这之前完赛，才造成这个时间段涌现大量人流。

<img src="http://wx2.sinaimg.cn/large/007BDy7nly1fziwq0iy3sj30mj0h2dgn.jpg"  style="zoom:50%">


### 5 全马总时长与BIB号的关系
选手BIB号码是根据报名时填写的预计完赛时间分配的，BIB号分为：0-1200，2000-2999，4000-4999，6000-6999，8000-8999，以及零散的9300以上，25000以上，40000以上。
图中可以看出，个位数及两位数的BIB号为前十名竞争选手，之后每一段比前一段慢一个台阶，直到9000。我的BIB号为4开头的四位数，在最慢那一档，因为当时报名填了5小时完赛。

<img src="http://wx2.sinaimg.cn/large/007BDy7nly1fziwpqn34bj30ys0u0gqq.jpg" style="zoom:40%">


### 6 分段配速
组织者给整个赛道分成九段：

![sections](http://wx4.sinaimg.cn/large/007BDy7nly1fziwqooscgj31jl093dkj.jpg)

其中，Hill Climb（1.5km）是一段上坡。由于最后的Finish（2.2km）多加了从枪响到芯片通过起点开始计时的时间，这里做了下处理，Finish段的实际配速为：

$$
\begin{eqnarray*}
Pace_{real}&=&Pace_{recorded}-(Pace_{Gun\,average}-Pace_{Chip\,average})\times\frac{Distance_{Total}}{Distance_{Finish}}\\
& = & Pace_{recorded}-(Pace_{Gun\,average}-Pace_{Chip\,average})\times\frac{42.2}{2.2}.
\end{eqnarray*}
$$



取前20名成绩，及完赛时长从3:00到5:30，每30min取十名选手成绩，绘图如下。
发现几乎所有人在爬坡（Hill Climb）的1.5km变快，很奇怪，是官方计算不准，还是大家都加快了呢？

第一名是实力跑将，全程配速均匀，第二、三名到最后几公里配速浮动有点大。4~20名，以及完赛时长3:00的选手全程配速都较均匀，3:30及以后的选手起伏较大，尤其是后半程。其中图中有两名选手，前半段直逼330，半途估计抽筋了，配速掉到10min/km，忍痛完赛，一定要注意安全。

<img src="http://wx1.sinaimg.cn/large/007BDy7nly1fziwqtqiqaj30xm0lw0zs.jpg"  style="zoom:50%">

### 7 团队排名
报名时有组队，然而最后并没有像Sun Run那样统计团队成绩，本文顺便把这事做了~

本次共有171个团队参加比赛，其中91个团队成员只有一人，不能算作团队，下图为成员人数在3人以上的团队，按成员人数由多到少排名，上部分为平均完赛成绩，最快和最慢成绩，下部分为成员人数。

我们加拿大乐跑俱乐部所组的团队LaPower，总数量名列第一，远超其他团队，可为其颁发“最佳组织奖”，平均4h21min，不好意思我给团队拖后腿了。VFAC团队只有四人，平均成绩最佳，且每人成绩相差甚微，可为其颁发“最和谐奖”，

![teams](http://wx2.sinaimg.cn/mw690/007BDy7nly1fzixlog5saj30tv0nl0vr.jpg)

## 总结
- 肯尼亚的选手真是能跑啊~
- 30岁左右是跑马成绩最好的年纪。所以如果你还年轻，只有十几二十几岁，不用担心跑得慢，再跑几年，会越来越好。
- 设定一个目标完赛时间，按照这个时间对应的配速，全程保持配速稳定。
- 但是一有受伤，请停下休息。
- 总之，开心就好~
