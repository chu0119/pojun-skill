# Pojun Skill

> ⚠️ **仅用于授权测试**：本技能只应用于拥有书面授权的目标、SRC/众测平台范围内、CTF 竞赛或自有系统。对未授权目标的任何测试都是违法行为。技能本身内置了授权门控与安全护栏——请勿试图移除它们。

**给任意 AI Agent 装上"授权渗透测试专家的大脑"。**

本技能把 [Pojun](https://github.com/chu0119/Pojun)（AI 自主渗透测试平台，前 ARTEX——百度"agent+"攻防挑战赛冠军项目的完全演进版）的核心能力蒸馏成一个纯提示+文件驱动的 Agent Skill——零基础设施、零依赖，装上即用：

- **三视角协议**：planner（规划）/ worker（执行）/ auditor（对抗式自检）三视角轮换，单 agent 模拟多智能体分工
- **三账本纪律**：资产 / 事实 / 漏洞三本 markdown 账，每条事实带 `observed/inferred` 置信度与证据指针，每个确认漏洞必须"真实触发 + 可复现 + 独立复现"三重门槛
- **L1-L4 证据分级 + 机械验证闸门**（v2.0 新增）：线索→medium→high→critical 的量化口径；critical/high 必须附 HTTP 状态码/curl 输出/工具命中——纯版本匹配不算漏洞
- **四层安全护栏**：scope 授权门（新目标≠新授权）→ 操作约束 → 资产黑名单（.gov/.edu）→ 危险命令拦截（系统/数据库/HTTP 破坏全量规则）+ 不可逆操作人工确认协议
- **SRC 打法速查**（v2.0 新增）：一种子闭环节奏、高价值手法短表（对象存储 STS 通配/存储代理/扫码绑定链/公示接口导出…）、FOFA 速查语法、CORS 不挖纪律

## 安装

**Claude Code / ZCode（Agent Skills 格式）**

```bash
git clone https://github.com/chu0119/pojun-skill.git ~/.claude/skills/pojun-skill   # Claude Code
git clone https://github.com/chu0119/pojun-skill.git ~/.zcode/skills/pojun-skill    # ZCode（或你的 skills 目录）
```

**Cursor / 其他支持自定义规则的 Agent**

把 `SKILL.md` 与 `references/` 复制进项目，在规则文件（如 `.cursorrules`、`CLAUDE.md`）里加一行：

```
渗透测试任务必须遵循 ./SKILL.md 的全部协议后再行动。
```

**一次性使用**：直接把 `SKILL.md` 全文粘贴进系统提示 / 对话开头即可。

## 快速开始

对 agent 说：

```
用 pojun-skill 对 https://target.example.com 做授权渗透测试，
授权来源：XX SRC 平台（范围链接），约束：不做端口扫描、不爆破。
```

打 SRC/众测时补一句「按 src-playbook 的节奏和短表打」。

## 与 Pojun 平台版的关系

| | pojun-skill（本仓库） | Pojun 平台版 |
|---|---|---|
| 形态 | 单 SKILL.md + references，纯提示驱动 | Go 单体 + 多 Agent 编排 + PostgreSQL |
| 方法论 | 三视角/三账本/证据分级/SRC 速查 | 同源 + 21 个场景 skill + 48 篇 SRC 知识库 |
| 证据留痕 | 本地 markdown 账本 + evidence/ 目录 | MITM 流量留证、证据版本化、Word 公文导出 |
| 适用 | 任意 AI Agent、零依赖 | 需 Linux 服务器 + PostgreSQL |

方法论同源：平台版 `skills/src-hunting`、`pentest-verification`、`evidence-rules` 与本仓库互相印证，改一处会同步另一处。

## 历史

本仓库前名 `artex-skill`（ARTEX 时代 v0.1.0），2026-11-06 随项目更名 Pojun 一并更名并升级 v2.0。旧链接由 GitHub 自动跳转。

## 许可

AGPL-3.0。仅用于授权测试。
