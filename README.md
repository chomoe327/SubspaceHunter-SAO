# SubspaceHunter-SAO

中文 | [English](README.en.md)

SubspaceHunter-SAO 是一个开源 Unity XR 动作游戏项目框架，围绕类似 SAO 风格的交互、战斗和场景体验进行整理。当前仓库正在分阶段公开，目标是在不误传大体量资源、第三方资源和版权不明确内容的前提下，先公开可共享的项目结构、配置、脚本和 demo 场景。

## 仓库状态

这个公开仓库目前主要包含 Unity 项目配置、可共享源码、公开 demo 场景和项目文档。完整本地项目仍包含大量二进制资源、第三方资源和可能涉及版权的内容，这些内容需要完成许可确认后，才会以外部资源包方式分发。

资源处理策略见 [docs/OPEN_SOURCE_ASSETS.zh-CN.md](docs/OPEN_SOURCE_ASSETS.zh-CN.md)，外部 `.unitypackage` 资源包方案见 [docs/EXTERNAL_ASSET_PACKAGES.zh-CN.md](docs/EXTERNAL_ASSET_PACKAGES.zh-CN.md)。

## Unity 版本

- Unity Editor：`2021.3.45f1`
- 主要目标平台：Android / Quest 类 XR 设备
- XR 相关包：Oculus XR、OpenXR、XR Management

## 当前包含

- `Packages/`
- `ProjectSettings/`
- `Assets/SubspaceHunter/Script` 下可共享脚本
- `Assets/SubspaceHunter/Scenes/Script` 下可共享场景辅助脚本
- `Assets/PublicDemo/PublicScenes` 下的公开 demo 场景文件，当前通过 Git LFS 管理
- 项目文档

## 暂不包含

- 付费 Asset Store 资源包
- 大体量贴图、模型、视频、音频、烘焙数据和 Unity 生成缓存
- 涉及版权或许可证不明确的角色、环境和素材资源

## 打开项目

这个仓库目前还不是完整可直接游玩的项目检出。公开 demo 场景当前作为过渡方案保留在仓库中，长期方案是把经过确认的大体量资源整理为外部 `.unitypackage`，并单独记录需要安装的依赖。若要运行原始完整项目，需要从合法授权的本地副本恢复所需资源目录，然后使用 Unity `2021.3.45f1` 打开。

## 贡献注意事项

- 不要提交 `Library/`、`Temp/`、`Logs/`、`UserSettings/`、`.csproj` 或 `.sln` 文件。
- 只有确认可再分发的大体量二进制资源才可使用 Git LFS 提交。
- 提交 Unity 资源时必须保留对应 `.meta` 文件。
- 不要提交 API Key、服务凭证、签名文件、私有数据库或其他敏感信息。
