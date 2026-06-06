# Qdrant

**类型**：向量数据库
**官网**：https://qdrant.tech
**GitHub**：https://github.com/qdrant/qdrant

---

## 更新记录

### v1.18.0~1.18.2 — 2026-05-11 ~ 06-04

**来源**：https://github.com/qdrant/qdrant/releases
**可信度**：🟢 官方

#### 变化了什么
- **⚠️ Breaking Change：完全移除 RocksDB 支持**
  - 必须已迁移到 Gridstore 存储格式才能升级
- 新功能：
  - **TurboQuant 量化变体**：8x 压缩，无 recall 惩罚
  - 命名向量增删 API
  - 深度内存报告
  - 低内存模式 + `max_resident_memory_percent` 严格模式参数
- 安全修复（v1.18.2）：
  - REST auth whitelist bypass（CVE）
  - 恶意快照越界堆读取

#### 有什么用
- **TurboQuant**：内存占用降至 1/8，相同硬件可存 8 倍向量，对大规模语义搜索意义重大
- **低内存模式**：对边缘设备或小内存实例友好
- **安全修复必须升级**：v1.18.2 修复了认证绕过 CVE，生产环境应尽快更新

#### 迁移成本
- **升级前必须确认存储已迁移到 Gridstore**。如果还在 RocksDB，需先完成数据迁移
- 命名向量 API 是增强，旧 API 兼容

#### 行动项
- [ ] 生产环境 Qdrant 集群尽快升级至 v1.18.2（安全修复）
- [ ] 升级前验证 Gridstore 迁移完成
- [ ] 评估 TurboQuant 对内存占用的实际降低效果
