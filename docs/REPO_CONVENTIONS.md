# 仓库约定 / Repository conventions

## 1. 这个仓库放什么

研究过程资产：设计文档、变量口径、裁决记录、文献笔记、论文草稿、审查报告。

**不放**：实验代码（去 `cdmn-fcs`）、原始数据与付费模型读数、任何密钥或 `.env`。

## 2. 目录

```
design/     实验设计、变量口径、裁决记录（权威文档）
notes/      工作笔记、日志、审查记录（可随时追加）
literature/ 文献笔记与引用核查
papers/     论文大纲、草稿、图表
archive/    冻结的历史版本，只读
docs/       仓库自身的规范与索引
```

## 3. 分支

| 分支 | 用途 | 生命周期 |
|---|---|---|
| `main` | 稳定快照，只接受 PR 合入 | 长期 |
| `docs/<slug>` | 文档与规范改动 | 合入即删 |
| `chore/<slug>` | 仓库维护（模板、ignore、索引） | 合入即删 |

不设 `develop`：单人研究项目，多一层分支只增加合并负担。

## 4. 提交信息

`<type>: <中文一句话>`

- `type` ∈ `docs` / `chore` / `fix` / `data` / `meta`
- 正文如涉及读数，必须写明**日期 + 文件路径 + 具体数值**

例：`docs: 记录 2026-11-08 的 41/46 提交含明文密钥读数`

## 5. Issue 与 PR

- 一个问题一个 Issue，标签用 `P0-blocker` / `P1-next` / `P2-later` + `area:*` + `type:decision`
- 需要研究者裁决的，标 `type:decision`，在 Issue 里列选项与影响，不代选
- PR 必须关联 Issue（`Refs #N`），合入前至少自查一遍清单

## 6. 硬性红线

1. 冻结材料（`materials_v5_20261106`、`truth_v5_full.json`、`formal_manifest_*`）不得修改
2. 不写入任何 Token / API Key / `.env` 内容
3. 不把历史含密钥的提交整段推到本仓库
4. 结论必须可回溯：文件路径 + 读数 + 日期，缺一不写