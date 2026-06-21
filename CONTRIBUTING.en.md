# Contributing Guide

[![中文](https://img.shields.io/badge/中文-贡献指南-red?style=flat-square)](CONTRIBUTING.md)
[![English](https://img.shields.io/badge/English-Contributing%20Guide-red?style=flat-square)](CONTRIBUTING.en.md)

Thank you for your interest in this project! Contributions via Issues, Pull Requests, or documentation improvements are welcome.

## Before You Start

- Read [README.md](README.en.md) and related documentation to understand the project features and how it works.
- Search existing Issues before submitting a new one to avoid duplicate feedback.
- For larger feature changes, it's recommended to create an Issue to discuss the approach before starting implementation.

## Local Development

```bash
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Visit `http://localhost:8000` to verify the web interface and API functionality.

## Submitting Code

1. Create a feature branch from the latest `main` branch.
2. Keep changes focused, avoid mixing multiple unrelated modifications in one PR.
3. Ensure code style is consistent with the existing project.
4. For changes related to API, model inference, WebSocket, or video processing, please add tests or verification instructions if possible.
5. When submitting a PR, explain:
   - What was changed
   - The problem it solves
   - How it was verified
   - Possible compatibility impacts

## Code and Documentation Standards

- Python code should maintain clear naming and proper exception handling.
- API behavior changes require updating documentation synchronously.
- When adding new configuration items, explain default values and usage in README or related documentation.
- Frontend static resource changes should consider both desktop and mobile experiences.

## Issue Feedback

When submitting an Issue, please include:

- Operating system and Python version
- Dependency installation method
- YOLO model name used
- Steps to reproduce
- Expected and actual results
- Relevant logs, screenshots, or sample file information

## Security Issues

If you discover a security vulnerability, please do not disclose sensitive details in public Issues. You can submit a brief description first, or communicate through private channels specified by maintainers.
