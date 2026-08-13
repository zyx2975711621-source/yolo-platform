# YOLO 训练平台

一键部署的 YOLO 深度学习训练平台，支持目标检测、自动标注、模型训练、视频分析、边缘端编译部署。

## 快速开始

**前置条件**：安装 [Docker Desktop](https://www.docker.com/products/docker-desktop/)（版本 ≥ 20.10）

```bash
# CPU 模式（默认，所有机器可用）
docker compose up -d

# GPU 模式（需要 NVIDIA 显卡 + nvidia-container-toolkit）
docker compose --profile gpu up -d

# 打开浏览器访问
# http://localhost:8000
```

> 首次启动会自动拉取 mysql、平台、TPU-MLIR 编译服务三个镜像，共约 20+ GB，需下载一段时间。

## 功能

- 项目管理（创建/删除）
- 图片上传 + 自动标注（YOLO / Grounding DINO 开放词汇）
- 手动标注工具
- 模型训练（后台异步，支持 CPU/GPU）
- 模型测试（上传图片验证效果）
- 算法流水线（目标检测、跟踪、区域入侵、绊线检测、人群密度、边缘检测、颜色识别）
- 模型编译部署（ONNX → BM1684X BModel，内置 TPU-MLIR 编译服务，开箱即用）

## 数据存储

所有数据保存在 `./data` 目录 + `mysql_data` 数据卷，删除容器不丢数据（不要用 `docker compose down -v`，会清空数据库）。

## 更新

```bash
docker compose down          # 停止
docker compose pull          # 拉取最新镜像
docker compose up -d         # 重新启动（数据不丢）
```

## 常见问题

- **编译一直等待/超时**：确认编译服务在运行 —— `docker compose ps` 查看 `yolo-tpu-compile`，日志 `docker compose logs tpu-compile`。
- **端口被占用**：改 `docker-compose.yml` 里 `ports` 左边的端口号（如 `8000:8000` → `8080:8000`）。
