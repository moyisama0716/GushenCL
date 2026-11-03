# NOTICE · 第三方声明

GushenCL · 古神启动器  
Copyright © 2026 福州风霜赴月科技有限公司 · 作者：沫逸  
All rights reserved.

本软件名为 GushenCL（中文名：古神启动器），由 **沫逸** 开发，所属公司为 **福州风霜赴月科技有限公司**。

## 与 Minecraft / Mojang / Microsoft 的关系

GushenCL 是**非官方**的 Minecraft: Java Edition 启动器，与 Mojang Studios、Microsoft 或任何模组平台均不存在隶属、授权或背书关系。

- Minecraft 是 Microsoft Corporation 的商标。
- 本启动器**不包含、不分发** Minecraft 游戏本体、客户端资源或任何需要 Mojang 授权的素材。
- 所有原版游戏文件均由用户本地机器上的启动器从 Mojang 官方渠道下载。
- 用户需要自行拥有合法的 Minecraft: Java Edition 账户及对应服务条款所允许的使用权。

## 第三方开源组件

| 组件 | 许可证 | 用途 |
| --- | --- | --- |
| OpenJFX / JavaFX 21 | GPL v2 with Classpath Exception | 桌面 UI 与渲染 |
| Jackson Databind / Core / Annotations | Apache License 2.0 | JSON 解析与序列化 |
| Jackson JSR-310 | Apache License 2.0 | 时间类型支持 |
| JUnit Jupiter 5 | Eclipse Public License 2.0 | 自动化测试（仅开发/测试期） |

这些组件的完整许可证文本请参阅其官方发布页或 `.m2` 本地仓库中对应构件附带的许可证文件。

## 外部 API / 数据源

- Minecraft 版本清单与资源：Mojang Piston Meta / Launcher Meta / resources.download.minecraft.net
- Fabric：Fabric Meta / Maven
- Quilt：Quilt Meta
- Forge：MinecraftForge Maven
- NeoForge：NeoForged Maven
- 社区内容：Modrinth API v2

各服务由相应组织独立运营，本启动器仅按照其公开接口获取数据。用户在使用时应遵守对应服务的 API 使用条款。

## 用户内容

用户导入的整合包、模组、资源包、光影、存档与配置均由用户自行获取并负责其合法性。GushenCL 不会上传用户数据；离线档案、UUID、实例配置与日志都保存在用户本机。

## 安全说明

启动器会校验下载文件的哈希、检查压缩包路径、验证 JAR 结构，并在导入时跳过可执行文件。但任何第三方内容仍然可能存在恶意代码；请仅从可信来源获取整合包与模组。
