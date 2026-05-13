# 快速开始

## 环境准备

确保已安装 Python 3.8 或更高版本，并安装依赖：

```bash
pip install -r requirements.txt
```

## 启动服务

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

服务启动后，访问 `http://localhost:8000` 即可使用 Web 界面。

## Web 界面功能

- **图片检测模式**：上传图片并查看检测结果
- **摄像头模式**：实时检测摄像头画面中的物体
- **视频模式**：上传视频文件，处理后下载标注视频
- **实时统计**：显示检测物体数量、推理时间等信息
- **类别选择**：可选择检测特定类别的物体
- **置信度调节**：可调整检测置信度阈值
- **PWA 支持**：可添加到主屏幕作为独立应用使用

## 配置选项

### 环境变量

| 变量 | 说明 | 默认值 |
|------|------|--------|
| `YOLO_MODEL` | 指定使用的 YOLO 模型 | `yolov8n` |

可用模型：
- `yolov8n.pt`: nano 版本，最快但精度最低
- `yolov8s.pt`: small 版本，速度与精度平衡
- `yolov8m.pt`: medium 版本，较慢但精度更高
- `yolov8l.pt`: large 版本，较慢但精度很高
- `yolov8x.pt`: extra-large 版本，最慢但精度最高

### 配置文件 (app/core/config.py)

```python
BATCH_PROCESSING = {
    "default_max_workers": 4,
    "default_batch_size": 10,
    "max_batch_size": 100,
    "max_workers": 10,
    "memory_threshold": 80,  # 内存使用阈值百分比
}
```

## 部署

### 生产环境

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --workers 4
```

### HTTPS

```bash
uvicorn app.main:app --host 0.0.0.0 --port 443 --ssl-keyfile ./key.pem --ssl-certfile ./cert.pem
```

> 注意：HTTPS 环境下摄像头功能才能正常工作。
