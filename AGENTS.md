# Repository Guidelines

本仓库是上游 `rasbt/LLMs-from-scratch` 的中文翻译版本（含笔记与代码）。贡献应以翻译准确性、表达清晰和小范围修复为主，避免会偏离书籍内容的大改动/重构。

## 项目结构与模块组织

- `ch01/` … `ch07/`：各章材料（以 `*.ipynb` 为主，配套 `*.py`）。
  - 主要实现通常在 `chXX/01_main-chapter-code/`（例如 `ch04/01_main-chapter-code/gpt.py`）。
  - 可选/扩展内容通常在 `02_*`、`03_*` 等同级目录。
- `appendix-*/`：附录笔记本与脚本。
- `setup/`：环境搭建说明、Docker/DevContainer、环境检查脚本。
- `imgs/`：文档图片与资源。

## 构建、测试与开发命令

- 使用 conda 创建环境 `llms` 并安装核心依赖：
  - `conda create -n llms python=3.10 -y -c defaults`
  - `conda activate llms`
  - `python -m pip install -r requirements.txt`
- 启动笔记本：`jupyter lab`
- 运行环境检查：`python setup/02_installing-python-libraries/python_environment_check.py`
- 部分目录需要额外依赖（见各自的 `requirements-extra.txt`），例如：`pip install -r ch07/06_user_interface/requirements-extra.txt`

## 代码风格与命名约定

- Python：4 空格缩进，遵循常见 PEP 8 命名（函数/变量 `snake_case`，类 `CapWords`），并尽量与当前章节既有风格保持一致。
- 保持章节目录结构（例如 `ch05/07_gpt_to_llama/...`）与相对导入可用；不要随意挪动文件/重命名入口。
- 不要提交生成物：`.ipynb_checkpoints/`、`.DS_Store`、以及包含大量输出的笔记本。

## 测试指南

- 有测试的地方通常使用 `pytest`（常见为 `tests.py` 或 `tests/test*.py`）。
- 示例：`python -m pytest setup/02_installing-python-libraries/tests.py`
- Llama 转换相关测试：先 `pip install -r ch05/07_gpt_to_llama/tests/test-requirements-extra.txt`，再 `python -m pytest ch05/07_gpt_to_llama/tests`

## Commit 与 Pull Request 指南

- 历史提交信息较随意（常见 `update`、`Update README.md` 等）。新提交建议用“章节 + 动作”的短句，例如：`ch03: 修正翻译错字`、`ch07: 更新说明文档`。
- PR 需说明改动范围，关联 issue/discussion；涉及 UI 或笔记本展示变更时附截图；新增依赖请在描述中说明（指向对应 `requirements(-extra).txt`）。
- 不要提交真实密钥：仓库中的 `config.json` 仅为占位示例；请使用本地私有配置或环境变量（例如 `OPENAI_API_KEY`）。

## 学习建议（面向读者）

> 说明：本节是给学习者的使用建议，不影响仓库代码结构与贡献规范。

### 快速上手（先跑通环境）

- 使用 conda 创建环境 `llms` 并安装依赖：
  - `conda create -n llms python=3.10 -y -c defaults`
  - `conda activate llms`
  - `python -m pip install -r requirements.txt`
- （可选）运行环境检查：`python setup/02_installing-python-libraries/python_environment_check.py`
- 启动 Jupyter：`jupyter lab`

### 推荐学习路径（主线优先）

- 先看 `ch01/README.md`（概览与学习路线，本章无代码）
- 按章节主线跑通：`ch02/01_main-chapter-code/ch02.ipynb` → `ch03/01_main-chapter-code/ch03.ipynb` → `ch04/01_main-chapter-code/ch04.ipynb` → `ch05/01_main-chapter-code/ch05.ipynb` → `ch06/01_main-chapter-code/ch06.ipynb` → `ch07/01_main-chapter-code/ch07.ipynb`
- 需要加餐时再看同章的 `02_*`、`03_*` 等 bonus 目录

### 学习方法（每章通用）

- 先“跑通 notebook”，再对照阅读同目录的 `.py`（通常是把 notebook 逻辑整理成模块/脚本）
- 用“小改动实验”建立直觉：改 `context_length`、`stride`、`batch_size`、学习率等，观察 loss/输出变化
- 有 `tests.py` 的目录用 `pytest` 做自检（例如：`pytest ch04/01_main-chapter-code/tests.py`）
