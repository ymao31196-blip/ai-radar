# Ollama

**类型**：本地模型推理工具
**官网**：https://ollama.com
**GitHub**：https://github.com/ollama/ollama

---

## 更新记录

### v0.30.0~0.30.6 — 2026-05-13 ~ 06-05

**来源**：https://github.com/ollama/ollama/releases
**可信度**：🟢 官方

#### 变化了什么
- 新功能：
  - **llama.cpp 引擎增强**：扩展 GGUF 模型兼容性，NVIDIA 性能改进
  - **MLX 引擎**：Apple Silicon 上的补充推理后端
  - **gemma4:12b 支持**（v0.30.3）
  - **Cline CLI 集成**（v0.30.2）
  - **Qwen code 集成**（v0.30.2）
  - **Radeon 8060S iGPU 默认发现**（v0.30.2）
  - **`ollama launch` 集成扩展**：Codex App（v0.24.0）、Oh My Pi AI coding agent（v0.30.6）
  - MLX 嵌入层 NVFP4 global scale 量化改进（v0.30.6）
- 修复：gemma4:12b 浮点异常崩溃（v0.30.5）、Windows 清理、Codex launch 配置隔离

#### 有什么用
- **Gemma 4 12B 本地运行**：Ollama 是目前最简单的 Gemma 4 本地部署方式
- **Apple Silicon 加速**：MLX 引擎对 M 系列芯片推理有专门优化
- **IDE 集成**：Cline CLI + Qwen code + Codex App 的 launch 集成，让终端 Agent 工具一键连接本地模型
- **AMD GPU 支持改进**：Radeon iGPU 自动发现，降低 AMD 用户配置门槛

#### 迁移成本
- gemma4:12b 在 v0.30.4/5 有已知崩溃，建议用 v0.30.6+
- llama.cpp 引擎升级向下兼容

#### 行动项
- [ ] 如果需要在本地跑 Gemma 4 12B，升级到 v0.30.6+
- [ ] 试用 `ollama launch` 集成：能否用本地模型驱动 Cline/Cursor？
- [ ] Apple Silicon 用户关注 MLX 引擎的性能提升
