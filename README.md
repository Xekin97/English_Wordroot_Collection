# English Wordroot Collection

基于多个项目的公开资料整理的英语词根库，提供词根、原始英文 `meaning` 及对应单词，保留同族变体之间的关联。

## 整理目的：词根平铺化

将原资料中「多个词根写法共用一组例词」的结构，整理为「每个词根写法独立对应自己的例词列表」，便于按单个词根检索、选词，以及用于词根学习和数据使用。

```text
整理前：a, b, c → 混合例词列表

整理后：a → a 对应的例词列表
        b → b 对应的例词列表
        c → c 对应的例词列表
```

平铺后仍保留原分组和同族关联。同族变体可以共享例词；同形异义词根分别保留。例如，表示脚的 `ped1` 与表示儿童的 `ped2` 展示时都可以写作 `ped`，但它们是不同条目。

## 资料来源

- [ECDICT](https://github.com/skywind3000/ECDICT)：基础词根与例词数据。
- [morphemes](https://github.com/colingoldberg/morphemes)：词根、词缀及构词关系参考。
- [generated-english-roots-list](https://github.com/WithEnglishWeCan/generated-english-roots-list)：词根与例词对照参考。
- [engra](https://github.com/eslsoft/engra)：词根及派生词关系参考。

数据文件：[JSON](roots.json) · [CSV](roots.csv)。

## JSON 字段说明

`roots.json` 的顶层是数组，每个对象代表一个独立的词根写法。

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `id` | string | 当前词根条目的唯一标识，用于关联和区分同形异义条目。 |
| `root` | string | 展示用词根写法，去掉原资料中的末尾义项编号，例如 `ped1` 显示为 `ped`。展示写法不保证唯一。 |
| `source_form` | string | 拆分后保留的原始写法，包括 `ped1`、`ped2` 这类义项编号及原有连字符。 |
| `meaning` | string | 原资料中的英文词根含义，保留原文。 |
| `class` | string | 原资料中的条目类别；当前 `roots.json` 收录的值均为 `root`。 |
| `origin` | string | 原资料标注的词源语言，例如 `Latin`、`Greek`。 |
| `example` | string[] | 当前词根写法对应的去重单词列表，可以为空。不同同族条目的列表允许重叠。 |
| `family_id` | string | 原始分组的标识；从同一分组拆出的词根共享此值。 |
| `related_root_ids` | string[] | 同一原始分组内其他词根条目的 `id`，不包含当前条目自身。 |
| `source_entry` | string | 原始分组名称，例如 `ped1, pedi, -pede`，用于追溯整理来源。 |
| `pending_family_examples` | integer | 当前原始分组仍待处理的例词关系数量，属于分组级统计；`0` 不代表所有例词均经过逐词词源核实。 |

关联条目时使用 `id`，不要只用 `root`。`family_id` 和 `related_root_ids` 保留分组联系，不表示组内所有写法都可以互换。`example` 保留符合字面对应规则的例词，已确认的历史拼写变化等非字面关系见 [补充记录](notes/related-only.json)。

另对 **67 个单词的词根对应关系**补充了校验核实，相关记录和整理说明见 [notes](notes/README.md)。

原创整理成果采用 [CC BY-NC 4.0 非商业许可](LICENSE)，上游资料保留原许可，详见[来源与许可说明](notes/THIRD_PARTY_NOTICES.md)。
