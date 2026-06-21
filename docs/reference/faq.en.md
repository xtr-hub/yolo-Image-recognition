# Troubleshooting

[![中文](https://img.shields.io/badge/中文-故障排除-red?style=flat-square)](faq.md)
[![English](https://img.shields.io/badge/English-Troubleshooting-red?style=flat-square)](faq.en.md)

## Common Issues

### Model Download Failure

Check network connectivity, or manually download model files to project root directory:
- Download URL: https://github.com/ultralytics/assets/releases

### Camera Permission Issues

Ensure browser has authorized camera access, camera works only under HTTPS.

### Video Processing Failure

Check video format support (MP4, AVI, MOV, MKV) and disk space.

### Out of Memory

Reduce batch size or increase `memory_threshold` configuration.

### WebSocket Connection Failure

Check firewall settings and proxy configuration.

## Performance Optimization Suggestions

- **GPU Acceleration**: Run on machines supporting CUDA for 10-50x inference speedup
- **Model Selection**: Choose appropriate model for your scenario, recommend yolov8n/yolov8s for real-time applications
- **Batch Processing**: Use batch processing optimization for batch detection to improve throughput
- **Video Frame Interval**: Increase `frame_interval` appropriately to reduce processing time
- **Memory Management**: System automatically monitors memory usage and adjusts batch size dynamically
