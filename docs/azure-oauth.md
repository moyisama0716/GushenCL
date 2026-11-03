# Microsoft 正版登录：Azure 应用配置教程

> 适用于 **GushenCL / MoyiCL** 的 Microsoft 正版登录。  
> 作者：沫逸　·　福州风霜赴月科技有限公司

GushenCL / MoyiCL 使用 **OAuth 2.0 设备代码流（Device Code Flow）** 完成微软登录，启动器不会接触你的微软密码。微软不允许第三方启动器共用官方启动器的 OAuth 凭据，所以需要你自己创建一个 Azure 应用，拿到 **Application (client) ID**（客户端 ID）。

> **重要：** 自 2026 年起，Minecraft Services 会校验客户端 ID 是否在 Minecraft 的白名单中。只在 Azure 注册应用还不够，还需要向 Minecraft 提交 **Java Edition Game Service API** 申请。否则最后一步会返回：
>
> `HTTP 403 Invalid app registration`
>
> 详见本文第 3 步。

---

## 一、准备

- 一个 Microsoft 账号（能正常登录 Azure / Microsoft Entra）。
- 不需要购买 Azure 服务器或付费资源；应用注册本身不产生资源费用。
- 一个已购买 **Minecraft: Java Edition** 的微软账号，用于测试登录。
- 建议使用个人 Microsoft 账号；不要使用学校/公司租户中受限的账号。

---

## 二、在 Azure 创建应用

### 1. 打开应用注册页面

浏览器打开以下任一入口：

