# 部署文档

这份文档面向 `dewey778899/new-api` 这个仓库本身，部署时直接从这个仓库拉取源码，而不是拉官方预构建镜像。

## 1. 前置条件

- Git
- Docker Desktop 或 Docker Engine
- 可用的 `3000` 端口

## 2. 拉取仓库

```bash
git clone https://github.com/dewey778899/new-api.git
cd new-api
```

## 3. 使用源码构建并启动

仓库里已经提供了源码部署用的 `docker-compose.source.yml`。

首次部署前，建议先把 `SESSION_SECRET` 改成你自己的随机字符串：

```yaml
SESSION_SECRET: change-this-session-secret
```

然后执行：

```bash
docker compose -f docker-compose.source.yml up -d --build
```

## 4. 访问地址

启动完成后访问：

```text
http://localhost:3000
```

## 5. 数据目录

默认数据会落在仓库根目录的 `data/` 下：

- `data/one-api.db`：SQLite 数据库
- 其他运行时文件也会保存在这里

因此升级代码时，只要保留 `data/` 目录，数据就不会丢。

## 6. 更新部署

```bash
git pull
docker compose -f docker-compose.source.yml up -d --build
```

## 7. 停止服务

```bash
docker compose -f docker-compose.source.yml down
```

## 8. 说明

- 这个仓库当前默认前端主题已经切到 `default`，也就是新版前端样式。
- 如果你后续要反向代理到域名，直接把外部流量转发到容器的 `3000` 端口即可。
- 如果你要改成 MySQL 或 PostgreSQL，可以在此基础上继续补数据库服务和 `SQL_DSN` 环境变量。
