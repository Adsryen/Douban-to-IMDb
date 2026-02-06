# Douban to IMDb

<div align="center">

![Version](https://img.shields.io/badge/version-2026.02.07-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Tampermonkey](https://img.shields.io/badge/Tampermonkey-Compatible-orange.svg)

一个自动将豆瓣电影评分同步到 IMDb 的用户脚本

[功能特性](#功能特性) • [安装方法](#安装方法) • [使用说明](#使用说明) • [配置选项](#配置选项) • [常见问题](#常见问题)

</div>

---

## 📖 简介

Douban to IMDb 是一个强大的浏览器用户脚本，可以帮助你轻松地将豆瓣上的电影评分自动同步到 IMDb。支持批量同步、自动评分、添加到 Watchlist 等功能。

### 🎯 项目初衷

本项目最初是为了解决**豆瓣到 Trakt 的数据同步问题**而创建的。由于豆瓣和 Trakt 之间没有直接的数据对接，而 IMDb 作为全球最大的电影数据库，与 Trakt 有良好的集成支持。因此，通过将豆瓣数据先同步到 IMDb，再利用 Trakt 的 IMDb 导入功能，就可以实现**豆瓣 → IMDb → Trakt** 的完整数据迁移链路。

**使用场景：**
- 🔄 将豆瓣观影记录迁移到 Trakt
- 📊 在 Trakt 上统一管理多平台的观影数据
- 🌐 利用 Trakt 的跨平台同步能力（Plex、Kodi、Infuse 等）
- 📱 通过 Trakt 在各种设备和应用间同步观影进度

### ✨ 功能特性

- 🎯 **一键同步** - 在豆瓣"我看过的电影"页面，每部电影旁边会显示同步按钮
- ⚡ **批量同步** - 支持批量同步当前页或所有页面的电影
- 🎬 **双重目标** - 可选择同步到 IMDb 已看（评分）或想看（Watchlist）
- 📊 **实时进度** - 美观的进度面板，实时显示同步状态
- 🔄 **智能评分** - 自动将豆瓣 5 星评分转换为 IMDb 10 分制
- 🎨 **现代界面** - 精美的 UI 设计，流畅的动画效果
- 🔗 **资源链接** - 在豆瓣电影详情页添加下载和字幕资源链接
- 🌐 **双向跳转** - 在 IMDb 页面添加豆瓣链接，方便双向查看

## 🚀 安装方法

### 前置要求

1. 安装浏览器扩展管理器（任选其一）：
   - [Tampermonkey](https://www.tampermonkey.net/) （推荐）
   - [Greasemonkey](https://www.greasespot.net/)
   - [Violentmonkey](https://violentmonkey.github.io/)

### 安装脚本

1. 点击下方链接安装脚本：
   - [从 Greasy Fork 安装（暂未上传）]（推荐）
   - [从 GitHub 安装](https://github.com/Anderson-Ryen/Douban-to-IMDb/raw/main/douban.js)

2. 在弹出的页面中点击"安装"按钮

3. 安装完成后，访问豆瓣或 IMDb 即可使用

## 📝 使用说明

### 方法一：单个同步（推荐新手）

1. 打开豆瓣"我看过的电影"页面
2. 每部电影标题后会显示 **"同步(X★)"** 按钮
3. 点击按钮，选择同步目标（已看/想看）
4. 脚本会自动在后台完成同步
5. 同步完成后按钮会变为 **"已同步✓"**

### 方法二：批量同步（推荐老手）

1. 打开豆瓣"我看过的电影"页面
2. 页面右侧会显示两个悬浮按钮：
   - **⚡ 同步本页** - 同步当前页面的所有电影
   - **🚀 同步所有** - 同步从当前页到最后一页的所有电影
3. 点击按钮，选择同步目标
4. 会弹出进度面板，显示实时同步状态
5. 可以随时暂停/继续同步

### 评分转换规则

豆瓣 5 星制会自动转换为 IMDb 10 分制：

| 豆瓣评分 | IMDb 评分 |
|---------|----------|
| ⭐ (1星) | 2 分 |
| ⭐⭐ (2星) | 4 分 |
| ⭐⭐⭐ (3星) | 6 分 |
| ⭐⭐⭐⭐ (4星) | 8 分 |
| ⭐⭐⭐⭐⭐ (5星) | 10 分 |

## ⚙️ 配置选项

脚本提供了丰富的配置选项，可以在 `douban.js` 文件顶部的 `CONFIG` 对象中修改：

```javascript
const CONFIG = {
    MOVIE_SYNC_INTERVAL: 5000,        // 每部电影同步间隔（毫秒）
    PAGE_OPEN_INTERVAL: 20000,        // 每页打开间隔（毫秒）
    AUTO_CLOSE_DELAY: 5000,           // 自动关闭标签页延迟（毫秒）
    TOAST_DURATION: 3000,             // 提示显示时长（毫秒）
    TEST_SYNC_COUNT: 3,               // 测试同步的电影数量
    // ... 更多配置选项
};
```

### 主要配置说明

- `MOVIE_SYNC_INTERVAL` - 控制批量同步时每部电影之间的间隔时间
- `TEST_SYNC_COUNT` - 批量同步时先测试前 N 部电影，成功后再继续
- `FLOAT_BUTTON_RIGHT` - 悬浮按钮距离右侧的距离


## � 与 Trakt 配合使用

如果你的最终目标是将数据同步到 Trakt，可以按照以下步骤操作：

### 完整同步流程

1. **第一步：豆瓣 → IMDb**
   - 使用本脚本将豆瓣评分同步到 IMDb
   - 建议先同步到 IMDb 的"已看"（评分）列表

2. **第二步：IMDb → Trakt**
   - 访问 [Trakt 导入页面](https://trakt.tv/welcome/7)
   - 选择"IMDb Ratings"导入选项
   - 按照 Trakt 的指引完成导入

3. **第三步：验证数据**
   - 在 Trakt 上检查导入的电影数据
   - 确认评分和观看状态是否正确

### 注意事项

- ⏱️ IMDb 到 Trakt 的同步可能需要一些时间，请耐心等待
- 🔄 如果有新的观影记录，重复上述步骤即可增量同步
- ⚠️ 部分冷门电影可能在 IMDb 或 Trakt 上找不到对应条目


## ❓ 常见问题

### Q: 同步失败怎么办？

A: 请检查：
1. 是否已登录 IMDb 账号
2. 网络连接是否正常
3. 浏览器是否允许弹出窗口
4. 尝试减少同步间隔时间

### Q: 为什么有些电影无法同步？

A: 可能的原因：
1. 豆瓣电影页面没有 IMDb ID
2. IMDb 上没有该电影
3. 电影信息不匹配

### Q: 批量同步会不会被 IMDb 限制？

A: 脚本已经设置了合理的同步间隔（默认 5 秒），正常使用不会被限制。如果担心，可以增加 `MOVIE_SYNC_INTERVAL` 的值。

### Q: 可以修改评分吗？

A: 可以。在豆瓣修改评分后，重新点击同步按钮即可更新 IMDb 上的评分。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

### 开发指南

1. Fork 本仓库
2. 创建你的特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交你的改动 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启一个 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 👨‍💻 作者

**ryen** - [Anderson-Ryen](https://github.com/Anderson-Ryen)

## 🙏 致谢

- 感谢豆瓣、IMDb 和 Trakt 提供的优质电影数据服务
- 感谢所有贡献者和用户的支持
- 特别感谢 Trakt 社区提供的数据同步方案灵感

## 📮 联系方式

如有问题或建议，欢迎：
- 提交 [Issue](https://github.com/Anderson-Ryen/Douban-to-IMDb/issues)

---

<div align="center">

**如果这个项目对你有帮助，请给个 ⭐ Star 支持一下！**

Made with ❤️ by ryen

</div>
