## ADDED Requirements

### Requirement: 禁止自动触发网易云账号敏感写操作
应用 MUST NOT 在后台自动触发可能影响账号状态或风控的写操作接口（例如自动签到、听歌打卡），除非由用户明确操作触发并在 UI 中可感知。

#### Scenario: 播放歌曲不再自动打卡
- **WHEN** 用户正常播放歌曲并产生播放进度/播放完成事件
- **THEN** 应用不会调用 `scrobble`（听歌打卡）相关接口

#### Scenario: 日常任务不再自动签到
- **WHEN** 应用执行 `dailyTask()` 或类似的周期性任务
- **THEN** 应用不会调用 `dailySignin`（每日签到）相关接口

