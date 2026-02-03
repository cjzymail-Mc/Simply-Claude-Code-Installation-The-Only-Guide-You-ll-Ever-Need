# Python 虚拟环境 (.venv) 实战精华笔记

## 📌 核心概念
- **虚拟环境作用**：为每个项目创建独立的 Python 包环境，避免依赖冲突
- **行业惯例**：虚拟环境统一命名为 `.venv`（前面的点表示隐藏文件夹）
- **重要提醒**：每次新开 PowerShell 窗口，默认都是全局环境，需要手动激活或指定路径

---

## ⭐ 最常用操作（日常开发 TOP 5）

### 1. 快速启动项目（三步走）
```powershell
# 步骤 1：进入项目目录
cd "D:\你的项目目录"

# 步骤 2：激活虚拟环境
.\.venv\Scripts\Activate.ps1

# 步骤 3：运行代码
python .\your_script.py
```

### 2. Claude Code 在虚拟环境中运行
```powershell
# 方法 1：激活后运行（推荐）
cd "D:\你的项目目录"
.\.venv\Scripts\Activate.ps1
claude                    # 或 claude --resume 继续之前的任务

# 方法 2：不激活直接运行
cd "D:\你的项目目录"
& ".\.venv\Scripts\python.exe" -m claude
```

### 3. 安装新的依赖包
```powershell
# 方法 A（推荐）：不激活，直接指定环境
& ".\.venv\Scripts\python.exe" -m pip install 包名

# 方法 B：激活后安装
.\.venv\Scripts\Activate.ps1
pip install 包名

# 批量安装（从 requirements.txt）
& ".\.venv\Scripts\python.exe" -m pip install -r requirements.txt
```

### 4. 检查当前使用的 Python 环境
```powershell
# 方法 1：查看 Python 路径
where python

# 方法 2：查看完整路径（更准确）
python -c "import sys; print(sys.executable)"

# 方法 3：查看已安装的包
pip list
```

### 5. 退出虚拟环境
```powershell
deactivate    # 返回上一个环境（不一定是全局！）
```

---

## 🔧 初始化新项目（只做一次）

### 步骤 1：创建虚拟环境
```powershell
# 进入项目目录
cd "D:\你的项目目录"

# 创建虚拟环境（统一命名为 .venv）
py -m venv .venv

# 或自定义名称（不推荐，除非有特殊需求）
py -m venv custom_env_name
```

### 步骤 2：准备依赖清单
```powershell
# 手动创建 requirements.txt 文件，内容示例：
# requests==2.31.0
# pandas>=2.1.0
# opencv-python
# pillow
# python-docx

# 批量安装所有依赖
& ".\.venv\Scripts\python.exe" -m pip install -r requirements.txt
```

### 步骤 3：导出当前环境的依赖
```powershell
# 导出到当前项目（推荐）
& ".\.venv\Scripts\python.exe" -m pip freeze > ".\requirements.txt"

# 全局环境导出（不推荐，会包含所有全局包）
pip freeze > requirements.txt
```

---

## 📂 项目迁移/克隆（迁移到新电脑）

### 在原电脑导出依赖
```powershell
cd "D:\原项目目录"
& ".\.venv\Scripts\python.exe" -m pip freeze > ".\requirements.txt"
# 将 requirements.txt 和代码一起复制到新电脑
```

### 在新电脑重建环境
```powershell
cd "D:\新项目目录"
py -m venv .venv
& ".\.venv\Scripts\python.exe" -m pip install -r requirements.txt
```

---

## 🚀 高级技巧

### 1. 用 IDLE 编辑器打开（带虚拟环境）
```powershell
cd "文件目录"
& ".\.venv\Scripts\python.exe" -m idlelib ".\your_script.py"
```

### 2. 完整路径运行（不用 cd 进目录）
```powershell
# 运行脚本
& "D:\project2\.venv\Scripts\python.exe" "D:\project2\main.py"

# 安装包
& "D:\project2\.venv\Scripts\python.exe" -m pip install requests
```

### 3. 升级 pip 到最新版本
```powershell
& ".\.venv\Scripts\python.exe" -m pip install --upgrade pip
```

### 4. 查看包的详细信息
```powershell
& ".\.venv\Scripts\python.exe" -m pip show 包名
```

### 5. 卸载包
```powershell
& ".\.venv\Scripts\python.exe" -m pip uninstall 包名
```

---

## ⚠️ 常见问题排查

### 问题 1：PowerShell 提示无法运行脚本
**错误信息**：`无法加载文件 Activate.ps1，因为在此系统上禁止运行脚本`

**解决方案**：
```powershell
# 以管理员身份运行 PowerShell，执行：
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

# 然后重新激活环境
.\.venv\Scripts\Activate.ps1
```

