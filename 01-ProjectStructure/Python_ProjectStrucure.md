---
Author: liuyangly1
Date  : 2021-07-06 18:53:47
Blog  : https://blog.csdn.net/liuyang_1106
Github: https://github.com/liuyangly1
Email : 522927317@qq.com
---

[toc]

# 项目结构

## 1. 项目结构目录

```text
ProjectName
|-- bin/                    # 存放脚本，执行文件
|   |-- projectname
|   |-- script
|
|-- packages/
|   |-- lib1                # 存放库文件
|
|-- configure               # 配置文档
|   |--seetting.py       
|
|-- projectname/            # 存放项目的所有源代码，包括所有模块和包
|   |-- tests/              # 存放单元测试代码
|   |   |-- __init__.py
|   |   |-- test_main.py
|   |
|   |-- __init__.py
|   |-- main.py             # 程序的入口
|
|-- docs/                   # 文档
|   |-- doc1.md
|   |-- doc2.word
|
|-- logs/                   # 日志文件
|   |-- logs.txt
|
|-- setup.py                # 安装、部署、打包的脚本
|-- requirements.txt        # 存放软件依赖的外部Python包列表
|-- README                  # 项目说明文档
```
- 开源项目还涉及LICENSE.txt,ChangeLog.txt文件等。
- 数据文件夹data等。

## 2. 项目生成脚本python-script.py

```python
#!/usr/bin/env python
# -*- encoding: utf-8 -*-
'''
-------------------------------------------
@File    :   project_structure.py
@Time    :   2020/08/24 11:19:37
@Author  :   liuyangly1
@Version :   1.0
@Contact :   522927317@qq.com
@Desc    :   A python project structure.
            ProjectName
                |-- bin/                    # 存放脚本，执行文件
                |   |-- projectname
                |
                |-- projectname/            # 存放项目的所有源代码，包括所有模块和包
                |   |-- tests/              # 存放单元测试代码
                |   |   |-- __init__.py
                |   |   |-- test_main.py
                |   |
                |   |-- __init__.py
                |   |-- main.py             # 程序的入口
                |
                |-- docs/                   # 文档
                |   |-- abc.rst
                |
                |-- conf/                   # 配置
                |   |-- settings.py
                |
                |-- logs/                   # 日志
                |   |-- logs.txt
                |
                |-- setup.py                # 安装、部署、打包的脚本
                |-- requirements.txt        # 存放软件依赖的外部Python包列表
                |-- README 
-------------------------------------------
'''
import os
import argparse

def project_structure(project_path, project_name):

    assert not os.path.exists(os.path.join(project_path, project_name)), "Error, project_name exist!"
    # 创建项目目录
    os.makedirs(os.path.join(project_path, project_name))
    # 创建执行目录
    os.mkdir(os.path.join(project_path, project_name, "bin"))
    fp = open(os.path.join(project_path, project_name, "bin", "run"),'w')
    fp.close()
    # 创建源代码目录
    os.mkdir(os.path.join(project_path, project_name, project_name.lower()))
    fp = open(os.path.join(project_path, project_name, project_name.lower(), "__init__.py"),'w')
    fp.close()
    # 创建程序入口文件
    fp = open(os.path.join(project_path, project_name, project_name.lower(), "main.py"),'w')
    fp.close()
	#  创建测试目录
    os.mkdir(os.path.join(project_path, project_name, project_name.lower(), "tests"))

    fp = open(os.path.join(project_path, project_name, project_name.lower(), "tests", "__init__.py"),'w')
    fp.close()
    fp = open(os.path.join(project_path, project_name, project_name.lower(), "tests", "test_main.py"),'w')
    fp.close()
    # 创建文档目录
    os.mkdir(os.path.join(project_path, project_name,"docs"))
    fp = open(os.path.join(project_path, project_name,"docs","conf.py"),'w')
    fp.close()
    # 创建配置文件目录
    os.mkdir(os.path.join(project_path, project_name,"conf"))
    fp = open(os.path.join(project_path, project_name,"conf","settings.py"),'w')
    fp.close()
    # 创建日志目录
    os.mkdir(os.path.join(project_path, project_name,"logs"))
    fp = open(os.path.join(project_path, project_name,"logs","logs.txt"),'w')
    fp.close()
    # 创建setup.py, requirements.txt and README文件
    fp = open(os.path.join(project_path, project_name,"setup.py"),'w')
    fp.close()
    fp = open(os.path.join(project_path, project_name,"requirements.txt"),'w')
    fp.close()
    fp = open(os.path.join(project_path, project_name,"README.md"),'w')
    fp.close()

def parse_args():
    parser = argparse.ArgumentParser(description="A python project structure")
    # 向该对象中添加你要关注的命令行参数和选项
    parser.add_argument("--project_path", type=str, default=".", help='Required parameters')
    parser.add_argument("--project_name", type=str, default="ProjectName", help='Required parameters')
    return parser.parse_args()

def main():
    project_structure(**vars(parse_args()))

if __name__ == "__main__":
    main()
```