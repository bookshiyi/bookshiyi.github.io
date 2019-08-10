---
title: SLAM技术浅析
url: 1849.html
id: 1849
categories:
  - 建站
tags:
---

  激光slam的经济成本相对较高，但是视角、稳定性有优势，目前无人车的主要难点之一就是激光雷达的价格居高不下。 视觉slam的运算成本相对较高，视角相对较窄，容易受到外界环境干扰（光线等），但是其造价相对较低。 2D激光slam算法： Hector slam 基于最小二乘法匹配扫描点，对扫描角和噪声要求比较高，如使用Kinect建图不推荐使用该算法，适合激光雷达 gmapping 基于粒子滤波的方法， cartographer