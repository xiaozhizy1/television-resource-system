# 常见问题 (FAQ)

本文档收集了用户在使用 Television Resource System (TRS) 过程中经常遇到的问题及解决方案。

## 目录

- [安装部署](#安装部署)
- [登录认证](#登录认证)
- [115网盘](#115网盘)
- [TMDB配置](#tmdb配置)
- [性能问题](#性能问题)
- [数据库问题](#数据库问题)
- [Docker相关](#docker相关)
- [其他问题](#其他问题)

## 安装部署

### Q: Docker镜像拉取失败怎么办？

**A:** 这通常是因为网络问题或Docker镜像源问题。解决方法：

1. 配置Docker镜像加速器（推荐）：
```bash
# 编辑Docker配置
sudo nano /etc/docker/daemon.json

# 添加以下内容
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://hub-mirror.c.163.com"
  ]
}

# 重启Docker
sudo systemctl restart docker
```

2. 或者使用代理：
```bash
# 设置代理
export HTTP_PROXY=http://your-proxy:port
export HTTPS_PROXY=http://your-proxy:port

# 拉取镜像
docker-compose pull
```

详见 [Docker镜像源配置指南](../DOCKER-MIRROR-FIX.md)

### Q: 端口被占用怎么办？

**A:** 修改端口配置：

如果使用Docker，还需修改 `docker-compose.yml`：
```yaml
ports:
  - "6200:6100"  # 前端端口
  - "6201:6101"  # 后端端口
```


## 登录认证

### Q: 忘记管理员密码怎么办？

**A:** 使用重置密钥重置密码：

1. 查看重置密钥：
```bash
# Docker部署
cat config/reset_key.txt

2. 在登录页面点击"忘记密码"
3. 输入重置密钥
4. 密码将重置为默认密码 `admin123`
5. 登录后立即修改密码

### Q: JWT Token过期怎么办？

**A:** Token过期是正常的安全机制：

- 默认有效期：7天
- 过期后需要重新登录
- 可在 `.env` 中修改有效期：
```env
JWT_EXPIRES_IN=30d  # 改为30天
```

### Q: 如何添加新用户？

**A:** 目前版本暂不支持多用户。

## 115网盘

### Q: 扫码登录失败？

**A:** 可能的原因和解决方法：

1. **二维码过期**：刷新页面重新生成
2. **网络问题**：检查服务器网络连接
3. **115服务异常**：稍后重试
4. **Cookie保存失败**：检查 `config` 目录权限

### Q: Cookie经常过期怎么办？

**A:** 解决方法：

1. 启用自动刷新任务：
   - 进入"任务调度"
   - 创建"115 Cookie刷新"任务
   - 设置每天执行一次

2. 使用更稳定的登录方式：
   - 推荐使用IOS或平板客户端登录
   - 避免频繁切换登录设备


### Q: 离线下载不工作？

**A:** 可能的原因：

1. **资源问题**：
   - 磁力链接无效
   - 资源已失效
   - 种子文件损坏

2. **账号限制**：
   - 检查115账号是否支持离线下载
   - 确认离线下载配额未用完

3. **网络问题**：
   - 115服务器连接异常
   - 检查系统网络设置

## TMDB配置

### Q: 无法获取TMDB数据？

**A:** 排查步骤：

1. **检查API Key**：
   - 确认API Key正确
   - 在TMDB官网验证Key是否有效

2. **网络连接**：
```bash
# 测试连接
curl https://api.themoviedb.org/3/movie/550?api_key=YOUR_API_KEY
```

3. **配置代理**（如果需要）：
```env
HTTP_PROXY=http://your-proxy:port
HTTPS_PROXY=http://your-proxy:port
```

### Q: TMDB搜索结果不准确？

**A:** 优化搜索：

1. 使用更精确的关键词
2. 包含年份信息
3. 使用原始标题搜索
4. 切换语言设置（中文/英文）

### Q: 如何获取TMDB API Key？

**A:** 详细步骤：

1. 访问 https://www.themoviedb.org/
2. 注册并登录账号
3. 进入"设置" > "API"
4. 选择"Request an API Key"
5. 选择"Developer"类型
6. 填写应用信息
7. 同意条款后获取API Key

## 性能问题

### Q: 系统运行缓慢？

**A:** 优化建议：

1. **清理日志**：
```bash
# 手动清理
find config/logs -name "*.log" -mtime +30 -delete

# 或在系统中设置自动清理
```

2. **优化数据库**：
   - 进入"系统管理" > "数据库管理"
   - 点击"优化数据库"

3. **检查资源使用**：
```bash
# Docker部署
docker stats TRS-app

```

4. **增加系统资源**：
   - 建议最低配置：2核CPU + 2GB内存
   - 推荐配置：4核CPU + 4GB内存

### Q: 内存占用过高？

**A:** 解决方法：

1. **重启服务**：
```bash
# Docker
docker-compose restart


3. **检查日志文件大小**：
   - 过大的日志文件会占用内存
   - 定期清理或归档

## 数据库问题

### Q: 数据库锁定错误？

**A:** 解决步骤：

1. **停止服务**：
```bash
docker-compose down

2. **删除锁文件**：
```bash
rm config/database/trs.db-shm
rm config/database/trs.db-wal
```

3. **重启服务**：
```bash
docker-compose up -d


### Q: 如何备份数据库？

**A:** 多种备份方式：


1. **手动备份**：

# 或直接复制
cp config/database/trs.db config/database/trs.db.backup
```

3. **完整备份**：
```bash
tar -czf trs-backup-$(date +%Y%m%d).tar.gz config/
```

### Q: 如何恢复数据库？

**A:** 恢复步骤：

1. **停止服务**
2. **替换数据库文件**：
```bash
cp config/database/trs.db.backup config/database/trs.db
```
3. **重启服务**
4. **验证数据完整性**

## Docker相关

### Q: Docker容器无法启动？

**A:** 排查步骤：

1. **查看日志**：
```bash
docker-compose logs -f TRS
```

2. **检查配置**：
   - 验证 `.env` 文件配置
   - 检查端口是否被占用
   - 确认目录权限正确

3. **重建容器**：
```bash
docker-compose down
docker-compose up -d --force-recreate
```

### Q: 数据持久化失败？

**A:** 检查挂载：

1. **验证挂载配置**：
```yaml
volumes:
  - ./config:/config  # 确保路径正确
```

2. **检查目录权限**：
```bash
sudo chown -R 1000:1000 config
chmod -R 755 config
```

3. **查看挂载状态**：
```bash
docker inspect TRS-app | grep Mounts -A 20
```

### Q: 如何更新Docker镜像？

**A:** 更新步骤：

```bash
# 1. 备份数据
tar -czf config-backup.tar.gz config/

# 2. 停止容器
docker-compose down

# 3. 拉取新镜像
docker-compose pull

# 4. 启动新容器
docker-compose up -d

# 5. 查看日志确认
docker-compose logs -f
```

## 其他问题

### Q: 如何查看系统日志？

**A:** 多种方式：

1. **Web界面**：
   - 进入"系统管理" > "系统日志"

2. **命令行**：
```bash
# Docker
docker-compose logs -f --tail=100 TRS

# 手动部署
tail -f config/logs/app-$(date +%Y-%m-%d).log
```



### Q: 支持哪些浏览器？

**A:** 推荐使用：

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Edge 90+
- ✅ Safari 14+
- ⚠️ IE 不支持

### Q: 如何报告Bug？

**A:** 报告步骤：

1. 访问 [GitHub Issues](https://github.com/your-repo/TRS/issues)
2. 点击"New Issue"
3. 选择Bug报告模板
4. 填写详细信息：
   - 系统版本
   - 操作步骤
   - 预期结果
   - 实际结果
   - 错误日志
   - 截图（如有）
5. 提交Issue

### Q: 如何贡献代码？

**A:** 贡献流程：

1. Fork项目
2. 创建功能分支
3. 提交代码
4. 发起Pull Request
5. 等待审核

详见项目的 CONTRIBUTING.md 文件

## 获取更多帮助

如果以上内容无法解决你的问题：

- 📖 查看 [用户手册](./USER_GUIDE.md)
- 📖 查看 [部署指南](./DEPLOYMENT.md)
- 💬 访问 [讨论区](https://github.com/your-repo/TRS/discussions)
- 🐛 提交 [Issue](https://github.com/your-repo/TRS/issues)
- 📧 发送邮件: support@example.com

---

最后更新: 2025-11-22