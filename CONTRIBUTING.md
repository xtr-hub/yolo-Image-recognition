# 贡献指南

[![中文](https://img.shields.io/badge/中文-贡献指南-red?style=flat-square)](CONTRIBUTING.md)
[![English](https://img.shields.io/badge/English-Contributing%20Guide-red?style=flat-square)](CONTRIBUTING.en.md)

感谢你对本项目的关注！欢迎通过 Issue、Pull Request 或文档改进参与贡献。

## 开始之前

- 先阅读 [README.md](README.md) 和相关文档，了解项目功能与运行方式。
- 提交问题前，请先搜索现有 Issue，避免重复反馈。
- 如果是较大的功能改动，建议先创建 Issue 讨论方案，再开始实现。

## 本地开发

```bash
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

访问 `http://localhost:8000` 验证 Web 界面和接口功能。

## 提交代码

1. 从最新的 `main` 分支创建功能分支。
2. 保持改动聚焦，避免在一个 PR 中混合多个无关修改。
3. 确保代码风格与现有项目一致。
4. 对接口、模型推理、WebSocket 或视频处理相关改动，请尽量补充测试或验证说明。
5. 提交 PR 时说明：
   - 改动内容
   - 解决的问题
   - 验证方式
   - 可能的兼容性影响

## 代码与文档规范

- Python 代码应保持清晰命名和合理的异常处理。
- API 行为变更需要同步更新文档。
- 新增配置项时，请在 README 或相关文档中说明默认值和使用方式。
- 前端静态资源改动应兼顾桌面端和移动端体验。

## 问题反馈

提交 Issue 时请尽量包含：

- 操作系统和 Python 版本
- 依赖安装方式
- 使用的 YOLO 模型名称
- 复现步骤
- 期望结果与实际结果
- 相关日志、截图或示例文件信息

## 安全问题

如果你发现安全漏洞，请不要在公开 Issue 中披露敏感细节。可以先提交简要说明，或通过维护者指定的私有渠道沟通。
