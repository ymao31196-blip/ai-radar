# vLLM

**类型**：推理部署框架
**官网**：https://vllm.ai
**GitHub**：https://github.com/vllm-project/vllm

---

## 更新记录

### v0.22.0 — 2026-05-29

**来源**：https://github.com/vllm-project/vllm/releases/tag/v0.22.0
**可信度**：🟢 官方

#### 变化了什么
- Breaking Change：Model Runner V2 默认用于 Qwen3 稠密模型（其他模型仍用 MRv1）
- 新功能：
  - **DeepSeek V4 全栈成熟支持**：NVFP4 MoE、CUDA graph、MTP spec decode
  - **实验性 Rust 前端**：性能敏感路径 Rust 化
  - **CUDA FP8 batch-invariant**：+28.9% 端到端吞吐提升
  - **多级 KV cache offloading**：降低显存占用
  - **JetBrains Mellum v2 支持**
  - **Blackwell SM12x flashinfer MoE**：新一代 GPU 加速
- 性能改进：
  - 459 commits, 230 贡献者 — 2026 年最大版本
  - FP8 计算路径大改，消除 batch-size 敏感

#### 有什么用
- **部署 DeepSeek V4**：v0.22 是 V4 生产部署的首选版本，解决了初始化、CUDA graph 等问题
- **FP8 推理提速**：batch-invariant CUDA FP8 提升 28.9%，对所有 FP8 量化模型受益
- **KV cache 优化**：多级 offloading 降低显存需求，相同硬件能跑更大 batch

#### 迁移成本
- Qwen3 稠密模型自动切换 MRv2，如有兼容性问题可通过环境变量回退 MRv1
- 其他模型无强制迁移

#### 行动项
- [ ] 如果部署 DeepSeek V4，升级到 v0.22+
- [ ] 评估 CUDA FP8 batch-invariant 对当前推理负载的吞吐提升
- [ ] 关注 v0.22.1 补丁（修复多节点 Ray hang、AMD Zen 优化）

---

### v0.22.1 — 2026-06-05

**来源**：https://github.com/vllm-project/vllm/releases/tag/v0.22.1
**可信度**：🟢 官方

#### 变化了什么
- 修复：多节点 Ray data-parallel hang
- 修复：DeepSeek-V4 初始化问题
- 新功能：AMD Zen CPU zentorch W8A8/W4A16 支持

#### 迁移成本
- 同 v0.22.0，无额外成本。建议从 v0.22.0 直接升级

#### 行动项
- [ ] 多节点部署用户升级到 v0.22.1（修复 Ray hang）
- [ ] AMD Zen 用户关注 zentorch 优化
