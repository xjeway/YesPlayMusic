## 1. 实现
- [x] 1.1 拉取 `qier222/YesPlayMusic` 与 `ZSXB2468/YesPlayMusic` 的 `master`，确认对比范围内提交列表
- [x] 1.2 仅同步非文档提交（跳过 `docs:` / `README.md` 等），并记录被跳过的提交与原因（已跳过 `f55a256 docs: 更新 README.md`，原因：文档类变更不在本次同步范围）
- [x] 1.3 应用“移除自动打卡”变更：删除 `scrobble` API 与调用点，确保无残留引用
- [x] 1.4 应用“移除自动签到”变更：删除 `dailySignin` API 与调用点，确保无残留引用
- [x] 1.5 应用 CI 相关变更：同步 `build.yaml`、新增 `nightly.yaml`、同步 `vue.config.js` 的构建目标切换逻辑
- [x] 1.6 处理冲突：优先保持与对比分支一致；若必须偏离，给出中文原因与替代方案（`build.yaml` 冲突已通过选择对比分支版本解决）

## 2. 验证
- [x] 2.1 本地执行 `yarn lint`（若项目已配置）（已通过 `npm run lint` 执行；当前仓库存在既有 lint 错误，未在本次同步中处理）
- [x] 2.2 本地执行一次构建（至少 `yarn build` 或 `yarn electron:build` 其一，按项目现状选择）（已通过 `NODE_OPTIONS=--openssl-legacy-provider npm run build` 构建通过；当前环境 Node 版本较新，需要该参数绕过 OpenSSL 兼容问题）
- [x] 2.3 检查 CI 配置文件语法（YAML）与关键环境变量开关是否正确生效

## 3. 交付
- [x] 3.1 输出同步摘要：包含新增/修改文件列表、关键行为变化、以及被忽略的文档类变更说明（中文）
