# OCI Help Telegram 机器人使用指南

`oci-help-telegram` 是一个基于 `lemoex/oci-help` 项目开发的 Telegram 机器人，允许用户通过 Telegram 界面管理和操作 Oracle Cloud Infrastructure (OCI) 实例。

与原版相比，多了多任务抢机，任务管理，租户测活等功能。

## 前置准备

1.  **获取 Telegram Bot Token:**
    *   在 Telegram 中与 [@BotFather](https://t.me/BotFather) 对话。
    *   使用 `/newbot` 命令创建一个新机器人，并获取其 API Token。
2.  **获取您的 Telegram Chat ID:**
    *   您可以使用特定的机器人（如 @userinfobot 或 @getmyid_bot）或通过机器人 API 来获取您自己的 Telegram Chat ID。

## 配置

1.  **配置 `oci-help.ini` 文件:**
    *   主要配置项包括：
        *   `user`: OCI 用户 OCID。
        *   `fingerprint`: API 密钥指纹。
        *   `tenancy`: 租户 (Tenancy) OCID。
        *   `region`: OCI 区域 (Region)。
        *   `key_file`: API 私钥文件路径。
        *   `key_password` (可选): 如果私钥有密码则需要配置。
    *   在 `oci-help.ini` 的 `[DEFAULT]` 部分，添加 Telegram Bot 的配置：
        *   `token`: 您从 BotFather 获取的 Bot Token。
        *   `chat_id`: 您的 Telegram Chat ID。
        *   `proxy` (可选): 如果需要，配置代理地址（如 `http://127.0.0.1:7890`）。
        *   `cmd` (可选): 预设的可以在机器人中执行的系统命令。
    *   确保 `oci-help.ini` 文件位于编译后的机器人程序同一目录下。

## 运行

    *   将编译好的可执行文件（例如oci-help-tgbot-linux-amd64）和 `oci-help.ini` 配置文件上传到您的服务器。
    *   在服务器上运行该程序：`./oci-help-tgbot-linux-amd64`。

    # 前台运行需要一直开着终端窗口，可以在 Screen 中运行程序，以实现断开终端窗口后一直运行。
    # 创建 Screen 终端
    screen -S oci-help-tgbot 
    # 在 Screen 中运行程序
    ./oci-help-tgbot-linux-amd64
    # 离开 Screen 终端
    按下 Ctrl 键不松，依次按字母 A 键和 D 键。或者直接关闭终端窗口也可以。
    # 查看已创建的 Screen 终端
    screen -ls
    # 重新连接 Screen 终端
    screen -r oci-help-tgbot 

## 使用方法

1.  **启动机器人:**
    *   在 Telegram 中搜索并打开您创建的机器人聊天窗口。
    *   发送 `/start` 命令启动机器人。如果您的 Chat ID 配置正确，机器人会显示欢迎信息和主菜单。
2.  **主菜单操作:**
    *   机器人启动后会显示一个 Inline Keyboard（内联键盘）菜单，提供以下主要功能：
        *   **列出实例 **: 查看当前账户下所有实例的状态。
        *   **管理引导卷**: 查看和管理引导卷。
        *   **批量导出实例IP **: 导出账户下所有实例的公共 IP 地址。
        *   **检查账户存活**: 检查配置的 OCI 账户连接状态。
        *   **查看运行中的任务**: 查看当前正在执行或排队的任务（如批量创建实例）。
        *   **重新加载配置**: 重新加载 `oci-help.ini` 配置文件，无需重启机器人。
        *   **执行命令 **: 执行在配置文件 `cmd` 项中预设的或直接输入的系统命令（谨慎使用）。
        *   **查看日志 **: 查看机器人运行的部分日志输出。
3.  **实例管理:**
    *   点击 "列出实例" 后，会显示实例列表。
    *   点击某个实例，可以进入该实例的详情页面。
    *   在实例详情页，通常可以进行以下操作（具体取决于实例状态）：
        *   启动 
        *   停止 
        *   重启
        *   终止
        *   更换公共IP
        *   升级/降级 - 需要实例处于停止状态。
        *   修改名称
        *   配置 Oracle Cloud Agent 插件 
4.  **引导卷管理:**
    *   点击 "管理引导卷" 后，会显示引导卷列表。
    *   点击某个引导卷，可以进入该引导卷的详情页面。
    *   在引导卷详情页，通常可以进行以下操作：
        *   修改性能 
        *   修改大小
        *   终止引导卷 
5.  **批量创建实例:**
    *   点击主菜单中的 "创建实例"
    *   选择一个配置好的租户账户。
    *   从该账户下配置的实例模板中选择一个开始创建。
    *   创建过程将在后台任务中运行，可以通过 "查看运行中的任务" 来监控进度。

## 注意事项

*   **权限:** 只有配置文件中指定的 `chat_id` 的用户才能使用该机器人。
*   **状态依赖:** 某些操作（如升级/降级）要求实例处于特定状态（如停止）。
*   **后台任务:** 批量创建实例等耗时操作会作为任务在后台运行。
*   **日志:** 机器人会将部分输出写入 `output.log` 文件。
*   **安全性:** 机器人涉及云资源管理，请确保配置文件和服务器安全，谨慎使用 "执行命令" 功能。

## 说明
存疑勿用。
