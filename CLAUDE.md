# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

这是一个个人笔记项目，使用 Obsidian 管理笔记内容，并通过 Git 子模块方式组织多个相关项目。项目采用动态路径管理，支持在不同代码托管平台（GitHub、Gitee）之间切换。

## 核心架构

### 主要结构
- **根目录**: 主笔记项目，包含 Obsidian 配置和子模块引用
- **blog/**: 技术博客子模块，包含软件开发、AI测试、Git 等技术笔记
- **program/**: 程序开发相关子模块
  - `czuan/`: czuan 开发文档项目
  - `mai-tian-fcd/`: 麦田FCD项目文档
  - `mai-tian-sdtr/`: 麦田SDTR项目文档
- **college-to-undergraduate/**: 本科学习相关内容
  - `math/`: 数学笔记（子模块）
  - `计算机/`: 计算机相关内容
- **english-words/**: 英语单词学习
- **recume--CV/**: 个人简历

### 技术栈
- **笔记管理**: Obsidian (启用了 file-explorer, global-search, daily-notes, templates, sync 等插件)
- **版本控制**: Git with submodules
- **文件夹别名**: 通过 `folder-alias.json` 提供文件夹描述

## 常用命令

### Git 子模块管理
```bash
# 初始化和更新所有子模块
git submodule update --init --recursive

# 同步子模块配置（切换平台后使用）
git submodule sync --recursive

# 更新所有子模块到最新版本
git submodule update --remote --recursive

# 检查子模块状态
git submodule status

# 进入特定子模块目录进行操作
cd blog/ && git status

# 遍历所有子模块执行命令
git submodule foreach 'git remote -v'
```

### 平台切换
```bash
# 切换到 Gitee
git remote set-url origin git@gitee.com:hong-ying-19/honlnk-note-store.git
git submodule sync --recursive

# 切换回 GitHub
git remote set-url origin git@github.com:honlnk/honlnk-note-store.git
git submodule sync --recursive
```

### Obsidian 工作流
- 工作区配置: `.obsidian/workspace.json` 和 `.obsidian/workspace-mobile.json`
- 核心插件: file-explorer, global-search, daily-notes, templates, sync, canvas
- 工作区文件被 .gitignore 排除，保持个人配置私有

## 开发规范

### 提交规范
- 遵循 `blog/dev-standards/code-commit-standards.md` 中定义的代码提交规范
- 相关的提交规范文档也存在于 `program/mai-tian-fcd/代码提交规范.md`

### 文档组织
- 使用 Markdown 格式编写所有文档
- 每个子模块都有独立的 README.md 说明项目用途
- 文件夹别名配置在相应的 `folder-alias.json` 文件中

### 子模块管理注意事项
- 新增子模块需要更新 `.gitmodules` 文件
- 子模块路径使用相对路径（`../repository.git`）以便动态重定向
- 私有文件夹别名在 `private-folder-alias.json` 中配置，当前为空

## 故障排除

### 子模块问题
- 如果子模块 URL 未按预期重写，执行 `git submodule sync --recursive`
- 检查主仓库的远程 URL 设置是否正确
- 使用 `git submodule foreach --recursive 'git remote -v'` 验证配置

### Obsidian 插件问题
- 工作区配置文件（.obsidian/workspace.json）被忽略，不影响版本控制
- 插件配置在 `.obsidian/core-plugins.json` 和 `.obsidian/community-plugins.json` 中

## 项目特色

1. **动态路径管理**: 通过相对路径机制实现跨平台的子模块管理
2. **知识组织**: 使用 Obsidian 强大的链接和图谱功能组织个人知识库
3. **模块化结构**: 通过子模块实现不同主题笔记的独立管理
4. **多平台支持**: 可在 GitHub 和 Gitee 之间无缝切换