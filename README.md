# 深港拼车 · 自用副本（sgy_offline）

  > ⚠️ **不是线上项目，是作者自用副本。**
  > 来源：主项目 sgy 的 `777c198` 快照 —— 删掉站内聊天室之前的那一版。
  > 用途：自己玩，**不参与提审**（带聊天室提审会原样撞回「社交-笔记」，见主仓库 ADR-0017）。
  > **别与主项目互拷文件** —— 两份 db.js 的管理员 openid 必须不同（openid 按 appid 生成）。

  ## 固定配置（副本专属）
  - appid：wx63a58f0163082859
  - 云环境：cloud1-d0giflnre1f5a6f54（写在 miniprogram/app.js 的 env）
  - 管理员 openid：osIpe7HUcD4FWqwhknrTCtw2elEI（cloudfunctions/rides/db.js 的 ADMIN_OPENIDS）
  - 增强编译：**关**（project.config.json 的 "enhance": false）

  ## 两个坑（都踩过，别再踩）
  1. **enhance: true + 数组解构 ⇒ 页面白屏**。本副本源自
  777c198，早于主项目的修复（2d9b2ef）。所以这里关了增强编译。若哪天又打开，必须先把
  miniprogram/pages/ride/ride.js、miniprogram/pages/create/create.js 那 3 处数组解构改成取下标。
  2. **换 appid ⇒ openid 会变**。同一个人在新 appid 下是另一个 openid；ADMIN_OPENIDS 不换，「我的」页就没有管理员入口。

  ## 首次跑起来（四步）
  1. 右键 cloudfunctions → 选择云环境 → cloud1-d0giflnre1f5a6f54
  2. 依次上传并部署 rides / routeInit / rideSweep —— 三个都要勾「云端安装依赖」
  3. 控制台 → 云函数 → routeInit → 云端测试 → 参数 {} → 运行（建 8 个集合 + 写 7 条线路）
  4. 打开小程序 → 注册 → 即可发局 / 加入 / 进聊天室

  **验收**：找局页不报"加载失败" · 「我的」页出现管理员入口 · 聊天室能发文字和图片。

  ## 版本与日志
  - 版本号**另起一套**（如 0.1.x），别沿用主项目的 0.5.0。
  - 提交信息沿用 feat：/ fix：/ docs： 前缀，一句话说清改了什么、为什么。
  - 应用内「近期更新」在 miniprogram/pages/profile/profile.js 的 CHANGELOG，发版时手动加一行。