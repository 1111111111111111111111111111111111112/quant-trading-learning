---
name: everything-claude-code-deep-learning
description: Everything Claude Code深度学习进度
type: project
originDate: 2026-05-11
lastUpdate: 2026-05-11
---

# Everything Claude Code 深度学习进度

## 学习时间
2026-05-11

## 已完成深度研究

### 1. continuous-learning-v2 (完整内容)
- **观察**: PreToolUse/PostToolUse hooks (100%可靠)
- **单元**: Atomic instincts with 0.3-0.9 confidence scoring
- **v2.1新增**: Project-scoped instincts (git remote hash隔离)
- **进化路径**: instincts → cluster → skill/command/agent
- **项目检测**: CLAUDE_PROJECT_DIR > git remote > git rev-parse > global fallback
- **命令**: /instinct-status, /evolve, /instinct-export, /instinct-import, /promote, /projects

### 2. eval-harness (完整内容)
- **Capability Evals**: 测试新能力
- **Regression Evals**: 确保不破坏现有功能
- **Grader类型**: Code-Based/Model-Based/Human
- **核心指标**: pass@k (at least one success in k attempts)
- **pass^k**: All k trials succeed (更高标准)

### 3. autonomous-loops (完整内容)
- **6种模式**: Sequential/NanoClaw/Infinite/PR Loop/De-Sloppify/RFC-DAG
- **Sequential Pipeline**: claude -p链式调用
- **De-Sloppify**: 分离cleanup pass处理过度测试
- **Continuous PR Loop**: 自动修复CI失败，SHARED_TASK_NOTES.md跨迭代
- **Infinite Loop**: 波浪式并行agent部署
- **RFC-DAG**: 多agent协调工作流

### 4. ECC 2.0 Reference Architecture (完整内容)
- **三层架构**: TUI Layer (ratatui) → Runtime Layer (library) → Daemon Layer
- **竞品对比**: vs Superset, dmux, opencode, claude-squad
- **优势**: Terminal-native, 116-skill生态系统, AgentShield, Rust单二进制(3.4MB)

### 5. ECC2 Codebase Analysis (完整内容，171行)
- **4,417行Rust代码**，15个.rs文件
- **模块分布**: session/(1974行), tui/(1613行), observability/(409行), config/(144行)
- **代码质量**: 29个测试函数，3个unwrap()，0个unsafe
- **风险评分**: 4轴分析(base tool risk, file sensitivity, blast radius, irreversibility)
- **主要Gap**:
  - comms模块半完成(无receive/poll)
  - 新会话对话框未实现
  - 单agent支持
  - 无聚合metrics
  - daemon无健康报告
- **依赖过时**: rusqlite 0.32 vs 最新0.39, tokio 1 vs 1.50

---

## 架构设计模式

### 1. Workspace Runtime Registry (from Superset)
- trait-based abstraction with capability flags
- Persistent daemon terminal via IPC
- Per-project mutex for git operations

### 2. Worker-per-pane (from dmux)
- Status detection via terminal output fingerprinting
- Agent Registry (install check, launch cmd, permissions)
- PaneLifecycleManager + exclusive locks
- Lifecycle hooks: worktree_created, pre_merge, post_merge

### 3. DbWriter Thread (ECC2原创)
- SQLite writes from async context via mpsc::unbounded_channel
- 解决"SQLite from async"问题

### 4. Ring Buffer (ECC2原创)
- Session output buffer: OUTPUT_BUFFER_LIMIT = 1000 lines
- 自动驱逐旧条目

---

## 项目隔离机制

### Instinct Scope
```
Project Detection优先级:
1. CLAUDE_PROJECT_DIR (最高)
2. git remote get-url origin (hash → portable ID)
3. git rev-parse --show-toplevel (机器特定)
4. Global fallback (无项目时)
```

### 12字符Hash ID
- A1b2c3d4e5f6格式
- 同一repo不同机器得到相同ID
- projects.json映射ID到人类可读名称

---

## 安全设计

### Risk Scoring (4轴)
1. **Base Tool Risk**: 工具固有风险
2. **File Sensitivity**: 文件敏感度
3. **Blast Radius**: 影响范围
4. **Irreversibility**: 不可逆性

Composite score: 0.0-1.0
Actions: Allow/Review/RequireConfirmation/Block

### 安全发现
- 无硬编码secret
- tokio::process::Command使用Stdio::piped()
- Task string无shell注入风险
- 但session task string需安全审计

---

## P0-P3优先级建议

### P0 Quick Wins
1. Config增加环境变量支持: ECC_DB_PATH, ECC_WORKTREE_ROOT, ECC_DEFAULT_AGENT

### P1 Feature Completions
2. 实现comms::receive/poll
3. TUI内建新会话对话框
4. 添加聚合metrics视图

### P2 Robustness
5. 扩展manager/runtime/daemon测试
6. comms/worktree模块添加测试
7. Daemon健康报告(PID file, graceful shutdown)
8. Task string安全审计
9. 拆分dashboard.rs(1273行 → 多文件)

### P3 Extensibility
10. Multi-agent支持
11. Config验证

---

## 与量化交易学习的关联

### 可以借鉴的思想
1. **Instinct-based learning** → 量化策略的模式识别
2. **Eval-driven development** → 量化策略的回测驱动
3. **Project-scoped isolation** → 多市场/多策略隔离
4. **Continuous PR Loop** → 量化策略的持续迭代优化

---

## 下一步
1. 研究更多skills: tdd-workflow, security-review, code-architect等
2. 深入hooks实现细节
3. 理解rules系统完整结构
4. 实践instinct-based learning系统