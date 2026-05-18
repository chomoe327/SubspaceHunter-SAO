# 外部资源包发布方案

这个项目更适合采用“轻量 GitHub 主仓库 + 外部 Unity 资源包”的发布方式。

## 目标架构

### GitHub 主仓库

保留在 Git 中的内容：

- 源代码
- `Packages/`
- `ProjectSettings/`
- 小型文本配置
- 资源包清单和导入说明
- 开源 fallback 版本所需的占位资源
- 项目文档

长期来看，不把大型生产资源作为 Git 或 Git LFS 的默认存储方式。

### 外部资源包

把已经确认可再分发的大型二进制内容打包成可下载的 `.unitypackage`：

- 公开 Demo 场景
- 模型
- 贴图
- 材质
- 动画片段
- 音频
- 字体
- 烘焙光照或导航数据
- 大型 prefab 和特效资源

用户下载资源包后，直接导入到克隆下来的 Unity 项目中即可。

### 由用户自行安装的依赖

付费、授权受限或来源不明确的内容不要再分发，只提供安装说明：

- 商业 Asset Store 包
- 厂商 SDK
- 版权 IP 资源
- 没有明确再分发授权的第三方资源包

## 推荐的资源包拆分

不要做一个覆盖全项目的超大包。按更新频率和授权边界拆开：

| 资源包 | 内容 | 说明 |
| --- | --- | --- |
| `SubspaceHunter.PublicDemo.Scenes.unitypackage` | 公开 Demo 场景及场景本地数据 | 场景单独拆包，避免每次改场景都让用户重新下载全部美术资源。 |
| `SubspaceHunter.PublicDemo.Gameplay.unitypackage` | 可公开的玩法 prefab、小配置、自有交互资源 | 只放确认可再分发的项目自有内容。 |
| `SubspaceHunter.PublicDemo.Environments.unitypackage` | 已批准公开的环境模型、贴图、材质、天空盒 | 如果继续变大，再按关卡或主题拆包。 |
| `SubspaceHunter.PublicDemo.Characters.unitypackage` | 已批准公开的原创角色资源 | 版权角色和未获授权的第三方角色不要放入。 |
| `SubspaceHunter.PublicDemo.Audio.unitypackage` | 已批准公开的原创或可再分发音频 | 音频体积大且授权敏感，建议单独拆包。 |
| `SubspaceHunter.PublicDemo.Fonts.unitypackage` | 已批准字体或重新生成的 fallback SDF 字体 | 公开版优先使用小型 fallback 字体。 |

如果某个包超过约 1-2 GB，或者更新特别频繁，就继续往下拆。

## 用户导入顺序

推荐的用户流程：

1. 克隆 GitHub 仓库。
2. 用 Unity `2021.3.45f1` 打开项目。
3. 先按文档安装必须从官方来源获取的 SDK 和第三方依赖。
4. 再按下面顺序导入公开资源包：
   1. `Gameplay`
   2. `Environments`
   3. `Characters`
   4. `Audio`
   5. `Fonts`
   6. `Scenes`
5. 如果导入过程改动了脚本、shader 或全局资源，重启一次 Unity。
6. 打开 `Assets/PublicDemo/PublicScenes/进入游戏.unity` 或文档指定的入口场景。

## 打包规则

- 用 Unity 导出 `.unitypackage`，不要手动压缩目录替代。
- 保持原始路径和 `.meta`，这样 GUID 引用才不会断。
- 除非是有意重构并且已经在 Unity 中验证，否则不要为了打包而先移动资源。
- 每个资源包都只能包含确认可再分发的内容。
- 每个资源包都维护一份清单，至少记录：
  - 文件名
  - 版本
  - 发布日期
  - Unity 版本
  - 包含的根目录
  - 依赖哪些其他资源包
  - 授权状态
  - 下载地址
  - SHA-256 校验值
- 如果一个资源依赖另一个资源，要么放在同一个包里，要么在文档中明确依赖关系和导入顺序。
- 推荐使用稳定包名加语义化版本，例如：

  ```text
  SubspaceHunter.PublicDemo.Scenes.v0.1.0.unitypackage
  ```

## 版本管理

建议维护两条版本线：

- 代码版本使用 Git tag，例如 `v0.1.0`
- 资源包使用匹配版本，例如 `PublicDemo.Scenes v0.1.0`

仓库文档中需要明确写出每个 Git tag 对应哪些资源包版本。

## 当前过渡状态

仓库目前已经通过 Git LFS 包含了 `Assets/PublicDemo/PublicScenes/`，这是因为这些场景是重要项目内容。这个状态可以作为过渡方案接受，但长期目标应该是：把大型 Demo 场景和已经获批的依赖一起迁移到外部资源包，GitHub 中只保留轻量占位内容或导入说明。

当前依赖审计见 `docs/PUBLIC_DEMO_DEPENDENCIES.zh-CN.md`。

## 下一步工程动作

1. 给每个 PublicDemo 依赖根目录标记：
   - 进入公开资源包
   - 由用户自行安装
   - 仅私有保留
   - 必须替换
2. 只用确认可再分发的资源构建第一版资源包集合。
3. 在一个干净 clone 中实际导入测试这些资源包。
4. 资源包列表稳定后，再补一份机器可读的资源包清单。
5. 等资源包导入流程验证完成后，再决定是否把当前托管在 Git LFS 的 PublicDemo 场景从公开分支和历史中清理出去。
