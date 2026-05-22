# SubspaceHunter-SAO

<h3 align="center">
中文 | <a href="README.en.md">English</a>
</h3>

SubspaceHunter-SAO 是一个开源的可商用的 Unity XR(VR+MR) 动作游戏项目框架以及可商用的原创美术资产、代码、特效、UI等；围绕类似 SAO 风格的交互、战斗和场景体验进行开发的项目。
项目在2022年由年仅22岁的Hexin Wang 在UCAS大学的宿舍中开发并免费发布下载；国内外社交媒体上传播的刀剑神域VR、SAO、Sword Art Online、以及2023年的Quest3 SAO视频均出自于此项目；
项目发起的初心是为了构建一个完全沉浸式基于脑机接口的无限庞大的多人在线虚拟世界，但由于当时技术不发达以及AI尚未崛起的原因，凭借个人的力量无法实现如此宏大的计划；在2026年Hexin Wang
转向World Model创业创立了Cardinal AI，希望能通过AIGC能力解决大规模3D可交互内容的生产力需求，让每一个人都能制作初属于自己的3A世界。本项目将会作为Cardinal AI开发的官方教程与最佳
实践案例，通过教程的形式教学如何开发出一款VR多人在线动作游戏。
<p align="center">
  <img src="docs/images/readme-hero.png" alt="SubspaceHunter-SAO 项目 Logo" width="720">
</p>

## 通过本项目你将学会/获得
1. 如何构建支持 Meta Quest 等 XR 一体机应用的开发、环境设置
2. 如何优化 VR 场景性能以及渲染处理
3. 带有物理的冷兵器刀剑战斗系统、魔法战斗系统、枪械战斗系统
4. 敌人角色物理系统打击感模拟（打击特效、音效）
5. 九种可拓展的敌人行为树 AI 战斗逻辑、技能设计、距离控制、动画控制
6. XR 设备粒子特效系统的处理与优化
7. XR 原生的手势追踪 UI 交互系统与 UI 动画构建
8. MR 场景下与环境相融合的阴影处理
9. XR 设备串流调试与开发
10. 9 个关卡场景、数种武器道具、十几种不同风格的士兵级、领主级、Boss 级敌人美术资产
11. 学会使用 Cardinal AI 生成配音、音乐、3D 模型、UI 等 AIGC 功能辅助开发

## 开源、可商用资产说明

原创美术资源统一集中在改目录下： Assets/SubspaceHunter/Model/SubspaceHunter-model 

项目中的UI交互、动画、物理系统模拟、战斗逻辑与行为树设计均为原创可商业化使用

<img src="docs/images/readme-characters.png" alt="SubspaceHunter-SAO 角色与敌人资产展示" width="100%">

<img src="docs/images/readme-public-demo.png" alt="SubspaceHunter-SAO 公开 Demo 展示" width="100%">

<img src="docs/images/readme-mr-demo.png" alt="SubspaceHunter-SAO MR 战斗展示" width="100%">

<img src="docs/images/readme-scene-collage.png" alt="SubspaceHunter-SAO 场景展示合集" width="100%">


## 由Hexin Wang 团队制作但不允许商业使用、仅供交流学习的SAO资产

希斯克里夫、青眼恶魔、狗头人领主、石头人、食人花、判教徒尼古拉斯、狗头人骑士、野猪

<img src="docs/images/readme-third-party-assets.png" alt="SubspaceHunter-SAO 第三方资产与 IP 相关资产展示" width="100%">

## 第三方资产Package如需商业化需取得授权


## 项目资源状态

这个公开仓库目前主要包含 Unity 项目配置、可共享源码、公开 demo 场景和项目文档。完整项目资源：3D模型、贴图、音效、音乐等大体量资源需要通过下方的第三方云链接下载Unitypackage并导入。

## Unity 版本

- Unity Editor：`2021.3.45f1`
- 主要目标平台：Android / Quest / PCVR 设备
- XR 相关包：Oculus XR、OpenXR、XR Management

## Github仓库包含

- `Packages/`
- `ProjectSettings/`
- `Assets/SubspaceHunter/Script` 下可共享脚本
- `Assets/SubspaceHunter/Scenes/Script` 下可共享场景辅助脚本
- `Assets/PublicDemo/PublicScenes` 下的公开 demo 场景文件，当前通过 Git LFS 管理
- 项目文档




## 打开项目

下载Github仓库资产后使用 Unity `2021.3.45f1` 打开，再下载资产Unitypackage包后导入项目。

## 贡献注意事项

- 不要提交 `Library/`、`Temp/`、`Logs/`、`UserSettings/`、`.csproj` 或 `.sln` 文件。
- 只有确认可再分发的大体量二进制资源才可使用 Git LFS 提交。
- 提交 Unity 资源时必须保留对应 `.meta` 文件。
- 不要提交 API Key、服务凭证、签名文件、私有数据库或其他敏感信息。
