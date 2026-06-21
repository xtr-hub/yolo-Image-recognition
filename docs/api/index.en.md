# API Documentation

[![中文](https://img.shields.io/badge/中文-API%20文档-red?style=flat-square)](index.md)
[![English](https://img.shields.io/badge/English-API%20Documentation-red?style=flat-square)](index.en.md)

## Health Check

```
GET /health
```

Check service running status, returns model info, device info, and performance statistics.

**Response Example:**
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

## Image Detection

```
POST /api/v1/detect
Content-Type: multipart/form-data

Parameters:
- file: Image file (JPG, PNG, BMP)
- classes: Classes to detect, comma-separated, e.g., 'person' or 'person,car'
- conf_threshold: Confidence threshold (0.1-0.9), default 0.5
```

**Response Example:**
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

## Video Detection

```
POST /api/v1/video
Content-Type: multipart/form-data

Parameters:
- file: Video file (MP4, AVI, MOV, MKV)
- return_video: Whether to return processed video file ("true" or "false", default "true")
- classes: Classes to detect, comma-separated
- use_batch_processing: Whether to use batch processing optimization (default true)
- batch_size: Batch size (1-32, default 8)
- frame_interval: Frame processing interval (1=process every frame, 2=process every other frame, default 1)

Returns: Detection result JSON or processed video file
```

**Response Example (JSON):**
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

## Video Detection (Tracking Mode)

Uses YOLO official tracking API for cross-frame object tracking and unique object counting:

```python
result = detector.process_video_file_track(
    video_path,
    output_path,
    classes=['person'],
    conf=0.5
)
```

**Return Value Includes:**
- `class_counts`: Count of each class detected
- `frames`: Detection results for each frame

---

## Batch Image Detection

```
POST /api/v1/batch/detect
Content-Type: multipart/form-data

Parameters:
- image_files: List of image files
- classes: Classes to detect, comma-separated
- max_workers: Maximum worker threads (1-10)
- batch_size: Batch size (1-100)
```

**Response Example:**
```json
{
  "success": true,
  "total_processed": 10,
  "failed_count": 0,
  "results": [{...}, {...}]
}
```

---

## WebSocket Real-time Detection

```
WS /ws/detect
```

Supports real-time image frame detection, suitable for camera real-time detection scenarios.

**Transport Format:** Pure binary transmission, no base64 encoding overhead

**Message Format:**
- **Input (Client→Server)**: JPEG binary data (Blob/ArrayBuffer)
- **Output (Server→Client)**: Sent in two parts:
  1. JSON metadata (detection results)
  2. JPEG binary data (annotated image)

**JSON Metadata Format:**
```json
{
  "success": true,
  "object_count": 2,
  "objects": [...],
  "inference_time_ms": 45.2,
  "has_image": true
}
```

**Performance Benefits:**
- ~33% reduction in data size compared to base64 encoding
- No encoding/decoding CPU overhead, lower latency
