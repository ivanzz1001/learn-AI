# Win10上安装OpenClaw

本文记录Win10上安装OpenClaw的过程， 参看：

- 官网：https://openclaw.ai/

- OpenClaw安装过程中卡住怎么办：https://www.php.cn/faq/2204563.html

- OpenClaw 仪表盘突然消失: https://blog.csdn.net/2301_78671196/article/details/159422822

- OpenClaw最新版(3月7日版本)Windows本地电脑部署教程: https://blog.csdn.net/luwei42768/article/details/158811930


## 1. 安装步骤

官方推荐我们使用如下脚本来在Win10上安装OpenClaw:

```bash
# powershell -c "irm https://openclaw.ai/install.ps1 | iex"
```

但是我们使用上述命令全局安装OpenClaw时经常出现卡死，下面我们介绍解决方法。

### 1.1 解决安装OpenClaw卡死问题

如果您尝试全局安装 OpenClaw，但命令长时间无响应、进度停滞或终端光标静止不动，则可能是由于网络阻塞、权限限制、Node.js 版本不兼容或依赖构建卡死所致。以下是解决此问题的步骤：

#### 1.1.1 切换 npm 镜像源并清理缓存

npm 默认源在部分地区访问缓慢或被限流，导致包下载中断；同时本地缓存损坏也可能引发安装流程异常中断。切换至稳定国内镜像并强制清除旧缓存可显著提升安装成功率。

1. 执行命令切换为 npmmirror 淘宝镜像源

    ```bash
    # npm config set registry https://registry.npmmirror.com
    ```

1. 清除全部 npm 缓存数据：

    ```bash
    # npm cache clean --force
    ```

1. 重新发起安装

    ```bash
    # npm install -g openclaw@latest --no-audit --no-fund
    ```



2 