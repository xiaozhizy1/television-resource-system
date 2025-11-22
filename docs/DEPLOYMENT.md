



# 部署指南

本文档详细介绍如何部署 Television Resource System (TRS)。



## Docker 部署（推荐）

### 前置要求

- Docker >= 20.10
- Docker Compose >= 1.29
- 磁盘空间 >= 2GB

### docker-compose 部署

services:
  trs:
    image: xiaozhizy/television-resource-system:latest
    container_name: trs-app
    ports:
      - "6100:6100"  # 前端端口
      - "6101:6101"  # 后端端口
    volumes:
      # 挂载配置目录 - 所有持久化数据都在这里
      - ./config:/config
    environment:
      - NODE_ENV=production
      # 时区设置
      - TZ=Asia/Shanghai
      # 密钥目录
      - SECRETS_DIR=/config
      # 配置文件路径
      - PAN115_COOKIE_FILE=/config/115-cookies.txt
      # 数据库路径
      - DATABASE_PATH=/config/database/trs.db
      # 日志目录
      - LOG_DIR=/config/logs
      # 临时文件目录
      - TEMP_DIR=/config/temp
    restart: unless-stopped
    networks:
      - trs-network

networks:
  trs-network:
    driver: bridge

```

**生成密钥的方法:**

```bash
# 生成 COOKIE_ENCRYPTION_KEY (32字节十六进制)
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"

# 生成 JWT_SECRET (64字节Base64)
node -e "console.log(require('crypto').randomBytes(64).toString('base64'))"

# 生成 SESSION_SECRET
node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
```

**可选配置项:**


# TMDB API配置（用于获取影视信息）
TMDB_API_KEY=your_tmdb_api_key

# 端口配置
PORT=6101  # 后端端口
PORT=6100  # 前端端口


```

# 设置权限
chmod -R 755 config uploads
```

### 步骤 3: 启动服务

```bash
# 拉取镜像并启动
docker-compose up -d

# 查看日志
docker-compose logs -f

# 检查服务状态
docker-compose ps
```

### 步骤 5: 访问系统

- **前端地址**: http://localhost:6100
- **后端API**: http://localhost:6101
- **默认账号**: admin
- **默认密码**: admin123

⚠️ **首次登录后请立即修改密码！**

### Docker 常用命令

```bash
# 停止服务
docker-compose stop

# 启动服务
docker-compose start

# 重启服务
docker-compose restart

# 停止并删除容器
docker-compose down

# 查看日志
docker-compose logs -f TRS

# 进入容器
docker-compose exec TRS sh

# 更新镜像
docker-compose pull
docker-compose up -d
```



### 前置要求

- Node.js >= 18.0.0
- npm >= 9.0.0
- 磁盘空间 >= 2GB


## 故障排查

### 端口被占用

```bash
# 查看端口占用
netstat -tulpn | grep 6100
netstat -tulpn | grep 6101

# 或使用 lsof
lsof -i :6100
lsof -i :6101

# 修改端口


### 数据库锁定

```bash
# 停止服务
docker-compose down  # Docker部署

# 重启服务
docker-compose up -d  # Docker部署


### 权限问题

```bash
# Docker 部署
sudo chown -R 1000:1000 config uploads

```

### 查看详细日志

```bash
# Docker 部署
docker-compose logs -f --tail=100 TRS


## 安全建议

1. **修改默认密码**: 首次登录后立即修改 admin 账号密码
2. **使用 HTTPS**: 生产环境必须启用 SSL/TLS
3. **定期备份**: 设置自动备份任务
4. **更新系统**: 定期更新到最新版本
5. **限制访问**: 使用防火墙限制不必要的端口访问
6. **强密钥**: 使用强随机密钥,不要使用示例值

## 监控和维护


```

### 日志轮转

系统自动进行日志轮转,保留最近 30 天的日志（可配置）。


## 获取帮助

如遇到问题:


1. 查看 [GitHub Issues](https://github.com/your-repo/TRS/issues)
2. 提交新的 Issue

---

更新时间: 2025-11-22
