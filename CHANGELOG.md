# 更新日志

所有重要的项目变更都会记录在此文件中。

格式基于 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.0.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [未发布]

### 计划中
- 支持更多云盘平台（阿里云盘、百度网盘等）
- 移动端适配优化
- 
## [1.0.10] - 2025-11-23
-  修复了远程端口转发导致的链接不到后端API
   
## [1.0.0] - 2025-11-22

### 新增
- 🎉 首个正式版本发布
- ✨ 完整的用户认证系统
  - JWT身份验证
  - Cookie加密存储
  - 会话管理
- 📁 115网盘深度集成
  - 扫码登录支持
  - 文件管理（删除、重命名）
  - 离线下载功能
  - 分享管理
  - 批量操作
- 🎬 影视资源管理
  - 资源添加
  - TMDB信息自动获取

- 📱 通知系统
  - Telegram Bot集成
  - 微信通知支持（企业微信）
  - 多种事件通知
- 📊 日志系统
  - 多级别日志记录
  - 日志查询和筛选
  - 日志导出功能
  - 自动日志轮转
- 🔐 安全特性
  - 密码加密存储
  - API访问限流
  - CORS配置
  - 错误追踪
- 🐳 Docker支持
  - 多阶段构建
  - 数据持久化
  - 一键部署
  - 健康检查
- 💾 数据库管理
  - SQLite数据库
  - 自动备份
  - 数据恢复
  - 数据库优化
- 🎨 用户界面
  - Vue 3 + Element Plus
  - 响应式设计
  - 深色模式支持
  - 实时数据更新

### 技术栈
- **前端**: Vue 3, Element Plus, Pinia, Vue Router
- **后端**: Node.js, Express, Better-SQLite3
- **认证**: JWT, bcryptjs
- **工具**: Vite, Docker, PM2

### 系统要求
- Node.js >= 18.0.0
- Docker >= 20.10 (可选)
- 磁盘空间 >= 2GB

---

## 版本说明

### 版本号格式: MAJOR.MINOR.PATCH

- **MAJOR**: 重大更新，可能包含不兼容的API变更
- **MINOR**: 新增功能，向后兼容
- **PATCH**: Bug修复，向后兼容



   # Docker部署
   docker-compose pull
   docker-compose up -d
   

## 已知问题

### v1.0.0

- 移动端部分页面需要优化



## 贡献者

感谢所有为项目做出贡献的开发者！

## 反馈

如有问题或建议，请：
- 提交 [Issue](https://github.com/xiaozhizy1/television-resource-system/issues)
- 发送邮件至: xiaozhizy1@gmail.com

---


最后更新: 2025-11-22

