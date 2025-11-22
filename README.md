# Television Resource System (TRS)

一个基于 Vue 3 + Express 的影视资源管理系统,支持115网盘集成、TMDB影视信息获取、自动化任务调度等功能。

## ✨ 主要功能

- 🎬 **影视资源管理** - 支持电影、电视剧资源的统一管理
- 📁 **115网盘集成** - 集成115网盘
- 🎯 **TMDB集成** - 自动获取影视作品的详细信息、海报、评分等
- 📱 **Telegram Bot** - 支持通过Telegram机器人进行远程管理
- 💬 **微信通知** - 支持微信消息推送通知
- ⏰ **任务调度** - 支持定时任务和自动化工作流
- 🔐 **安全认证** - JWT身份验证,Cookie加密存储
- 📊 **日志系统** - 完整的操作日志和错误追踪
- 🐳 **Docker支持** - 一键部署,开箱即用

## 🚀 快速开始

### 使用 Docker 部署（推荐）

1. **克隆配置文件**
```bash
# 下载 docker-compose.example.yml
wget https://raw.githubusercontent.com/your-repo/TRS/main/docker-compose.example.yml -O docker-compose.yml


2. **启动服务**
```bash
docker-compose up -d
```

3. **访问系统**
- 前端地址: http://localhost:6100
- 后端API: http://localhost:6101
- 默认账号: admin / admin123 (首次登录后请修改密码)

### 手动部署

详细的手动部署步骤请参考 [部署指南](./docs/DEPLOYMENT.md)

## 📋 系统要求

- Node.js >= 18.0.0
- Docker >= 20.10 (使用Docker部署时)
- 磁盘空间 >= 2GB (用于数据库和日志)


## 📖 使用教程

详细的使用教程请参考 [用户手册](./docs/USER_GUIDE.md)


## 🛠️ 故障排查

### Docker镜像拉取失败

如果遇到Docker镜像拉取失败,请参考 [Docker镜像源配置指南](./DOCKER-MIRROR-FIX.md)


### 更多问题

请查看 [常见问题](./docs/FAQ.md) 或提交 Issue

## 📝 更新日志

查看 [CHANGELOG.md](./CHANGELOG.md) 了解版本更新内容

## 🤝 贡献

欢迎提交 Issue 和 Pull Request!

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](./LICENSE) 文件

## ⚠️ 免责声明

本项目仅供学习交流使用,请勿用于非法用途。使用本项目所产生的一切后果由使用者自行承担。


## 🙏 致谢

感谢以下开源项目:

- [Vue.js](https://vuejs.org/)
- [Element Plus](https://element-plus.org/)
- [Express](https://expressjs.com/)
- [TMDB](https://www.themoviedb.org/)

---

⭐ 如果这个项目对你有帮助,请给个Star支持一下!