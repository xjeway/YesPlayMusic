# Change: 同步 `ZSXB2468/YesPlayMusic` 非文档变更（移除自动签到/打卡，完善 CI）

## Why
上游对比 `qier222/YesPlayMusic:master...ZSXB2468/YesPlayMusic:master` 包含若干与账号安全和 CI 构建相关的实质性变更。当前仓库需要同步这些非文档类修改，以降低因自动化账号操作导致的封号风险，并让 GitHub Actions 构建配置与分支保持一致。

## What Changes
- 移除“听歌打卡（scrobble）”的自动上报逻辑，避免在用户未明确授权/触发时向接口写入行为数据。
- 移除“每日签到（dailySignin）”的自动执行逻辑，避免后台自动触发签到请求。
- 同步 GitHub Actions 构建配置：
  - Release workflow 仅在 tag（`v*`）触发，调整产物上传规则与多平台依赖安装。
  - 增加 Nightly workflow（`test_build` 分支）用于测试构建。
  - `vue.config.js` 根据 `GITHUB_ACTIONS_BUILD` / `NIGHTLY_BUILD` 环境变量切换 electron-builder 的构建目标矩阵。
- **排除** 文档类变更（例如 `README.md` 更新）。

## Impact
- Affected code:
  - `src/utils/Player.js`：移除播放完成/播放进度的打卡上报调用。
  - `src/api/track.js`：移除 `scrobble` API 封装。
  - `src/api/user.js`：移除 `dailySignin` API 封装。
  - `src/utils/common.js`：移除 `dailyTask()` 中的自动签到逻辑。
  - `.github/workflows/build.yaml`、新增 `.github/workflows/nightly.yaml`：CI 构建与产物上传调整。
  - `vue.config.js`：根据 CI 环境变量调整构建目标。
- Risk:
  - CI 行为改变（触发条件、产物命名/路径）可能影响现有发布流程；需在合并后通过一次手动触发或 tag 验证。
  - 自动签到/打卡相关的依赖调用被移除，若下游代码仍引用对应函数，需要确保编译期即可发现并修复引用。

