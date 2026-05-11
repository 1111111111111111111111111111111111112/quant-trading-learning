---
name: everything-claude_code_skills
description: ECC核心Skills深入学习
type: reference
originDate: 2026-05-11
---

# ECC Skills 深入学习

## security-review (495行)
综合安全审查技能，覆盖：
- Secrets管理 (env变量，无硬编码)
- Input验证 (Zod schemas)
- SQL注入防护 (参数化查询)
- Auth (httpOnly cookies，非localStorage)
- XSS防护 (DOMPurify, CSP)
- CSRF保护 (tokens, SameSite)
- Rate Limiting (API限流)

## tdd-workflow (TDD开发流程)
测试驱动开发，80%+覆盖率：
- RED阶段：先写测试，验证失败
- GREEN阶段：写最小代码让测试通过
- REFACTOR阶段：重构优化
- Checkpoint commits记录每个阶段

## deep-research (深度研究)
多源研究，使用firecrawl/exa MCP：
- 分解子问题(3-5个)
- 并行搜索(15-30个源)
- 深度阅读关键URL
- 综合报告+引用

## architecture-decision-records (ADR)
架构决策记录：
- 格式：Nygard ADR格式
- 触发：明确决策时刻
- 生命周期：proposed → accepted → deprecated/superseded
- 项目隔离+全局提升

## continuous-learning-v2 (完整Instinct架构)
- Hooks观察(100%可靠)
- Atomic instincts (0.3-0.9 confidence)
- 项目隔离(git remote hash)
- 自动进化：instincts → skills/commands
- 自动提升：project → global

## 核心Skills列表
| Skill | 用途 |
|-------|------|
| security-review | 安全审查 |
| tdd-workflow | TDD开发 |
| deep-research | 深度研究 |
| architecture-decision-records | ADR记录 |
| continuous-learning-v2 | 跨对话学习 |
| eval-harness | 评估框架 |
| autonomous-loops | 自动循环 |
| code-architect | 代码架构 |
| git-workflow | Git工作流 |
| cost-aware-llm-pipeline | 成本优化 |

## 全部Skills (182个)
覆盖：accessibility, ai-first-engineering, android, api-design, backend-patterns, benchmark, blueprint, browser-qa, bun-runtime, claude-devfleet, clickhouse-io, code-tour, codebase-onboarding, coding-standards, configure-ecc, content-engine, continuous-agent-loop, continuous-learning, cpp-coding-standards, cpp-testing, crosspost, csharp-testing, customer-billing-ops, dashboard-builder, data-scraper-agent, database-migrations, deployment-patterns, design-system, django-patterns, django-security, django-tdd, dmux-workflows, docker-patterns, documentation-lookup, eval-harness, evm-token-decimals, exa-search, fal-ai-media, finance-billing-ops, flutter-dart-code-review, foundation-models-on-device, frontend-patterns, frontend-slides, gan-style-harness, gateguard, git-workflow, github-ops, golang-patterns, golang-testing, google-workspace-ops, healthcare-cdss-patterns, healthcare-emr-patterns, healthcare-eval-harness, healthcare-phi-compliance, hexagonal-architecture, hipaa-compliance, hookify-rules, inventory-demand-planning, investor-materials, investor-outreach, iterative-retrieval, java-coding-standards, jira-integration, jpa-patterns, kotlin-coroutines-flows, kotlin-exposed-patterns, kotlin-ktor-patterns, kotlin-patterns, kotlin-testing, laravel-patterns, laravel-plugin-discovery, laravel-security, laravel-tdd, laravel-verification, lead-intelligence, liquid-glass-design, llm-trading-agent-security, logistics-exception-management, manim-video, market-research, mcp-server-patterns, messages-ops, nanoclaw-repl, nestjs-patterns, nextjs-turbopack, nodejs-keccak256, nutrient-document-processing, nuxt4-patterns, openclaw-persona-forge, opensource-pipeline, perl-patterns, perl-security, perl-testing, plankton-code-quality, postgres-patterns, product-capability, product-lens, production-scheduling, project-flow-ops, prompt-optimizer, python-patterns, python-testing, pytorch-patterns, quality-nonconformance, ralphinho-rfc-pipeline, regex-vs-llm-structured-text, removal-video-creation, repo-scan, research-ops, returns-reverse-logistics, rust-patterns, rust-testing, safety-guard, santa-method, search-first, security-bounty-hunter, security-scan, seo, skill-comply, skill-stocktake, social-graph-ranker, springboot-patterns, springboot-security, springboot-tdd, springboot-verification, strategic-compact, swift-actor-persistence, swift-concurrency-6-2, swift-protocol-di-testing, swiftui-patterns, team-builder, terminal-ops, token-budget-advisor, ui-demo, unified-notifications-ops, verification-loop, video-editing, videodb, visa-doc-translate, workspace-surface-audit
