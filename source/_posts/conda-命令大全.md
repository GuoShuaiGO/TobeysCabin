---
title: conda 命令大全
date: 2023-01-07 09:52:26
categories: ai
tags: 
      - conda
      - 命令大全
---





下面展示了一些常用conda命令

<!-- more -->



## 链接：

[conda命令大全 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/68578051#:~:text=conda环境使用基本命令： conda update -n base conda %2F%2Fupdate最新版本的conda conda,%2F%2F开启xxxx环境 conda deactivate %2F%2F关闭环境 conda env list %2F%2F显示所有的虚拟环境)



[[命令\]使用的conda命令大全 - 林间飞鹿 - 博客园 (cnblogs.com)](https://www.cnblogs.com/ljfl-study/p/12129853.html)



[conda | 创建环境、安装包、删除环境步骤_Begonia_cat的博客-CSDN博客_conda 删除环境](https://blog.csdn.net/qq_44250700/article/details/125348008)

## 我常用命令

**<>中为自己填的东西，  [] 为选填**

- 查看conda版本

  ```bash
  conda -V/--version
  ```

- 查看所有环境

  ```bash
  conda info --env
  ```

- 创建虚拟环境

  ```bash
  conda create -n <name> [python=xxx]
  ```

- 激活环境

  ```bash
  conda activate <name>
  ```

- 查看环境下的包版本

  ```bash
  conda list
  ```

- 查看环境下的python版本

  ```bash
  python --version
  ```

- 下载包

  ```bash
  conda install <name>==<1.10.2>
  pip install <name>==<1.10.2>
  pip install -r requirements.txt [-i https://mirrors.aliyun.com/pypi/simple/  或者 -i https://pypi.tuna.tsinghua.edu.cn/simple]
  ```

- 删除包

  ```bash
  conda/pip uninstall <name>==<1.10.2>
  ```

- 退出环境

  ```bash
  conda deactivate 
  ```

- 删除环境

  ```bash
  conda remove -n <name> -all
  ```

  
