# 90-maintenance — 项目维护区

> 这里放"维护这个学习项目本身"的文档：规范演进、环境记录、决策日志、文档模板。
> 与学习内容无关；学习记录一律去 `01-learning/`。

## 目录说明

| 目录 | 放什么 | 命名规范 |
|------|--------|----------|
| `decisions/` | 决策日志：目录怎么定、规则为什么这么定、改动原因 | `D-序号-主题.md`，如 `D-001-目录结构V2.md` |
| `dev-notes/` | 维护笔记：CI 排障、git 操作记录、工具链问题 | `YYYY-MM-DD-主题.md` |
| `env/` | 环境快照：Python 版本、依赖 freeze、硬件说明 | `env-YYYY-MM-DD.txt` |
| `templates/` | 项目级文档模板 | 见下 |

## 模板清单

- `templates/TEMPLATE-week.md` — 周报模板（与 `01-learning/weekly/` 内一致）
- `templates/TEMPLATE-experiment.md` — 实验模板（与 `03-experiments/templates/` 内一致）
- `templates/TEMPLATE-review.md` — 阶段验收审查模板
- `templates/TEMPLATE-mistake.md` — 错题本条目模板

## 什么会进这里

- 调整了目录结构 / 学习规则 → 记一条 decision
- CI 挂了、推送被拒、权限问题 → 排障过程记入 dev-notes
- 换了机器 / 升级了依赖 → env 里存一份快照
- 模板要改版 → 在 templates 里改，并同步各使用处

## 什么不进这里

- 学习笔记、推导、错题 → `01-learning/`
- 代码实现 → `02-practice/`
- 实验数据 → `03-experiments/`
- 论文笔记 → `04-papers/`
