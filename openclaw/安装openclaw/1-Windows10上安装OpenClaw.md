# Win10上安装OpenClaw


本文记录一下Win10上安装OpenClaw的过程，参看了如下网站：

- [OpenClaw官网](https://openclaw.ai/)

- [2026 OpenClaw安装教程全攻略：从安装到启动，新手一步到位不踩坑](https://www.oschina.net/news/414502)

- [Windows 10⁄11 OpenClaw安装与配置说明](https://zhuanlan.zhihu.com/p/2010383824069096813)

- [龙虾AI（OpenClaw）在Windows保姆级部署教程](https://www.bilibili.com/opus/1177996279628693508)

- [windows系统本地安装部署openclaw详细版教程（最细保姆版）](https://www.cnblogs.com/yjd_hycf_space/p/19696891)

- [Windows安装OpenClaw保姆级教程: 集成Deepseek+飞书, 1小时搞定你的私人AI助手](https://news.qq.com/rain/a/20260302A02C8X00)


⚠️ 注意：原生 Windows 支持有限，官方更推荐通过 WSL2 部署

<br />

## 1. 安装部署(Installation)

OpenClaw提供了自动化脚本安装和手动 npm 安装两种方式。推荐优先使用自动化脚本

### 1.1 方式一：自动化脚本安装（推荐）

在Windows命令行执行如下命令:

```bash
# powershell -c "irm https://openclaw.ai/install.ps1 | iex"
```
阅读`install.psl`可以看到主要会执行如下步骤：

- 检测系统环境

- 安装必要依赖（Node.js等）

- 下载OpenClaw核心文件

- 配置环境变量

- 启动配置向导

>ps: 此安装过程可能花费时间较长，请耐心等待

---

### 1.2 方式二：手动安装（备选）

如果脚本执行失败（如网络问题或权限限制），可使用npm全局安装。

#### 1.2.1 安装Node.js

OpenClaw 必须运行在Node.js `v22.22或更高版本`。我们可以[https://nodejs.org/zh-cn](https://nodejs.org/zh-cn)来进行下载。

安装完成后在命令行验证是否成功：

```bash
# npm --version
11.11.0

# node --version
v24.14.1
```

若npm命令找不到，则按如下步骤进行设置：

1. **打开系统环境变量设置**

    按下Win + R，输入`sysdm.cpl`，回车 → 切换到「高级」→「环境变量」.

    或「我的电脑」→「属性」

1. **编辑用户 PATH 变量**

    - 在「用户变量」下找到Path，点击「编辑」

    - 点击「新建」，粘贴 npm 全局目录. (例如：C:\Users\liuzyan\AppData\Roaming\npm)

    - 点击「确定」保存所有设置

#### 1.2.2 安装openclaw

使用npm来进行openclaw的安装：

```bash
# npm install -g openclaw@latest --verbose
```

鉴于npm 默认源在部分地区访问缓慢或被限流，我们可以使用淘宝镜像源来进行安装：

```bash
# npm install -g openclaw@latest --registry=https://registry.npmmirror.com --verbose
```

#### 1.2.3 手动安装网关服务（关键步骤！）

网关服务必须单独安装，否则无法后台运行:

>ps: 本人未亲自验证是否须单独安装

```bash
# openclaw gateway install
```

安装成功后，会看到类似`Service: Scheduled Task (registered)` 的提示.

<br>

## 2. 验证安装 (Verification)

安装完成后，验证 CLI 工具是否可用，并确认 Node 环境正确.

1. **检查Node版本**

    ```bash
    # node --version
    v24.14.1
    ```

    确认Node.js版本仍未v24.14.1

1. **检查 OpenClaw 版本**

    若成功输出如下信息，则表明openclaw安装成功：

    ```bash
    # openclaw --help
        
    🦞 OpenClaw 2026.4.1 (da64a97) — If something's on fire, I can't extinguish it—but I can write a bea utiful postmortem.
    
    Usage: openclaw [options] [command]

    ...
    ```

<br>

## 3. 通过向导进行配置(Wizard Configuration)

安装完成后，需通过交互式向导完成核心功能配置。此环节将设置网关、通信渠道、AI 模型及工作空间。

`openclaw onboard` 是 OpenClaw 的交互式初始化配置向导，用于帮助用户快速完成 AI 助手的核心设置，使其从“安装完成”状态变为“真正可使用”的状态：

- ‌配置大模型提供商‌（如 Anthropic Claude、OpenAI、Qwen、DeepSeek、GLM 等）并绑定 API Key 或本地模型；

- ‌设置消息渠道‌（如 Telegram、Discord、Slack、QQ、微信等），以便通过常用通讯工具与 OpenClaw 交互；
‌
- 安装和启用技能（Skills）‌，赋予 OpenClaw 执行具体任务的能力（如文件操作、网页浏览、自动化办公等）；
‌
- 配置网关（Gateway）‌，启动本地或远程服务，支持 Web 控制面板访问（默认 http://127.0.0.1:18789）；

- 安装守护进程‌（通过 --install-daemon 参数），实现开机自启、7×24 小时运行。

该命令是官方推荐的‌新手首选配置方式‌，采用问答式引导，无需手动编辑配置文件，大幅降低使用门槛 ‌

---

### 3.1 启动配置向导

使用全新的 onboard 向导：

```bash
# openclaw onboard --install-deamon
```

根据自己的情况选择是否安装守护进程(--install-daemon)。如果未未安装此守护进程，意味着未配置开机自启动的守护服务，此时需‌手动启动 OpenClaw Gateway 服务‌(ps: 请参看如下“补充”部分)，并可选择是否后续补装自启动配置。

#### 补充: 手动启动OpenClaw Gateway方法

>ps: 这里我们openclaw是采用原生windows安装

1. **若使用 WSL2（推荐环境）**

    在 WSL2 的 Ubuntu 终端中运行以下命令启动 Gateway 服务：

    ```bash
    # openclaw gateway start
    ```

    或者直接运行网关进程（适用于临时测试）：

    ```bash
    # openclaw gateway --port 18789
    ```

1. **若在原生Windows(非WSL)**

    打开 ‌PowerShell 或 CMD‌，执行:

    ```bash
    # openclaw gateway start
    ```

---

### 3.2 配置步骤详解

向导将按顺序引导您完成以下关键配置:

#### 第一步： 风险告知

这一步主要是告诉你，使用OpenClaw可能会有一些风险。请问你是否继续？

你想使用OpenClaw, 那就必须要同意它的一些风险告知。按`向左方向键←`，选择`Yes`，按`Enter`回车确认:




#### 第二步：选择配置模式




<br />

## 4. 附录1：openclaw安装位置

通常我们可以使用如下命令来查看openclaw的安装位置：

```bash
# where openclaw
C:\Users\xxxx\AppData\Roaming\npm\openclaw
C:\Users\xxxx\AppData\Roaming\npm\openclaw.cmd
```


## 5. 附录2：openclaw卸载

可以通过执行如下命令进行卸载：

```bash
# npm uninstall -g openclaw
# npm cache clean --force   # 清理缓存
```
