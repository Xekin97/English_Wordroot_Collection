# English Wordroot Collection

基于多个项目的公开资料整理的英语词根库，提供词根、原始英文 `meaning` 及对应单词，保留同族变体之间的关联。

当前共收录 **1,141 个词根条目**，所有 `example` 合并去重后共有 **9,671 个单词**，合计 **12,550 条词根与例词关系**。词根数量按平铺后的独立条目统计，同族变体与同形异义条目分别计数；单词在多个词根下出现时只计一次，保留的不同词形分别计数。

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

词根与例词主要整理自以下项目：

- [ECDICT](https://github.com/skywind3000/ECDICT)：基础词根与例词数据。
- [morphemes](https://github.com/colingoldberg/morphemes)：词根、词缀及构词关系。
- [generated-english-roots-list](https://github.com/WithEnglishWeCan/generated-english-roots-list)：词根与例词。
- [engra](https://github.com/eslsoft/engra)：词根及派生词关系。

整理和核对时还参考了以下构词与词源资料：

- [MorphoLex-en](https://github.com/hugomailhot/MorphoLex-en)：英语单词的构词标注。
- [MorphyNet](https://github.com/kbatsuren/MorphyNet)：单词派生和词形变化关系。
- [etymology-db](https://github.com/droher/etymology-db)：从 Wiktionary 词源数据整理的词源关系。
- [Kaikki.org 的 Simple English Wiktionary 数据](https://kaikki.org/simplewiktionary/English/index.html)：词条及其词源资料，用于辅助查找；与其他 Wiktionary 衍生数据存在来源重叠。
- 词典与词源参考：[Online Etymology Dictionary](https://www.etymonline.com/)、[Merriam-Webster](https://www.merriam-webster.com/)、[Dictionary.com](https://www.dictionary.com/)、[Collins Dictionary](https://www.collinsdictionary.com/)、[Wiktionary](https://en.wiktionary.org/)、[American Heritage Dictionary](https://www.ahdictionary.com/)、[Oxford Learner’s Dictionaries](https://www.oxfordlearnersdictionaries.com/) 等。

这些资料用于对照与核实，词形相似或出现在同一资料中并不自动证明词根关系。各来源的许可说明见 [notes/THIRD_PARTY_NOTICES.md](notes/THIRD_PARTY_NOTICES.md)。

数据文件：[JSON](roots.json) · [CSV](roots.csv)。JSON 是完整数据；CSV 提供常用字段，例词以 ` | ` 分隔。

## JSON 字段说明

`roots.json` 的顶层是数组，每个对象代表一个独立的词根写法。

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `id` | string | 当前词根条目的唯一标识，用于关联和区分同形异义条目。 |
| `root` | string | 展示用词根写法，去掉原资料中的末尾义项编号，例如 `ped1` 显示为 `ped`。展示写法不保证唯一。 |
| `source_form` | string | 采用的来源写法，包括 `ped1`、`ped2` 这类义项编号及原有连字符；补充写法的依据见整理记录。 |
| `meaning` | string | 基础来源中的英文词根含义，保留原文；新增词根采用对应参考条目的英文含义。 |
| `class` | string | 条目类别；当前 `roots.json` 收录的值均为 `root`。 |
| `origin` | string | 词源语言，例如 `Latin`、`Greek`。 |
| `example` | string[] | 当前词根写法对应的去重单词列表，可以为空。不同同族条目的列表允许重叠。 |
| `family_id` | string | 词根分组的标识；同一分组的写法及确认补充的同族写法共享此值。 |
| `related_root_ids` | string[] | 同一分组内其他词根条目的 `id`，不包含当前条目自身。 |
| `source_entry` | string | 作为基础的来源分组名称，例如 `ped1, pedi, -pede`；补充同族写法时沿用该名称，具体依据见整理记录。 |
| `pending_family_examples` | integer | 当前原始分组仍待处理的例词关系数量，属于分组级统计；`0` 不代表所有例词均经过逐词词源核实。 |

关联条目时使用 `id`，不要只用 `root`。`family_id` 和 `related_root_ids` 保留分组联系，不表示组内所有写法都可以互换。`example` 保留当前已收录的对应例词；部分历史拼写变化等非字面关系见 [补充记录](notes/related-only.json)。

另对 **67 个单词的词根对应关系**补充了校验核实，相关记录和整理说明见 [notes](notes/README.md)。

## TODO

- [ ] 继续对照四个来源，去重、整理尚未处理的词根与例词候选；候选中包括已有关系、词缀、不同义项和证据不足的条目，不能直接视为可收录数据。
- [ ] 复核待确认关系，区分同形异义、同族变体、历史词形变化和跨越构词边界的字母匹配。
- [ ] 检查现有条目中沿用自来源的例词及英文 `meaning`，修正发现的问题；当前数据尚未全部逐词核实。
- [ ] 为目前没有例词的词根继续查找可靠例词，并处理不适合保留的条目。
- [ ] 整理完成后以 JSON 为准统一生成 CSV，并核对两个文件的一致性。

当前为整理中的阶段性数据；例词可能包含罕见词、不同词形或多义词，使用时请结合词根义项判断。

原创整理成果采用 [CC BY-NC 4.0 非商业许可](LICENSE)，上游资料保留原许可，详见[来源与许可说明](notes/THIRD_PARTY_NOTICES.md)。
