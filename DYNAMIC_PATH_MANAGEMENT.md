# 动态 Git 子模块路径管理配置说明

## 配置说明

本项目使用 Git 的相对路径机制来实现动态的子模块路径管理，允许在不同平台（GitHub、Gitee 等）之间轻松切换，而无需修改 `.gitmodules` 文件。

## 配置文件

1. `.gitmodules` 文件现在使用相对路径：
   - `../mathnotes-shadow.git`
   - `../maitian---fcd.git`
   - 等等

2. 这样，子模块 URL 将相对于主仓库的 URL 进行解析：
   - 当主仓库为 `git@github.com:honlnk/honlnk-note-store.git` 时
   - 子模块 `../honlnk-blog.git` 将解析为 `git@github.com:honlnk/honlnk-blog.git`
   - 子模块 `../mathnotes-shadow.git` 将解析为 `git@github.com:honlnk/mathnotes-shadow.git`

## 如何切换到不同的平台

### 切换到 Gitee
```bash
# 修改主仓库的远程 URL
git remote set-url origin git@gitee.com:hong-ying-19/honlnk-note-store.git

# 同步子模块配置
git submodule sync --recursive
```

### 切换回 GitHub
```bash
# 恢复主仓库的远程 URL
git remote set-url origin git@github.com:honlnk/honlnk-note-store.git

# 同步子模块配置
git submodule sync --recursive
```

## 使用场景

1. **迁移仓库**：只需修改主仓库的远程 URL，子模块会自动适应
2. **多平台开发**：不同开发者可根据需要使用不同的主仓库 URL
3. **环境切换**：在不同环境（开发/测试/生产）之间切换仓库源

## 注意事项

- 使用 `git submodule sync --recursive` 命令来同步所有子模块的 URL 重写
- 此配置是基于 SSH URL 格式，适用于 GitHub、Gitee 等代码托管平台
- 相对路径中的 `..` 表示向上一级，即从主仓库名切换到用户名级别

## 验证与故障排除

### 验证配置是否生效
1. 检查子模块的远程 URL：
   ```bash
   git submodule foreach --recursive 'git remote -v'
   ```
   确认子模块的远程 URL 按预期格式显示

2. 查看特定子模块的状态：
   ```bash
   cd <submodule-path>
   git remote -v
   ```

### 故障排除
- 如果子模块 URL 没有按预期重写，请确保执行了 `git submodule sync --recursive`
- 验证主仓库的远程 URL 设置是否正确
- 确保网络连接正常，能够访问目标 Git 服务器