# Context Handoff 中文说明

这个文件是 `context-handoff` 技能的中文补充说明。

保留 [../SKILL.md](../SKILL.md) 作为技能必需入口文件；当需要中文规则、中文措辞或中文示例时，优先参考本文件。以后如果需要增加其他语言，沿用同样命名方式，例如：

- `SKILL-cn.md`
- `SKILL-ja.md`
- `SKILL-fr.md`

## 目的

生成一份可在新线程、新窗口或后续会话中继续使用的高密度交接文档，避免重复搜索、重复判断和上下文丢失。

## 调用方式

可以直接这样调用：

```text
用 $context-handoff 生成交接文档
```

也可以更明确一点：

```text
用 $context-handoff 把当前任务整理成可在新线程继续的 handoff，写到工作区文件里
```

如果你想指定输出目标，也可以这样说：

```text
用 $context-handoff 生成交接文档，写到当前工作区根目录
```

```text
用 $context-handoff 生成交接文档，文件名用 handoff-api.md
```

## 默认行为

- 默认输出语言：中文
- 代码标识符、命令、API、路径名保持原文
- 默认输出到当前工作区根目录
- 默认文件名为 `handoff.md`
- 如果 `handoff.md` 已存在且用户没有明确要求覆盖，则改为 `handoff-YYYYMMDD-HHMM.md`

## 交接文档固定结构

按以下顺序输出：

```md
# Task

## Current Goal

## Confirmed Facts

## Key References

## Assumptions / Inferences

## Tried Already

## Open Questions

## Next Best Step

## Suggested New-Thread Prompt
```

## 写作规则

- 只把已经验证过的内容写进 `Confirmed Facts`
- 推断、猜测、未证实内容写进 `Assumptions / Inferences`
- 不要粘贴整段聊天记录
- 不要用空泛总结，优先保留能帮助续做的细节
- 保留已经执行过的命令、已验证结论、走不通的方向
- 至少提供一个可直接复制到新线程的提示词

## 不同任务类型的处理

### 代码类任务

在 `Key References` 中优先包含：

- 关键文件链接
- 精确行号
- 相关符号名
- 已运行命令
- 测试或构建状态

### 调研/分析类任务

在 `Key References` 中优先包含：

- 证据来源
- 已确认发现
- 尚未证实的假设
- 建议继续的分析方向

### 混合任务

同时保留代码线索和分析线索，不要偏废任何一边。

## 中文措辞建议

优先使用以下风格：

- `已确认`
- `推断`
- `尚未证实`
- `已尝试`
- `下一步最佳动作`

避免使用：

- `大概就是`
- `差不多`
- `可能应该没问题`

## 新线程提示词模板

```md
继续处理当前任务。先阅读 [handoff.md](/abs/path/handoff.md) 和其中引用的关键文件，然后从 “Next Best Step” 开始继续，不要重复已经验证过的搜索、命令和结论。
```

## 文件写入失败时

如果当前环境不能写文件：

- 仍然在聊天中给出完整 handoff 内容
- 明确说明未能落盘
- 仍然提供可直接粘贴的新线程提示词