- [Microsoft Entra 管理中心](https://entra.microsoft.com/) → 左侧 **Entra ID** → **应用注册 / App registrations**
- 或 [Azure Portal](https://portal.azure.com/) → **Microsoft Entra ID** → **应用注册**

点击 **新注册 / New registration**。

### 2. 填写注册信息

| 字段 | 填写建议 |
| --- | --- |
| 名称 / Name | `GushenCL` 或 `MoyiCL`（以后可改） |
| 受支持的账户类型 | **仅个人 Microsoft 账户**（Personal Microsoft accounts only）<br>或 **任何 Entra ID 租户 + 个人 Microsoft 账户** |
| 重定向 URI | 设备代码流不需要；如页面要求，选 **移动和桌面应用程序**，填 `https://login.microsoftonline.com/common/oauth2/nativeclient` |

> 不要选择“仅此组织目录中的账户”。我们的设备代码流走 `/consumers`，应用必须支持个人 Microsoft 账户。

点击 **注册 / Register**。

### 3. 复制客户端 ID

注册完成后进入应用 **概述 / Overview**，复制：

```text
应用程序(客户端) ID
Application (client) ID
```

形如：

```text
00000000-0000-0000-0000-000000000000
```

这个 ID **不是密码**，可以安全地填进启动器。不要创建或填写客户端密码（Client Secret）。

### 4. 启用公共客户端流（必做）

左侧 **管理 → 身份验证 / Authentication**：

1. 拉到 **高级设置 / Advanced settings**；
2. 把 **允许公共客户端流 / Allow public client flows** 设为 **是 / Yes**；
3. 点击 **保存 / Save**。

不开启会报：

```text
AADSTS7000218: The request body must contain the following parameter: 'client_assertion' or 'client_secret'
```

### 5. API 权限

默认的 `Microsoft Graph → User.Read` 足够完成登录，不需要手动添加 `XboxLive.signin`。  
`XboxLive.signin` 是登录时请求的 scope，不是 Azure 门户里能勾选的普通 API 权限；Minecraft 的客户端 ID 白名单独立在下一步申请。

不需要：

- 客户端密码 / Client Secret
- 证书
- 暴露 API
- 付费订阅

---

## 三、向 Minecraft 申请客户端 ID 白名单（关键）

只在 Azure 注册应用，通常会在启动器最后一步失败：

```text
HTTP 403
Invalid app registration, see https://aka.ms/AppRegInfo
```

原因是 Minecraft Services 要求第三方启动器的 Client ID 先通过审核。

### 官方入口

- 说明页：[Java Edition Game Service API Review or Application Process](https://help.minecraft.net/hc/en-us/articles/16254801392141)
- 申请表单（Minecraft 官方 Microsoft Forms）：  
  <https://forms.cloud.microsoft/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR-ajEQ1td1ROpz00KtS8Gd5UNVpPTkVLNFVROVQxNkdRMEtXVjNQQjdXVC4u>

### 填写内容

表单通常需要：

- 应用名称：`GushenCL` / `MoyiCL`
- **Application (client) ID**：第二步复制的 ID
- 启动器说明：Minecraft Java Edition 第三方启动器
- 认证方式：Microsoft OAuth 2.0 Device Code Flow
- 用途：仅用于用户登录其已拥有的 Minecraft: Java Edition
- 联系邮箱
- 隐私/安全说明：不收集微软密码，只保存本机令牌

提交后等待 Minecraft / Mojang 审核邮件。审核时间不固定，可能数天到数周；没有加急通道。通过后，同一个 Client ID 才能通过 `login_with_xbox`。

> 如果表单打不开，先从官方说明页进入；不要使用来历不明的“代申请”服务，也不要把 Client ID 交给第三方代填。

---

## 四、把 Client ID 填进启动器

### GushenCL

1. 打开 **设置**；
2. 找到 **Microsoft 正版登录**；
3. 在 `Azure Application (client) ID` 中粘贴第二步复制的 ID；
4. 点击 **保存**；
5. 打开 **账户** → 点击 **正版登录**。

### MoyiCL

MoyiCL 使用独立数据目录 `%USERPROFILE%\MoyiCL`，需要单独填一次；可以使用同一个 Client ID。

### 完成设备代码授权

1. 启动器弹出设备代码窗口；
2. 点击 **打开授权页面**（或手动打开 <https://microsoft.com/devicelogin>）；
3. 输入窗口中显示的代码；
4. 登录拥有 Minecraft 的微软账号；
5. 同意授权；
6. 回到启动器，等待自动完成；
7. 账户页出现 **Microsoft 正版** 档案后即可启动。

首次登录后启动器会保存 refresh token，后续启动自动续期，不需要每次重新授权。

---

## 五、常见错误

| 错误 | 原因 | 处理 |
| --- | --- | --- |
| `AADSTS7000218` | 没开启公共客户端流 | 身份验证 → 允许公共客户端流 → 是 → 保存 |
| `AADSTS700016` / `unauthorized_client` | 账户类型或租户不对 | 应用必须支持个人 Microsoft 账户；代码使用 `/consumers` |
| `invalid_client` | Client ID 填错，或应用不是公共客户端 | 重新复制 Client ID；开启公共客户端流 |
| `403 Invalid app registration` | Client ID 未通过 Minecraft 白名单 | 完成第三步申请；等待审核通过 |
| `2148916233` | 微软账号没有 Xbox 档案 | 先在 [Xbox 官网](https://www.xbox.com/) 创建档案 |
| `2148916238` | 未成年账号受家庭组限制 | 让家庭组中的成年人授权 |
| `404` / 无 Minecraft 档案 | 该微软账号没有购买 Java Edition | 换拥有游戏的账号；检查是否买到了基岩版 |
| 授权页登录后仍失败 | 代理、VPN、浏览器缓存 | 换网络/浏览器重试；确认系统时间正确 |
| `AADSTS65001` | 用户/管理员未同意权限 | 保留默认 `User.Read`；个人账号重新授权 |

---

## 六、安全说明

- **Client ID 不是密钥**，可以公开；不要创建 Client Secret，也不要把它发给别人。
- 启动器只保存 Minecraft 访问令牌和 OAuth refresh token 到本机 `accounts.json`，不保存微软密码。
- 不要分享 `%USERPROFILE%\GushenCL\config\accounts.json` 或 `%USERPROFILE%\MoyiCL\config\accounts.json`；其中的令牌等同于登录凭据。
- 如需撤销授权，可到 [Microsoft 账户的应用和 services 管理页](https://account.live.com/consent/Manage) 移除对应应用。
- 建议只从本仓库/本发布页获取 EXE，不要使用他人提供的“已配置好 Client ID”的修改版。

---

## 七、快速检查清单

- [ ] Azure 应用已注册
- [ ] 支持个人 Microsoft 账户
- [ ] 已复制 Application (client) ID
- [ ] Authentication → Allow public client flows = Yes
- [ ] 没有创建/填写 Client Secret
- [ ] 已向 Minecraft 提交 Client ID 白名单申请
- [ ] 已收到审核通过邮件
- [ ] 启动器设置中已保存 Client ID
- [ ] 使用拥有 Minecraft: Java Edition 的微软账号登录
- [ ] 账户页显示“Microsoft 正版”
