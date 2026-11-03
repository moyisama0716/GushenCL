# Security Policy / 安全说明

## 凭据处理

- GushenCL / MoyiCL 不收集 Microsoft 或 LittleSkin 密码。
- Microsoft 登录使用官方 OAuth 2.0 Device Code Flow。
- LittleSkin 密码只发送给 LittleSkin 官方 Yggdrasil 服务器。
- 访问令牌和 refresh token 仅保存在本机数据目录。
- 启动器不包含客户端密钥（Client Secret），Microsoft 应用按公共客户端配置。

## 本地令牌

在线令牌位于：

```text
%USERPROFILE%\GushenCL\config\accounts.json
%USERPROFILE%\MoyiCL\config\accounts.json
```

`accounts.json` 等同登录凭据，请不要上传、截图或分享。若怀疑泄露，请在对应平台撤销授权并重新登录。

## 下载与安装

- 只从项目正式发布页获取启动器。
- 启动器不会要求用户关闭杀毒软件。
- 启动器不会索取 Microsoft 密码、邮箱密码或支付信息。
- 任何声称“代办 Minecraft 白名单”“出售正版登录 Client ID”的第三方服务都与本项目无关。

## 漏洞报告

请通过项目公开页面中的联系方式私下报告安全问题，不要在公开 Issue 中粘贴令牌、邮箱密码或 `accounts.json` 内容。
