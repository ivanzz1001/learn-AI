# 解决安装OpenClaw卡死问题

如果您尝试全局安装 OpenClaw，但命令长时间无响应、进度停滞或终端光标静止不动，则可能是由于网络阻塞、权限限制、Node.js 版本不兼容或依赖构建卡死所致。本文介绍一下此问题的解决方法。

参看:

- [OpenClaw安装过程中卡住怎么办](https://www.php.cn/faq/2204563.html)


## 1. 切换 npm 镜像源并清理缓存

npm 默认源在部分地区访问缓慢或被限流，导致包下载中断；同时本地缓存损坏也可能引发安装流程异常中断。切换至稳定国内镜像并强制清除旧缓存可显著提升安装成功率。

1. 执行命令切换为 npmmirror 淘宝镜像源

    ```bash
    # npm config set registry https://registry.npmmirror.com
    ```

1. 清除全部 npm 缓存数据

    ```bash
    # npm cache clean --force
    ```

1. 重新发起安装

    ```bash
    # npm install -g openclaw@latest --no-audit --no-fund
    ```

## 2. 验证并升级Node.js至v22或更高版本

OpenClaw 明确要求 Node.js ≥22.0.0，低于该版本将导致依赖解析失败或编译阶段静默卡死，且错误日志可能不直接提示版本问题。

1. 检查当前Node.js版本

    ```bash
    # node --version
    v24.14.1
    ```

1. 若输出为`v20.x`或更低，请卸载旧版并从[https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)下载安装 LTS（v22.x）及以上版本

1. 验证路径是否正确（尤其存在 nvm 多版本时）

    ```bash
    # where node     //windows  
    # which node     //macOS or Linux
    ```

## 3. 以管理员权限运行安装命令

全局安装需向系统级目录(如/usr/local/lib/node_modules 或 C:\Users\xxx\AppData\Roaming\npm\node_modules)写入文件，普通用户权限不足会导致进程挂起或报 EACCES 错误。

- **Windows用户**

  右键“Windows PowerShell”，选择以`管理员身份运行`，再执行安装命令


- **macOS/Linux用户**

  执行命令时添加上sudo:

  ```bash
  # sudo npm install -g openclaw@latest --no-audit --no-fund
  ```

  或采用免`sudo`方案, 创建独立全局目录并配置prefix，避免后续每次均需提权

## 4. 启用详细日志定位卡点位置

添加`--verbose`参数可输出完整安装流水，帮助识别卡死环节是发生在下载、解压、preinstall 脚本还是 node-gyp 构建阶段，从而针对性干预:

- 运行带调试信息的安装命令

  ```bash
  # npm install -g openclaw@latest --no-audit --no-fund --verbose
  ```

- 观察终端最后有效输出行，例如：fetching: https://registry.npmmirror.com/xxx/-/xxx.tgz 表示网络层阻塞

- 若停在 gyp info using node-gyp@... 后无进展，则大概率是 Python 环境或编译工具链缺失


## 5. 跳过非核心依赖与脚本执行

某些可选依赖（optionalDependencies）或 postinstall 脚本在特定环境下无法完成，会阻塞整个安装流程。跳过它们可在保留主功能前提下完成基础安装。

1. 禁用可选依赖安装
    
    ```bash
    # npm install -g openclaw@latest --no-audit --no-fund --no-optional
    ```

1. 同时忽略所有生命周期脚本`--ignore-scripts`
    
    组合使用如下命令:
    ```bash
    # npm install -g openclaw@latest --no-audit --no-fund --no-optional --ignore-scripts
    ```

## 6. 改用 Yarn 替代 npm 执行安装

Yarn 的依赖解析策略和并发下载机制与 npm 存在差异，在 npm 持续卡死时，Yarn 常能绕过相同障碍完成安装。

1. 确保已安装 Yarn

    ```bash
    # npm install -g yarn
    ```

1. 设置 Yarn 镜像源
    
    ```bash
    # yarn config set registry https://registry.npmmirror.com
    ```

1. 执行全局安装

    ```bash
    # yarn global add openclaw@latest
    ```