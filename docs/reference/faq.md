# 故障排除

[![中文](https://img.shields.io/badge/中文-故障排除-red?style=flat-square)](faq.md)
[![English](https://img.shields.io/badge/English-Troubleshooting-red?style=flat-square)](faq.en.md)

## 常见问题

### 模型下载失败

检查网络连接，或手动下载模型文件至项目根目录：
- 下载地址：https://github.com/ultralytics/assets/releases

### 摄像头权限问题

确保浏览器已授权访问摄像头，HTTPS 环境下才能使用摄像头。

### 视频处理失败

检查视频格式支持情况（MP4, AVI, MOV, MKV）及磁盘空间。

### 内存不足

降低批处理大小或增加 `memory_threshold` 配置。

### WebSocket 连接失败

检查防火墙设置和代理配置。

## 性能优化建议

- **GPU 加速**：在支持 CUDA 的机器上运行，推理速度提升 10-50 倍
- **模型选择**：根据场景选择合适的模型，实时场景推荐 yolov8n/yolov8s
- **批处理**：批量检测时使用批处理优化，提升吞吐量
- **视频帧间隔**：适当增加 `frame_interval` 可减少处理时间
- **内存管理**：系统自动监控内存使用，动态调整批处理大小
