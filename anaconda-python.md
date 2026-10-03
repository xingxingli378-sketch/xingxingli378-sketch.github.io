从零开始配置 Jupyter + Python

阅读指引
- 零基础读者：建议全文循序阅读学习
- 具备基础环境认知：可直接从第二章开始阅读

一、实操内容总览
本文基于 Windows 平台，完整完成 AI 入门必备环境搭建与工具配置：
1. 电脑硬件适配性自查，确认零基础 AI 学习设备标准
2. 梳理 Python、Anaconda、Jupyter、VSCode 四大工具的定位与协作逻辑
3. 安装配置完整版 Anaconda，完成环境初始化校验
4. 创建独立虚拟环境 `env`，配置 `Python3.13` 版本，安装 AI 核心依赖库
5. 配置 Jupyter Notebook，绑定虚拟环境内核，调试 ipynb 实验文件
6. 部署 VSCode 开发环境，解决虚拟环境识别异常等高频问题

二、核心工具作用与关联逻辑
1. Python
人工智能、数据分析、模型训练的核心底层语言，所有主流 AI 框架均基于 Python 开发。
本次不安装系统原生 Python，全程依托 Anaconda 虚拟环境统一管理版本，从根源规避版本冲突。

2. Anaconda
一站式环境管理与包管理工具，是 AI 开发的行业标准工具。
- 支持创建多套隔离虚拟环境，实现项目环境互不干扰
- 自带海量常用 AI 库与 Jupyter 工具，开箱即用、配置简单

3. Jupyter Notebook
Anaconda 内置交互式开发工具，主打碎片化代码调试、小型实验验证、学习笔记记录，适合零基础语法练习与代码试错。

4. VSCode
专业工程化代码编辑器，弥补 Jupyter 无法做项目开发的短板，支持断点调试、文件管理、批量代码开发，适配进阶 AI 项目实操。

工具协作流程
Anaconda 创建独立虚拟环境 → 配置 Python3.13 与依赖库 → Jupyter 碎片化实验调试 → VSCode 规范化项目开发

三、全套环境实操搭建流程
1. 安装完整版 Anaconda
1. 官网下载 Windows 64 位完整版 Anaconda
2. 自定义非 C 盘安装路径，路径无中文、无空格
3. 默认勾选核心组件，安装完成后打开 Anaconda Prompt

环境验证
```bash
# 查看 conda 版本，验证安装成功
conda --version
```

2. 创建专属虚拟环境
统一环境标准：环境名 `env`，Python 版本 `3.13`

 创建虚拟环境
```bash
# 创建名为 env、Python3.13 的独立虚拟环境
conda create -n env python=3.13
```

激活虚拟环境
```bash
激活 env 环境
conda activate env
```

常用环境管理指令
```bash
# 查看所有虚拟环境
conda env list

# 退出当前虚拟环境
conda deactivate

# 删除指定虚拟环境
conda remove -n 环境名 --all
```

安装 AI 核心依赖库
```bash
# 批量安装数据分析、可视化、Jupyter 必备库
pip install numpy pandas matplotlib jupyter
```

3. VSCode 基础配置
1. 安装官方纯净版 VSCode
2. 安装 Microsoft 官方插件：`Python`、`Jupyter`
3. `Ctrl+Shift+P` → `Python: Select Interpreter`，选中 `env` 虚拟环境解释器

在配置vscode的过程中我遇到了虚拟环境始终无法选中的问题，如果你也遇到这类问题，可以试试以下方法：


