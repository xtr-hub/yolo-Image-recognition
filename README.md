# YOLO 物体识别服务

基于 YOLOv8 的物体检测 Web 服务，提供图片、视频和实时摄像头的物体检测，支持 COCO 数据集 80 种常见类别。

[![Quick Start](https://img.shields.io/badge/Quick%20Start-%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B-blue?style=flat-square)](docs/guides/quick-start.md)
[![API](https://img.shields.io/badge/API-%E6%8E%A5%E5%8F%A3%E6%96%87%E6%A1%A3-green?style=flat-square)](docs/api/index.md)
[![COCO](https://img.shields.io/badge/COCO-%E7%B1%BB%E5%88%AB%E5%88%97%E8%A1%A8-orange?style=flat-square)](docs/reference/coco-classes.md)
[![FAQ](https://img.shields.io/badge/FAQ-%E6%95%85%E9%9A%9C%E6%8E%92%E9%99%A4-yellow?style=flat-square)](docs/reference/faq.md)
[![English](https://img.shields.io/badge/English-Documentation-red?style=flat-square)](README.en.md)

## 核心功能

- **图片检测**：上传图片快速识别物体，支持 80 种类别筛选
- **视频检测**：上传视频文件，输出带标注的检测视频
- **视频追踪**：使用 YOLO 官方追踪 API，支持跨帧物体追踪和唯一计数
- **批量检测**：多张图片批量处理，提升检测效率
- **WebSocket 实时检测**：纯二进制传输，支持摄像头实时检测
- **Web 界面**：PWA 支持，可视化操作，可自定义类别和模型

## 技术栈

| 技术 | 用途 |
| --- | --- |
| Python 3.8+ | 开发语言 |
| FastAPI | 高性能 Web 框架 |
| Ultralytics YOLOv8 | 目标检测模型 |
| OpenCV | 图像/视频处理 |
| WebSocket | 实时通信（二进制传输） |
| imageio | 视频编解码 |
| PyTorch | 深度学习框架 |

## 快速开始

```bash
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

访问 `http://localhost:8000` 使用 Web 界面，详见 [快速开始](docs/guides/quick-start.md)。

## 项目结构

```
opencv_api/
├── app/
│   ├── api/routes.py          # API 路由
│   ├── core/config.py          # 配置模块
│   ├── models/detector.py      # 检测模型
│   ├── utils/batch_processor.py # 批处理器
│   └── main.py                 # 应用入口
├── static/
│   ├── index.html              # Web 界面
│   └── manifest.json           # PWA 配置
├── docs/                       # 文档
│   ├── api/index.md            # API 文档
│   ├── guides/quick-start.md   # 快速开始
│   └── reference/              # 参考资料
├── test_api.py
└── requirements.txt
```

## 许可证

本项目遵循开源许可证，详见 [LICENSE](./LICENSE) 文件。
