# API 文档

## 健康检查

```
GET /health
```

检查服务运行状态，返回模型信息、设备信息和性能统计。

**响应示例：**
```json
{
  "status": "healthy",
  "model_loaded": true,
  "device": "cuda",
  "batch_processing_enabled": true,
  "supported_classes": ["person", "bicycle", "car", ...],
  "performance_stats": {...}
}
```

---

## 图片检测

```
POST /api/v1/detect
Content-Type: multipart/form-data

参数：
- file: 图片文件 (JPG, PNG, BMP)
- classes: 要检测的类别，逗号分隔，例如 'person' 或 'person,car'
- conf_threshold: 置信度阈值 (0.1-0.9)，默认 0.5
```

**响应示例：**
```json
{
  "success": true,
  "object_count": 2,
  "objects": [
    {
      "bbox": { "x1": 100, "y1": 50, "x2": 200, "y2": 300, "width": 100, "height": 250 },
      "confidence": 0.95,
      "class_id": 0,
      "class_name": "person"
    }
  ],
  "inference_time_ms": 45.2,
  "image_shape": { "height": 480, "width": 640 },
  "annotated_image": "data:image/jpeg;base64,..."
}
```

---

## 视频检测

```
POST /api/v1/video
Content-Type: multipart/form-data

参数：
- file: 视频文件 (MP4, AVI, MOV, MKV)
- return_video: 是否返回处理后的视频文件 ("true" 或 "false", 默认 "true")
- classes: 要检测的类别，逗号分隔
- use_batch_processing: 是否使用批处理优化 (默认 true)
- batch_size: 批处理大小 (1-32，默认 8)
- frame_interval: 帧处理间隔 (1=每帧处理，2=隔帧处理，默认 1)

返回：检测结果 JSON 或处理后的视频文件
```

**响应示例 (JSON)：**
```json
{
  "total_frames": 150,
  "processed_frames": 150,
  "fps": 30.0,
  "duration": 5.0,
  "resolution": { "width": 1920, "height": 1080 },
  "frames_with_detection": 23,
  "frames": [
    { "frame": 10, "timestamp": 0.33, "object_count": 1, "objects": [...] }
  ]
}
```

---

## 视频检测（追踪模式）

使用 YOLO 官方追踪 API，支持跨帧物体追踪和唯一物体计数：

```python
result = detector.process_video_file_track(
    video_path,
    output_path,
    classes=['person'],
    conf=0.5
)
```

**返回值包含：**
- `class_counts`: 各类别的出现次数
- `frames`: 每帧的检测结果

---

## 批量图片检测

```
POST /api/v1/batch/detect
Content-Type: multipart/form-data

参数：
- image_files: 图片文件列表
- classes: 要检测的类别，逗号分隔
- max_workers: 最大工作线程数 (1-10)
- batch_size: 批处理大小 (1-100)
```

**响应示例：**
```json
{
  "success": true,
  "total_processed": 10,
  "failed_count": 0,
  "results": [{...}, {...}]
}
```

---

## WebSocket 实时检测

```
WS /ws/detect
```

支持实时图像帧检测，适用于摄像头实时检测场景。

**传输格式：** 纯二进制传输，无 base64 编码开销

**消息格式：**
- **输入（前端→后端）**：JPEG 二进制数据（Blob/ArrayBuffer）
- **输出（后端→前端）**：分两次发送
  1. JSON 元数据（检测结果）
  2. JPEG 二进制数据（标注后的图片）

**JSON 元数据格式：**
```json
{
  "success": true,
  "object_count": 2,
  "objects": [...],
  "inference_time_ms": 45.2,
  "has_image": true
}
```

**性能优势：**
- 相比 base64 编码，数据量减少约 33%
- 无编解码 CPU 开销，延迟更低
