+++
title = "SVO相关问题"
date = 2018-04-03T18:09:01+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Handuo"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Tips"]
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = false

+++

1.  ORBSLAM vs SVO

    * SVO （单目）

        * 优点： 速度极快，100多帧，在低端计算机上也能达到实时性。追踪和建图两个线程，追踪线程和ptam或者orbslam很像，也是建立误差项，然后refine和BA，区别就是用的直接法的Image alignment而不是特征点几何位置信息。

        * 缺点：只是里程计，没有后端优化和回环检测，所以累计误差较大，而且一旦丢了就挂了，没法重定位; 而且在设计的时候针对的是俯视的无人机摄像头，对于平视的摄像机效果很差; 拥有直接法的所有缺点：怕光照变化，怕模糊，怕大运动

    > svo还有一个不是缺点的缺点，它开源的代码有好多好多坑，作者很多私货故意没有写进开源的代码里面，所以实际用的时候有很多问题，需要自己根据情况改进。

    * OrbSLAM
        * 优点：支持单目，双目，RGBD，是一个完整的系统，包含了里程计，特征点建图BA，回环检测三个独立线程，在i7上大概15～20hz（跟输入图像大小以及参数设置有关），精确度在近年来属于比较高的了。综合能力最强。

        * 缺点：ORB的提取以及match耗时较大，过快的旋转可能会丢失。而且因为三个线程会给CPU带来较大负担，基本没办法再跑其他大型算法了。对于场景特征点丰富要求高，某些场景如果没什么特征可能就会失败或者不准确。

    > 能够跟orbslam pk的是比较新的DSO算法，SVO除了速度基本各个方面被吊打。


2.  Depth acquirement


    * 1) 先说svo的深度滤波器，属于渐进式的三维重建，不是单纯的求取keypoint的深度，而是要维护候选点seed的深度分布，从未知到粗略到收敛，收敛了才放到地图中共追踪线程使用。实际上收敛较慢，结果严重依赖于准确的位姿估计，因此相比于特征点法的BA没有什么优势。

    * 2）再说orbslam的BA，相比来说计算量更大，但是因为是frame-frame以及local map的两次优化，精确度应该高于svo的滤波器。


3.  灰度不变性假设

    灰度值不变是很强的假设。如果相机是自动曝光的，当它调整曝光参数时，会使得图像整体变亮或变暗。光照变化时也会出现这种情况。特征点法对光照具有一定的容忍性，而直接法由于计算灰度间的差异，整体灰度变化会破坏灰度不变假设，使算法失败。

    svo不直接取某一个像素，而是4x4的patch，我们对多个点进行最小化光度误差来计算的。所以没有明确的threshold，如果某一两个点光照发生变化还好，少数服从多数。如果发生微小变化了，但是只要选取的特征区域的光照跟其他区域区别很大，也是可以忍受的，毕竟最小化而不强求光照的误差为0。所以说有一定的鲁棒性，虽然跟特征点法没法比。


4.  VO静止的时候，会漂吗

    一般情况下VO一般不会漂的
    如果是VIO的话是有可能的，一般有几个原因:

 * 1) calibration做的不够准

 * 2) 初始化的时候摄像头尽量冲着特征点丰富的地方，并缓慢移动摄像头，充分初始化

 > IMU如果质量不好也会轻微的漂，但是不严重

