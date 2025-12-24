## ADDED Requirements

### Requirement: Release 构建仅在 tag 触发并上传多平台产物
仓库的 GitHub Actions Release workflow SHALL 仅在推送 `v*` tag 或手动触发时运行，并按平台上传对应构建产物。

#### Scenario: 推送版本 tag 触发构建
- **WHEN** 推送形如 `v1.2.3` 的 tag
- **THEN** workflow 在 macOS / Windows / Ubuntu 三个平台执行构建流程

#### Scenario: 产物按平台区分上传
- **WHEN** 构建在 Linux 运行
- **THEN** 上传 `dist_electron/*.rpm`、`dist_electron/*.deb`、`dist_electron/*.AppImage`（若存在）
- **WHEN** 构建在 Windows 运行
- **THEN** 上传 `dist_electron/*.exe`（若存在）
- **WHEN** 构建在 macOS 运行
- **THEN** 上传 `dist_electron/*.dmg`（若存在）

### Requirement: Nightly 构建用于测试分支
仓库 SHALL 提供 Nightly workflow，在 `test_build` 分支推送或手动触发时运行，并上传 nightly 产物以便验证构建可用性。

#### Scenario: 推送 test_build 触发 Nightly
- **WHEN** 推送到 `test_build` 分支
- **THEN** workflow 运行并上传 nightly 产物

### Requirement: CI 环境可切换 electron-builder 构建目标矩阵
构建配置 MUST 根据环境变量切换 electron-builder 的构建目标，以适配 GitHub Actions 与 Nightly 的不同需求。

#### Scenario: GitHub Actions 构建使用精简目标矩阵
- **WHEN** 环境变量 `GITHUB_ACTIONS_BUILD` 为 `true`
- **THEN** 使用面向 CI 的构建目标矩阵（如减少 Windows 目标与架构）

#### Scenario: Nightly 构建使用更精简目标矩阵
- **WHEN** 环境变量 `NIGHTLY_BUILD` 为 `true`
- **THEN** 使用 nightly 目标矩阵（仅保留必要平台/格式用于验证）