1. 查看 Python 插件日志
打开插件输出日志，看到 Python-envs 扩展信息，配置项`workspaceFolderValue`、`workspaceValue`都是 undefined，代表**工作区没有指定环境管理器**，默认使用 venv，不会自动扫描 conda 环境。
2. 确认虚拟环境本身有效
在终端用命令查看 conda 环境、环境内 Python 版本，验证 conda 环境本身创建正常、能在命令行激活，排除环境损坏。
3. 核心修复操作
   - 方式 1：在 VSCode 设置里，配置 Python 插件，开启 Conda 环境扫描；修改`python.condaPath`，指定 conda 可执行文件路径，让插件找到 conda。
   - 方式 2：手动选择解释器：`Ctrl+Shift+P` → Python: Select Interpreter → 手动找到 conda 环境下的 python 可执行文件（不用等插件自动列出）。
   - 方式 3：检查插件版本：Python 插件新版本存在 bug，必要时降级 Python 扩展版本。
4. 辅助检查项
   - 确认当前终端 shell 识别 conda（初始化 conda，不然 VSCode 内嵌终端看不到 conda）
   - 检查工作区`.vscode/settings.json`，删掉冲突的旧 python 路径配置
   - 重启 VSCode、重载窗口，使配置生效


四、工具使用与切换逻辑
1. Jupyter Notebook 实操（初期学习）
适合零基础入门调试、分段代码练习、记录实验过程。

启动指令
```bash
# 在 env 环境下启动 jupyter
jupyter notebook
```

环境测试代码
```python
# -*- coding: utf-8 -*-
# 虚拟环境适配测试

print("Anaconda env 虚拟环境配置成功")

核心库可用性测试
import numpy as np
arr = np.array([1,2,3,4,5])
print("Numpy 数组测试结果：", arr)
```

#### 常用操作
- `Shift + Enter`：运行当前代码单元格
- 支持切换代码 / Markdown 模式，边调试边记录笔记

### 2. 切换 VSCode 的核心原因
随着学习深入，Jupyter 无法满足进阶需求，因此切换 VSCode 作为主力工具：
1. 无工程化能力，仅支持单文件零散调试，无法管理多文件项目
2. 不支持断点调试，复杂代码报错难以定位
3. 依赖浏览器运行，操作割裂，不适合长期项目开发
4. 扩展性弱，无法适配深度学习、模型部署等进阶场景

## 六、VSCode 虚拟环境识别异常 完整解决方案
### 问题现象
电脑**未安装原生 Python**，仅使用 Anaconda 虚拟环境；VSCode 重启后自动丢失 `env` 环境，无法识别库、无可用解释器、代码报错。

### 问题根源
VSCode 默认优先检索系统原生 Python，无原生 Python 时缓存极易失效；Anaconda 虚拟环境路径未写入全局变量，重启后无法自动识别。

### 分步标准化解决方案
#### 1. 查看虚拟环境完整路径
```bash
where python
```

#### 2. 最优修复：终端继承环境启动 VSCode
```bash
conda activate env
code .
```

#### 3. 清除 VSCode 失效缓存
`Ctrl+Shift+P` 输入：
```
Python: Clear Editor Cache
```
清除缓存后重启 VSCode。

#### 4. 彻底根治
手动复制 `env` 环境 Python 完整路径，在 VSCode 解释器选择界面手动锁定，永久固定环境。

## 七、AI 循序渐进学习路线
基于纯净 `env` 虚拟环境，聚焦刚需知识点：

### 第一阶段：Python 核心语法
变量类型、运算符、数据容器、分支循环、自定义函数、模块导入

### 第二阶段：三大核心 AI 库
- Numpy：数组运算、维度处理、矩阵操作
- Pandas：数据读取、清洗、筛选、规整
- Matplotlib：数据可视化绘图

### 第三阶段：进阶 AI 实操
- 机器学习：Sklearn 数据集划分、传统模型训练与验证
- 深度学习：PyTorch 环境配置、基础神经网络搭建

## 八、实操避坑总结
1. 全程使用 Anaconda 虚拟环境，不安装系统原生 Python，杜绝版本冲突
2. 拒绝 base 默认环境，所有开发基于独立 `env` 环境，保持环境干净隔离
3. 统一使用 Python3.13 版本，保证库版本兼容
4. 定期清理冗余依赖，避免环境臃肿
5. Jupyter 内核卡死，重启内核或重新激活环境即可修复
