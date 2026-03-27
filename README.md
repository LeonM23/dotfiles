# Chezmoi 点文件配置库

这是一份使用 [chezmoi](https://www.chezmoi.io/) 管理的个人点文件 (dotfiles) 配置库。包含了多个操作系统和编程工具的配置文件。

---

## 📋 配置文件总览

| 文件名 | 功能描述 | 适配系统 | 关键作用 |
|--------|--------|--------|--------|
| **dot_bash_profile** | Bash 初始化配置 | macOS, Linux | 登录 shell 启动时加载环境变量，配置 Conda、Homebrew 镜像 |
| **dot_bashrc** | Bash 交互配置 | macOS, Linux | 定义别名、导出环境变量 (Git、文件操作等) |
| **dot_zshrc** | Zsh Shell 主配置 | macOS, Linux | 配置 Zsh 主题 (Powerlevel10k)、加载插件、设置 Oh My Zsh 框架 |
| **dot_zshrc.pre-oh-my-zsh** | Zsh 旧版配置 | macOS (历史版本) | 转换到 Oh My Zsh 之前的 Zsh 设置，包含 Conda 初始化 |
| **executable_dot_zprofile** | Zsh 初始化文件 | macOS | 登录 shell 启动时加载，初始化 Homebrew、调用 .zshrc |
| **dot_gitconfig.tmpl** | Git 全局配置 (模板化) | Windows, macOS, Linux | 根据操作系统自动调整换行符处理和凭据存储；定义用户信息、分支配置 |
| **dot_vimrc** | Vim/Neovim 配置 | macOS, Linux, Windows | 配置 Vim 编辑器的键盘映射、快捷方式、基础设置 |
| **dot_ideavimrc** | IdeaVim 配置 | 跨平台 (JetBrains IDE) | 为 IntelliJ IDEA 等 IDE 配置 Vim 模拟模式的快捷键 |
| **dot_tmux.conf** | Tmux 窗口管理器配置 | macOS, Linux | 配置 Tmux 前缀键、窗口分割、插件 (resurrect、continuum、vim-navigator) |
| **dot_condarc.tmpl** | Conda 包管理器配置 (模板化) | 所有使用 Anaconda/Miniconda 的系统 | 根据操作系统自动设置环境/包存储路径；配置下载镜像 (清华镜像) |
| **dot_p10k.zsh** | Powerlevel10k 主题配置 | macOS, Linux (Zsh) | 配置 Powerlevel10k 提示符主题的外观和元素 |
| **theme.omp.json** | Oh My Posh 主题配置 | Windows PowerShell, 跨平台 | 配置 PowerShell 提示符的颜色、字体、显示元素 |
| **AppData/Roaming/pip/pip.ini** | Python pip 配置 (Windows) | Windows | 配置 pip 软件包管理器的下载镜像 (清华镜像) |
| **dot_pip/pip.config** | Python pip 配置 (Unix) | Linux, macOS | 配置 pip 软件包管理器的下载镜像 (清华镜像) |

---

## 🔧 主要工具和依赖

### Shell 环境

- **Bash**: macOS 旧版默认 shell
- **Zsh**: macOS Catalina+ 默认 shell
- **Oh My Zsh**: Zsh 框架，提供插件和主题支持
- **Powerlevel10k**: Zsh 主题，提供美观的提示符

### 编辑器和 IDE

- **Vim/Neovim**: 高效的文本编辑器 (.vimrc 配置)
- **JetBrains IDE** (IntelliJ IDEA, PyCharm 等): 支持 IdeaVim 插件进行 Vim 模拟
- **Oh My Posh**: PowerShell 主题引擎

### 窗口管理和终端

- **Tmux**: 终端多路复用器，支持会话管理、插件系统
- **tmux-resurrect**: Tmux 会话持久化插件
- **tmux-continuum**: 自动保存 Tmux 会话插件
- **vim-tmux-navigator**: Vim 与 Tmux 窗口导航插件

### 包管理器

- **Homebrew**: macOS 包管理器 (配置了国内镜像)
- **Conda/Anaconda/Miniconda**: Python 环境和包管理 (配置了清华镜像)
- **pip**: Python 包管理器 (配置了清华镜像)

---

## 📚 Zsh 插件列表

在 `dot_zshrc` 中加载的主要插件:

| 插件 | 功能 |
|------|------|
| **git** | Git 命令缩写和增强 |
| **colored-man-pages** | 彩色 man 手册页 |
| **colorize** | 命令输出彩色化 |
| **cp** | 增强的 cp 命令 |
| **man** | 改进的 man 手册支持 |
| **command-not-found** | 命令未找到时建议安装 |
| **sudo** | 快速 sudo 命令前缀 |
| **ubuntu / archlinux** | 系统特定命令快捷方式 |
| **zsh-navigation-tools** | 目录导航工具 |
| **z** | 快速目录跳转 |
| **extract** | 自动提取压缩文件 |
| **history-substring-search** | 历史命令子字符串搜索 |
| **python** | Python 相关快捷方式 |
| **zsh-syntax-highlighting** | 命令语法高亮 |
| **zsh-autosuggestions** | 命令自动补全建议 |
| **autojump** | 智能目录跳转 |

---

## 🚀 快速开始

### 1. 安装 chezmoi
```bash
# macOS
brew install chezmoi

# Linux
sh -c "$(curl -fsLS chezmoi.io/get)" -- -b ~/.local/bin

# Windows (PowerShell)
choco install chezmoi
```

### 2. 初始化配置库
```bash
chezmoi init https://github.com/username/dotfiles.git
chezmoi apply
```

### 3. 更新配置
```bash
# 编辑配置后
chezmoi add ~/.bashrc
chezmoi add ~/.zshrc
# ... 其他文件

# 提交和推送
chezmoi cd
git add .
git commit -m "Update configuration"
git push
```

---

## 🎯 模板化配置 (Chezmoi Templates)

某些配置文件采用 **Chezmoi 模板**方式编写 (`.tmpl` 后缀)，能够根据操作系统、用户等变量自动调整配置。

### dot_gitconfig.tmpl - 跨平台 Git 配置

这是一个根据操作系统自动调整的模板文件:

```ini
[core]
    autocrlf = {{ if eq .chezmoi.os "windows" }}true{{ else }}input{{ end }}
```

**自动行为**:
- **Windows**: `autocrlf = true` - 自动处理 CRLF/LF 转换
- **Linux/macOS**: `autocrlf = input` - 仅在提交时转换 CRLF → LF

**Windows 特定配置**:
```ini
[credential]
    helper = manager-core
```
在 Windows 上使用系统凭据管理器存储 Git 凭据。

### dot_condarc.tmpl - 跨平台 Conda 环境配置

这个模板根据操作系统自动配置 Conda 虚拟环境和包缓存的存储位置，解决 Windows 和 Linux/macOS 路径差异的问题。

**问题背景**:
- 在 Windows 和 WSL/Linux 上同时使用 Conda 时，需要不同的存储路径
- **Windows**: 将环境和包存放在 D 盘（数据分区），避免占用 C 盘（系统盘）空间
- **Linux/macOS**: 环境和包存放在用户主目录下 (`~/.conda/`)

**自动配置**:

**在 Windows 上**:
```yaml
envs_dirs:
  - D:\Conda\envs                  # 量化研究环境存放位置
  - %USERPROFILE%\AppData\Local\miniconda3\envs  # Miniconda 备选

pkgs_dirs:
  - D:\Conda\pkgs                  # 包缓存（优化 C 盘空间）
  - %USERPROFILE%\AppData\Local\miniconda3\pkgs  # Miniconda 备选
```

**在 Linux/macOS 上**:
```yaml
envs_dirs:
  - ~/.conda/envs                  # Conda 标准路径
  - ~/miniconda3/envs              # Miniconda 备选

pkgs_dirs:
  - ~/.conda/pkgs                  # Conda 标准路径
  - ~/miniconda3/pkgs              # Miniconda 备选
```

**关键优势**:
- ✅ **自动化**: 跨系统自动选择合适的路径，无需手工修改
- ✅ **性能优化**: Windows 下使用 D 盘缓存，保护 C 盘系统分区
- ✅ **一致性**: 统一的配置管理，易于维护和同步
- ✅ **灵活扩展**: 支持多个备选路径，适应不同安装方式

**自定义路径**:
编辑 `dot_condarc.tmpl` 修改存储位置 (例如改为其他驱动器或目录):
```yaml
{{ if eq .chezmoi.os "windows" }}
envs_dirs:
  - E:\MyEnvs                      # 改为 E 盘
{{ end }}
```

📖 **详细指南**: 参考 [CONDA_PATHS_GUIDE.md](CONDA_PATHS_GUIDE.md) 了解更多配置选项、常见场景和故障排查。

---

## ⚙️ 配置说明

### 镜像配置
本配置库使用了多个国内镜像来加快软件包下载 (主要针对中国用户):

- **Homebrew**: 清华大学镜像 `https://mirrors.tuna.tsinghua.edu.cn/`
- **Conda**: 清华大学镜像 `https://mirrors.tuna.tsinghua.edu.cn/anaconda/`
- **pip**: 清华大学镜像 `https://pypi.tuna.tsinghua.edu.cn/simple`

### Vim 快捷键
- Leader 键: 空格
- 窗口导航: `<Ctrl-h/j/k/l>` 或 `<Leader>w[hjkl]`
- 缓冲区导航: `<Shift-h/l>` 或 `<Leader>b[hl]`
- 缩进操作: `<Tab>` / `<Shift-Tab>`

### Tmux 快捷键
- 前缀键: `<Ctrl-a>` (代替默认的 `<Ctrl-b>`)
- 水平分割: `<Prefix>|`
- 竖直分割: `<Prefix>-`
- 窗口调整: `<Prefix>hjkl` (调整大小)
- 最大化窗口: `<Prefix>m`

### Git 别名 (来自 dot_bashrc)
```bash
gs  = git status
ga  = git add
gc  = git commit -m
```

---

## 📝 特殊配置

### RiceQuant 交易平台
某些配置文件中包含了 RiceQuant 量化交易平台的许可证配置
- `RQSDK_LICENSE`: RQSDK 许可证 (数据获取)
- `RQDATAC_CONF`: RQDATAC 配置 (实时数据)

---

## 🔄 定期维护

建议定期检查和更新:
1. **Zsh 插件**: 通过 `oh-my-zsh update` 更新
2. **Tmux 插件**: 使用 `~/.tmux/plugins/tpm/bin/update_plugins`
3. **主题**: 检查 Powerlevel10k 和 Oh My Posh 的更新

---

## 📄 许可证

这个点文件配置库可按需自由使用和修改。

---

## 💡 说明

- `executable_` 前缀的文件表示可执行文件
- `dot_` 前缀的文件在部署时会自动转换为 `.` 前缀 (chezmoi 约定)
- 所有配置文件都包含详细的中文注释，方便理解和修改
