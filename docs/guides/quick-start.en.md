# Quick Start

[![中文](https://img.shields.io/badge/中文-快速开始-red?style=flat-square)](quick-start.md)
[![English](https://img.shields.io/badge/English-Quick%20Start-red?style=flat-square)](quick-start.en.md)

## Environment Preparation

Ensure Python 3.8 or higher is installed, and install dependencies:

```bash
pip install -r requirements.txt
```

## Start the Service

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

After the service starts, visit `http://localhost:8000` to use the web interface.

## Web Interface Features

- **Image Detection Mode**: Upload images and view detection results
- **Camera Mode**: Real-time detection of objects in camera feed
- **Video Mode**: Upload video files, process and download annotated videos
- **Real-time Statistics**: Display detection count, inference time and other information
- **Class Selection**: Option to detect specific classes of objects
- **Confidence Adjustment**: Adjust detection confidence threshold
- **PWA Support**: Can be added to home screen as standalone application

## Configuration Options

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `YOLO_MODEL` | Specify YOLO model to use | `yolov8n` |

Available models:
- `yolov8n.pt`: nano version, fastest but lowest accuracy
- `yolov8s.pt`: small version, balanced speed and accuracy
- `yolov8m.pt`: medium version, slower but higher accuracy
- `yolov8l.pt`: large version, slower but much higher accuracy
- `yolov8x.pt`: extra-large version, slowest but highest accuracy

### Configuration File (app/core/config.py)

```python
BATCH_PROCESSING = {
    "default_max_workers": 4,
    "default_batch_size": 10,
    "max_batch_size": 100,
    "max_workers": 10,
    "memory_threshold": 80,  # Memory usage threshold percentage
}
```

## Deployment

### Production Environment

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000 --workers 4
```

### HTTPS

```bash
uvicorn app.main:app --host 0.0.0.0 --port 443 --ssl-keyfile ./key.pem --ssl-certfile ./cert.pem
```

> Note: Camera functionality works properly only under HTTPS environment.