### 问题 2：pip 安装包速度慢
**解决方案**：使用国内镜像源
```powershell
# 临时使用
& ".\.venv\Scripts\python.exe" -m pip install 包名 -i https://pypi.tuna.tsinghua.edu.cn/simple

# 永久配置（创建 pip.ini 文件）
# 位置：C:\Users\你的用户名\pip\pip.ini
# 内容：
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

### 问题 3：虚拟环境被意外修改
**场景**：文件同步软件（OneDrive、Dropbox）同步了 `.venv` 文件夹导致环境损坏

**解决方案**：
```powershell
# 1. 删除旧的虚拟环境
Remove-Item -Recurse -Force .\.venv

# 2. 重新创建
py -m venv .venv

# 3. 重新安装依赖
& ".\.venv\Scripts\python.exe" -m pip install -r requirements.txt

# 4. 配置 .gitignore（如果使用 Git）
# 添加这行：.venv/
```

### 问题 4：找不到模块（ModuleNotFoundError）
**检查步骤**：
```powershell
# 1. 确认当前使用的 Python 路径
python -c "import sys; print(sys.executable)"

# 2. 检查包是否安装在虚拟环境中
& ".\.venv\Scripts\python.exe" -m pip list

# 3. 如果没有，重新安装
& ".\.venv\Scripts\python.exe" -m pip install 缺失的包名
```

---

## 📋 最佳实践 Checklist

- [ ] ✅ 每个项目都创建独立的 `.venv`
- [ ] ✅ `.venv` 加入 `.gitignore`（不要上传到版本控制）
- [ ] ✅ 提交代码时包含 `requirements.txt`
- [ ] ✅ 使用 `& ".\.venv\Scripts\python.exe"` 而不是全局 `python`
- [ ] ✅ 定期导出依赖：`pip freeze > requirements.txt`
- [ ] ✅ 项目文档中说明 Python 版本要求（如 Python 3.9+）
- [ ] ⚠️ 不要在虚拟环境内再创建虚拟环境
- [ ] ⚠️ 不要手动修改 `.venv` 内的文件

---

## 🎯 快速参考表

| 操作 | 命令 | 说明 |
|------|------|------|
| 创建环境 | `py -m venv .venv` | 只需执行一次 |
| 激活环境 | `.\.venv\Scripts\Activate.ps1` | 每次新开窗口需要 |
| 退出环境 | `deactivate` | 返回上一个环境 |
| 安装单个包 | `& ".\.venv\Scripts\python.exe" -m pip install 包名` | 推荐用完整路径 |
| 批量安装 | `& ".\.venv\Scripts\python.exe" -m pip install -r requirements.txt` | - |
| 导出依赖 | `& ".\.venv\Scripts\python.exe" -m pip freeze > requirements.txt` | 迁移项目前必做 |
| 运行脚本 | `& ".\.venv\Scripts\python.exe" ".\script.py"` | 不激活也能运行 |
| 检查环境 | `python -c "import sys; print(sys.executable)"` | 确认用对环境 |
| 查看已装包 | `& ".\.venv\Scripts\python.exe" -m pip list` | - |
| 升级 pip | `& ".\.venv\Scripts\python.exe" -m pip install --upgrade pip` | 首次创建后建议执行 |

---

## 💡 Pro Tips

1. **别名设置**（可选，提高效率）
```powershell
# 在 PowerShell 配置文件中添加别名
# 文件位置：$PROFILE（输入这个命令查看路径）

function venv-activate { .\.venv\Scripts\Activate.ps1 }
Set-Alias va venv-activate

function venv-python { & ".\.venv\Scripts\python.exe" $args }
Set-Alias vpy venv-python
```

2. **项目模板**（新项目快速启动）
```powershell
# 创建标准项目结构
mkdir MyProject
cd MyProject
py -m venv .venv
New-Item requirements.txt
New-Item README.md
New-Item .gitignore
mkdir src
mkdir tests
```

3. **多 Python 版本管理**
```powershell
# 指定 Python 版本创建虚拟环境
py -3.9 -m venv .venv_py39
py -3.11 -m venv .venv_py311

# 查看系统安装的所有 Python 版本
py --list
```

---

## 📚 延伸阅读

- **为什么不用全局安装？**  
  避免不同项目的包版本冲突，例如项目 A 需要 requests 2.25，项目 B 需要 requests 2.31

- **虚拟环境占用空间大吗？**  
  通常 100-500MB，取决于安装的包数量。可以用 `du -sh .venv`（Linux/Mac）或资源管理器查看

- **可以移动虚拟环境文件夹吗？**  
  不推荐！虚拟环境内部使用绝对路径。移动后需要重新创建

- **requirements.txt 的进阶用法**
  ```txt
  # 指定版本
  requests==2.31.0
  
  # 版本范围
  pandas>=2.0.0,<3.0.0
  
  # 从 Git 仓库安装
  git+https://github.com/user/repo.git@main
  
  # 本地包
  -e ./local_package
  ```

---

**最后更新**：2026-01-15  
**适用系统**：Windows PowerShell  
**Python 版本**：3.7+
