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

## 切换国内镜像源

如果拉取镜像慢，编辑 `.env` 文件，注释 Docker Hub 行，取消阿里云 ACR 注释：

```env
# Docker Hub (国外)
# DOCKER_REGISTRY=ccgogogo/

# 阿里云 ACR (国内)
DOCKER_REGISTRY=registry.cn-hangzhou.aliyuncs.com/hahayykx/
```

## 功能

- 项目管理（创建/删除）
- 图片上传 + 自动标注（YOLO / Grounding DINO 开放词汇）
- 手动标注工具
- 模型训练（后台异步，支持 CPU/GPU）
- 模型测试（上传图片验证效果）
- 算法流水线（目标检测、跟踪、区域入侵、绊线检测、人群密度、边缘检测、颜色识别）
- 模型编译部署（ONNX → BM1684X BModel）

## 数据存储

所有数据保存在 `./data` 目录，删除容器不丢数据。

## 停止/更新

```bash
docker compose down          # 停止
docker compose pull          # 拉取最新镜像
docker compose up -d         # 重新启动
```
