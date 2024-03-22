---
title: DQN笔记
top: false
cover: false
toc: true
mathjax: false
date: 2023-07-21 20:00:23
tags:
- 算法
- 强化学习
categories:

---

# DQN

DQN两个因素

 DQN 有一个记忆库用于学习之前的经历. 在之前的简介影片中提到过, Q learning 是一种 off-policy 离线学习法, 它能学习当前经历着的, 也能学习过去经历过的, 甚至是学习别人的经历. 所以每次 DQN 更新的时候, 我们都可以随机抽取一些之前的经历进行学习. 随机抽取这种做法打乱了经历之间的相关性, 也使得神经网络更新更有效率. Fixed Q-targets 也是一种打乱相关性的机理, 如果使用 fixed Q-targets, 我们就会在 DQN 中使用到两个结构相同但参数不同的神经网络, 预测 Q 估计 的神经网络具备最新的参数, 而预测 Q 现实 的神经网络使用的参数则是很久以前的. 有了这两种提升手段, DQN 才能在一些游戏中超越人类.

## 2. 程序运行

安装TensorFlow

```bash
 pip3 install tensorflow==1.0.0
```

将脚本中`output_graph=True`设置后

运行

```bash
 tensorboard --logdir=logs
```



