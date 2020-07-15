---
layout: post
title:  "Virtual oscilloscope"
date:   2020-06-27 22:14:54
categories: Robot
comments: true
---
*** 读研期间制作的项目 ***

## 虚拟示波器界面
虚拟示波器与真实示波器对比，信号来源于真实示波器的矫正信号<br>
![V-os1](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/Virtual-oscilloscope/Virtual-oscilloscope.gif)

## 转速控制
设置虚拟示波器上的speed值，机器人会相应的调整占空比来控制电机的转速<br>
![I-speed](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/Virtual-oscilloscope/Improve-speed.gif)

## 自主平衡
机器人处于自平衡状态时，虚拟示波器上显示的是机器人的倾角变化，倾角分别由加速度计和陀螺仪通过卡尔曼滤波算法计算后获得，机器人中的控制模块根据倾角的变化，输出相应的力矩使之保持平衡<br>
![I-speed](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/Virtual-oscilloscope/balance.gif)

## 遥感控制机器人运动
虚拟示波器读取摇杆的位置变化，将变化值转化成倾角与速度差，机器人根据以上两者的变化，调整力矩的输出，从而完成机器人的左转、右转、前进、后退等动作。<br>
![move](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/Virtual-oscilloscope/move1.gif)

![move](https://github.com/lbbxsxlz/lbbxsxlz.github.io/raw/master/images/blog/Virtual-oscilloscope/move2.gif)


完整视频见[优酷](https://v.youku.com/v_show/id_XNjAzNzA4MTYw.html)