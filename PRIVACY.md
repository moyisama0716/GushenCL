# Privacy Policy / 隐私说明

**GushenCL / MoyiCL**  
作者：沫逸  
公司：福州风霜赴月科技有限公司

## 1. 我们收集什么

启动器不需要注册开发者账户，也不包含开发者运营的账户服务器、统计 SDK 或广告 SDK。

启动器会在本机保存：

- 启动器设置；
- 本地实例与游戏目录配置；
- 玩家档案；
- 在线登录令牌（Microsoft / LittleSkin）；
- 日志与缓存。

这些数据保存在用户自己的数据目录中，默认位置：

```text
%USERPROFILE%\GushenCL
%USERPROFILE%\MoyiCL
```

## 2. Microsoft 登录

Microsoft 登录通过 Microsoft identity platform 的 OAuth 2.0 设备代码流完成。

- 启动器不会接触或保存 Microsoft 账户密码。
- 启动器只在本机保存 OAuth access token / refresh token，用于后续免密续期。
- 令牌不会发送给开发者，也不会发送给任何第三方。
- 启动器只请求 `XboxLive.signin offline_access`，用于验证 Minecraft: Java Edition 所有权与获取启动档案。

用户可以在 Microsoft 账户的“应用和服务”页面撤销授权。

## 3. LittleSkin 登录

LittleSkin 登录使用 LittleSkin 官方 Yggdrasil API。

- 启动器不保存 LittleSkin 密码。
- 只在本机保存 Yggdrasil access token / client token。
- 密码仅发送给 LittleSkin 官方认证服务器。

## 4. 网络请求

启动器会访问以下类别的服务，以完成其功能：

- Mojang / Minecraft 官方版本与资源 API；
- Fabric / Quilt / Forge / NeoForge 官方或镜像 API；
- Modrinth、CurseForge（经 MCIM 镜像）、MC百科；
- Microsoft / Xbox Live / Minecraft Services 登录服务；
- LittleSkin / authlib-injector；
- 用户在启动器中配置的其他地址。

这些请求受对应服务自己的隐私政策约束。

## 5. 我们不做什么

- 不收集 Microsoft 或 LittleSkin 密码；
- 不建立开发者侧账户数据库；
- 不出售、出租或共享用户令牌；
- 不将令牌上传到开发者服务器；
- 不分发 Minecraft 游戏本体或付费资源。

## 6. 数据删除

退出启动器后，用户可以直接删除对应数据目录来删除本地数据。删除前请自行备份存档。

## 7. 联系方式

如对隐私或安全有疑问，请通过项目公开页面或公司官方联系方式联系开发者。
