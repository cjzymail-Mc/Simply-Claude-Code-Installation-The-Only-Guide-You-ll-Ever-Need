# Simply-Claude-Code-Installation-The-Only-Guide-You-ll-Ever-Need
Thank you Grok my best bud~




安装 Claude Code 非常简单，直接在powershell中输入 【irm https://claude.ai/install.ps1 | iex】即可

当然，如果很不幸，你碰到下面和我一样的错误，dont panic  

    PS C:\Users\xy24> irm https://claude.ai/install.ps1 | iex
    Setting up Claude Code...
    Claude Code on Windows requires git-bash (https://git-scm.com/downloads/win). If installed but not in PATH, set environment variable pointing to your bash.exe, similar to:
    CLAUDE_CODE_GIT_BASH_PATH=C:\Program Files\Git\bin\bash.exe 
    
这个提示不是报错，而是在告诉你 Claude Code 在 Windows 上需要 git-bash 才能运行。


那么只能从头开始 ————

------------------------------------------
步骤1：安装 Git for Windows（如果还没安装）
------------------------------------------
      访问 https://git-scm.com/downloads/win 下载并安装 Git for Windows，安装时确保勾选 "Git Bash" 组件。
      
      安装时，有非常多选项 
      choosing the default editor used by git—— 可选 vim / notepad++/visual studio/sublime/vscodium/notepad  我应该选哪个？？？
      1. Visual Studio Code（如果你已安装 VS Code，就选这个）
      2. Notepad（如果你是新手）最简单，Windows 自带 ✅
      ...
      
      
      adjusting the name of the initial branch in new repositories  这个是啥？  我需要let git decide嘛？
      推荐选择：
      ✅ 选择 "Override the default branch name" 并设为 main
      原因：
      与 GitHub、GitLab 等主流平台保持一致
      现代标准做法
      避免后续手动改名的麻烦
      
      
      adjusting your path enviroment :  recommended git from the command line and also from 3rd-party software  选这个嘛？
      2. Git from the command line and also from 3rd-party software
       ✅ 推荐
      ✅ Git Bash、PowerShell、CMD 都能用
      ✅ 其他软件（如 VS Code）也能调用 Git
      ✅ 最常用的选择
      这是默认推荐选项，选这个！
      
      
      choosing the openssh 呢
      选择第一个选项（Use bundled OpenSSH）✅ 推荐
      两个选项说明：
      1. Use bundled OpenSSH ✅ 推荐
      Git 自带的 OpenSSH
      兼容性好，开箱即用
      大多数人的选择
      默认推荐选项
      
      
      https transport backend 呢？
      选择第一个选项（Use the OpenSSL library）✅ 推荐
      两个选项说明：
      1. Use the OpenSSL library ✅ 推荐
      Git 自带的 OpenSSL
      标准配置，兼容性最好
      适合绝大多数场景
      默认推荐选项
      
      
      configuring the line ending conversions?
      选择第一个选项（Checkout Windows-style, commit Unix-style line endings）✅ 推荐
      三个选项说明：
      1. Checkout Windows-style, commit Unix-style line endings ✅ 推荐
      检出代码时：转换为 Windows 格式（CRLF）
      提交代码时：转换为 Unix 格式（LF）
      Windows 用户的标准配置
      与团队协作时兼容性最好
      
      
      configuring the terminal emulator to use with git bash 呢
      选择第一个选项（Use MinTTY）✅ 推荐
      两个选项说明：
      1. Use MinTTY (the default terminal of MSYS2) ✅ 推荐
      Git Bash 的默认终端
      功能更强大
      支持更好的颜色显示和字体
      更好的复制粘贴体验
      推荐选择
      
      
      choose the default behavior of git pull?
      选择第一个选项（Default (fast-forward or merge)）✅ 推荐
      三个选项说明：
      1. Default (fast-forward or merge) ✅ 推荐
      Git 的传统默认行为
      简单直接，适合大多数场景
      新手友好
      
      
      credential helper呢
      选择第一个选项（Git Credential Manager）✅ 推荐
      三个选项说明：
      1. Git Credential Manager ✅ 强烈推荐
      微软开发的现代凭证管理工具
      自动安全地保存 GitHub/GitLab 等账号密码
      支持多因素认证（2FA）
      与 Windows 凭证管理器集成
      目前最好的选择
      
      
      
      extra options :  enable file system caching  / enable symbolic links
      ✅ Enable file system caching - 勾选（推荐）
      提升 Git 性能
      缓存文件系统状态，加快操作速度
      几乎没有缺点
      建议勾选
      我的建议：
      ✅ Enable file system caching  （勾选）
      	☐ Enable symbolic links        （不勾选，除非你知道需要）
      
      在 Grok 细致入微的指导下，Git for Windows总算安装成功了。。。



--------------------------------------------------------------------------
步骤2：安装  Powershell 7 - x64 （系统自带pwshell 5，你必须装 pwshell版本7xx）
--------------------------------------------------------------------------
    我是windows用户，直接进下面的链接，找到对应自己系统的版本即可
    https://github.com/PowerShell/PowerShell/releases/latest
    进去之后发现眼花了，巨多版本，选择【PowerShell-7.5.4-win-x64.msi】
    装完新开powershell终端即可 pwsh --version 检查确认是 pwsh7xx

    怎么找到 powershell 7 ？？？？？？？？？？？？？？？？？？？？？？？？？？？？？？？？？
    win + s —— 搜索 powersehll —— 右键选中PowerShell 7 (x64) —— 添加到桌面（以防下次找不到）
    
    所以，为了防止找不到，建议安装时最好将PowerShell 7 (x64) 的图标放到桌面上


--------------------------------------------------------------------------
步骤3：安装 Claude Code  （via VPN）
--------------------------------------------------------------------------
    我的v2ray http/https 代理端口为：http://127.0.0.1:10809
    将下面三行复制到pwshell 7 ，一次性粘贴、回车
    即可安装 Claude Code
    
    $env:HTTP_PROXY = "http://127.0.0.1:10809"
    $env:HTTPS_PROXY = "http://127.0.0.1:10809"
    irm https://claude.ai/install.ps1 | iex
    
    
    你的代理端口是多少？ 你最好问问Grok/GPT/Gemini/deepseek， 如何在powershell中检查自己目前的VPN端口
    然后改成你自己的端口
    假设你的VPN是 Clash，端口是 7890
    那么你的代码需要改成：
          $env:HTTP_PROXY = "http://127.0.0.1:7890"
          $env:HTTPS_PROXY = "http://127.0.0.1:7890"
          irm https://claude.ai/install.ps1 | iex


    如果你碰到更复杂的 网络 / VPN / 端口 问题，建议询问 Grok/GPT/Gemini/deepseek，寻求更多帮助




--------------------------------------------------------------------------
步骤4：使用 Claude Code  
--------------------------------------------------------------------------
    
    右键 - 以管理员身份运行：pwshell 7 
    输入
    setx PATH "$env:PATH;$env:USERPROFILE\.local\bin"
    这行代码可以实现手工添加 Claude path 至系统环境变量

    随后，重启pwshell 7 
    输入
    claude --version

    如果你运气足够好，应该能看到
      PS C:\Users\**your_user_name**> claude --version
      2.1.7 (Claude Code)

    恭喜你，Claude Code安装成功了！！
    
    
