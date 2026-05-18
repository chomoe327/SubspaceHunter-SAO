# 开源资源处理策略

这个 Unity 项目包含大量第三方资源和二进制内容。在公开仓库前，需要逐个检查资源目录的授权情况。

## 当前体积概况

- `Assets/` 约 26 GB。
- 体积最大的目录包括 `Assets/SubspaceHunter`、`Assets/Resources`、`Assets/Knife`、`Assets/Frank_Slash_Pack`、`Assets/InsaneGunner`、`Assets/Rifle_27A2_Pro`、`Assets/Oculus`。
- 有多个单文件超过 100 MiB，包括大贴图、视频、字体、DLL 和导入模型。

## GitHub 处理策略

建议采用下面的拆分方式：

1. 将源代码、项目设置、包清单、小配置文件和可开源的占位资源放入 Git。
2. 已确认可再分发的大型二进制资源，长期应通过外部 `.unitypackage` 下载包发布，而不是把 Git LFS 当作资源仓库。
3. Git LFS 只作为迁移期过渡手段，用于暂时保留少量关键资源。
4. 不要提交付费 Asset Store 包、版权角色/媒体资源、授权不明确的可再分发文件。
5. 对不能公开的原始资源，提供一套小型替代资源用于开源构建。

## 需要授权审查的资源目录

公开仓库前优先检查这些目录：

- `Assets/SAO`
- `Assets/SubspaceHunter`
- `Assets/Knife`
- `Assets/Frank_Slash_Pack`
- `Assets/InsaneGunner`
- `Assets/Rifle_27A2_Pro`
- `Assets/Weapons Pro Pack`
- `Assets/PureNature`
- `Assets/Oculus`
- `Assets/Rabbit312319_Enemy`
- `Assets/SpearAndHalberdAnimset`
- `Assets/Allsky`
- `Assets/GabrielAguiarProductions`
- `Assets/YummyGames`
- `Assets/3D Gamekit - Environment Pack`
- 任何看起来像商业资源包或版权 IP 的目录。

## 推荐的公开仓库结构

推荐先公开：

```text
Assets/
  SubspaceHunter/Script/
  SubspaceHunter/Scenes/Script/
  PublicDemo/PublicScenes/
  Resources/Configs/
Packages/
ProjectSettings/
docs/
```

`Assets/PublicDemo/PublicScenes/` 目前因为是重要项目内容，暂时通过 Git LFS 纳入公开仓库。这个状态只是过渡方案，不是长期目标。长期发布架构见 `docs/EXTERNAL_ASSET_PACKAGES.zh-CN.md`，当前场景依赖审计见 `docs/PUBLIC_DEMO_DEPENDENCIES.zh-CN.md`。

可选或受限资源应替换为占位资源、移动到单独的私有归档，或在文档中说明导入步骤。

## 首次推送 GitHub 前检查

1. 运行：

   ```powershell
   git lfs install
   ```

2. 确认 `.gitattributes` 已经先于大文件提交。

3. 检查超过 50 MiB 的文件：

   ```powershell
   Get-ChildItem -Recurse -File | Where-Object { $_.Length -gt 50MB } | Sort-Object Length -Descending
   ```

4. 检查密钥和凭据：

   ```powershell
   rg -n "apiKey|API_KEY|secret|password|Authorization|sk-" Assets Packages ProjectSettings
   ```

5. 发布前在另一个路径做一次干净 clone 测试。
