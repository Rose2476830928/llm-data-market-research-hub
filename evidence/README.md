# evidence —— 实验证据库

存放**实验协议**与**原始实验数据**，目标是让论文里的每一个数字都能追到一份未改动的原始文件。

## 目录

```
protocols/   实验协议、测量规范、预注册（文本；改动即新版本）
materials/   冻结的实验材料（materials_v5_*）
fcs/         FCS 测量产物（prompts / raw / judgments / truth / audit）
runs/        运行清单 manifest（含 sha256）与审计摘要
```

## 准入规则

1. **不可变**：`materials/`、`fcs/truth/`、`runs/manifest*` 一旦入库不再修改；要改就新增版本目录
2. **单文件 ≤ 5 MB**：更大的原始轨迹（如 `calls.jsonl` 29.8 MB、`turns.jsonl` 28.2 MB）不进 git 历史，走 Release 附件
3. **不存密钥**：`.env`、Token、API Key 一律不入库
4. **每批带说明**：运行日期 + 参数快照（场景集 / K / 温度 / seed）+ commit sha

## 为什么单文件限 5 MB

git 删除文件不会释放历史体积。一次误推 30 MB 的 `.jsonl`，此后每次 clone 都要付这笔钱，且 `git rm` 收不回来。

## 当前已有的可入库材料（2026-11-08 实测体积）

| 来源 | 文件数 | 体积 | 建议 |
|---|---|---|---|
| `materials_v5_20261106/`（29 套） | 29 | 0.3 MB | 入库 |
| `fcs_v5_full_r5_20261106/` | 181 | 1.1 MB | 入库 |
| `study_a/plans/`（manifest 含 sha256） | 9 | 7.1 MB | 入库（单文件最大 1.8 MB） |
| `study_a/audit/` | 3 | 0.1 MB | 入库 |
| `study_a/offline/calls.jsonl` | 1 | **29.8 MB** | Release 附件 |
| `study_a/offline/turns.jsonl` | 1 | **28.2 MB** | Release 附件 |