---
name: everything-claude-code
description: AI agent harness性能优化系统深度学习
type: reference
originDate: 2026-05-11
lastUpdate: 2026-05-11
---

# Everything Claude Code 深度学习

## 项目信息
- **Stars**: 178,174
- **Forks**: 27,513
- **语言**: JavaScript/TypeScript
- **认证**: Anthropic Hackathon Winner
- **仓库**: affaan-m/everything-claude-code

---

## 核心架构

### 跨Harness设计
```
skills/*/SKILL.md  ← 最可移植的单元
rules/             ← 共享规则
hooks/            ← 事件钩子
MCP configs       ← 工具配置
```

### 支持的Harnesses
- Claude Code (原生hooks)
- Codex (AGENTS.md)
- OpenCode (plugin/events)
- Cursor (rules/hooks适配)
- Gemini (指令兼容)

---

## 核心组件统计

| 组件 | 数量 |
|------|------|
| Agents | 48 |
| Skills | 182 |
| Commands | 68 |
| Rules语言 | 12 |

---

## 目录结构

```
everything-claude-code/
├── .agents/           # agent配置
├── agents/            # 48 agents
├── commands/          # 68 commands
├── hooks/             # hooks.json + scripts/hooks/
├── rules/             # common + 12语言
├── skills/            # 182 skills
├── scripts/           # 核心脚本
├── docs/              # 架构文档
├── ecc2/              # Rust控制平面(alpha)
├── manifests/         # 安装清单
└── .claude-plugin/    # Claude插件
```

---

## 关键Skills

### 1. continuous-learning-v2 (Instinct架构)
- **观察**: PreToolUse/PostToolUse hooks (100%可靠)
- **单元**: Atomic "instincts" with confidence scoring
- **进化**: instincts → cluster → skill/command/agent

### 2. nanoclaw-repl
- 基于`claude -p`的session-aware REPL
- 零外部依赖
- markdown持久化

### 3. eval-harness
- 验证循环系统
- checkpoint vs continuous evals
- pass@k metrics

### 4. autonomous-loops
- 自动循环执行
- 5层guard防止observer爆炸

---

## Hooks系统 (scripts/hooks/)

### PreToolUse Hooks
- `pre-bash-dispatcher.js` - 质量/tmux/push/GateGuard
- `pre-bash-dev-server-block.js` - 开发服务器阻止
- `pre-bash-git-push-reminder.js` - git push提醒
- `pre-bash-commit-quality.js` - 提交质量检查
- `design-quality-check.js` - 设计质量检查

### PostToolUse Hooks
- `post-bash-dispatcher.js` - 后处理分发
- `post-edit-format.js` - 格式化
- `post-edit-typecheck.js` - 类型检查
- `session-activity-tracker.js` - 会话追踪
- `stop-format-typecheck.js` - 停止时格式化

### Stop Hooks
- `session-end.js` - 会话结束处理
- `evaluate-session.js` - 会话评估

---

## 规则系统 (rules/)

### 语言覆盖
- common/ - 通用规则
- typescript/, python/, golang/, rust/
- java/, cpp/, csharp/, dart/, kotlin/
- swift/, php/, perl/, web/, zh/

### 规则目录结构
```
rules/
├── README.md
├── common/        # 通用
├── typescript/   # TS规则
├── python/       # Python规则
└── ... (其他语言)
```

---

## 安装方式

### 1. 插件安装 (推荐)
```bash
/plugin marketplace add https://github.com/affaan-m/everything-claude-code
/plugin install everything-claude-code@everything-claude-code
```

### 2. 手动安装
```bash
./install.sh --profile full
```

### 3. 最小化安装
```bash
./install.sh --profile minimal --target claude
```

---

## 核心脚本 (scripts/)

| 脚本 | 用途 |
|------|------|
| ecc.js | 主入口/lifecycle管理 |
| claw.js | NanoClaw REPL |
| doctor.js | 诊断修复 |
| install-apply.js | 安装应用 |
| catalog.js | 组件目录 |

---

## 创新点

### 1. Instinct-Based Learning
- 替代skills作为学习单元
- 0.3-0.9 confidence scoring
- project-scoped + global隔离

### 2. Project Detection
- git remote URL hash → project ID
- 跨机器项目同步
- scope污染防止

### 3. Observer Loop Prevention
- 5层guard防止无限循环
- throttling + tail sampling
- lazy-start + re-entrancy guard

### 4. ECC 2.0 Rust Control Plane
- ecc2/ 构建本地可用
- dashboard/start/sessions/status/stop/resume/daemon

---

## References

- [GitHub](https://github.com/affaan-m/everything-claude-code)
- [中文README](README.zh-CN.md)
- [跨Harness架构](docs/architecture/cross-harness.md)
- [HERMES设置](docs/HERMES-SETUP.md)

---

## 下一步学习

1. 深入研究某个具体skill (eval-harness/autonomous-loops)
2. 分析hooks实现细节
3. 研究rules目录结构
4. 理解ecc2 Rust控制平面