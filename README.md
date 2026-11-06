# English Wordroot Collection

基于多个项目的公开资料整理的英语词根库，收录词根、前缀、后缀和部分构词形式，提供英文 `meaning` 及对应单词，保留同族变体之间的关联。

当前 JSON 共收录 **4,314 个词根及词缀条目**，所有 `example` 合并去重后共有 **26,980 个单词**，合计 **36,710 条词根与例词关系**。条目数量按平铺后的独立记录统计，同族变体与同形异义条目分别计数；单词在多个词根下出现时只计一次，保留的不同词形分别计数。

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
- 词典与词源参考：[Online Etymology Dictionary](https://www.etymonline.com/)、[Merriam-Webster](https://www.merriam-webster.com/)、[Dictionary.com](https://www.dictionary.com/)、[Collins Dictionary](https://www.collinsdictionary.com/)、[Wiktionary](https://en.wiktionary.org/)、[American Heritage Dictionary](https://www.ahdictionary.com/)、[Oxford Learner’s Dictionaries](https://www.oxfordlearnersdictionaries.com/) 等；医学词缀另参考 [MedlinePlus 词素表](https://medlineplus.gov/appendixa.html)，部分历史词形参考大学教材及历史词典。
- 部分英文词根含义和变体还参考词根词典、教材和学术资料，具体来源见[来源与许可说明](notes/THIRD_PARTY_NOTICES.md)。

这些资料用于对照与核实，词形相似或出现在同一资料中并不自动证明词根关系。各来源的许可说明见 [notes/THIRD_PARTY_NOTICES.md](notes/THIRD_PARTY_NOTICES.md)。

数据文件：[JSON](roots.json) · [CSV](roots.csv)。CSV 已从当前 JSON 生成并核对，提供 `id`、`root`、`source_form`、`meaning`、`class`、`origin`、`source_entry` 和 `example` 八个常用字段；例词以 ` | ` 分隔。同族关联和待处理计数请使用 JSON。

## JSON 字段说明

`roots.json` 的顶层是数组，每个对象代表一个独立的词根写法。

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `id` | string | 当前词根条目的唯一标识，用于关联和区分同形异义条目。 |
| `root` | string | 展示用词根写法，去掉原资料中的末尾义项编号，例如 `ped1` 显示为 `ped`。展示写法不保证唯一。 |
| `source_form` | string | 采用的来源写法，包括 `ped1`、`ped2` 这类义项编号及原有连字符。 |
| `meaning` | string | 英文词根含义；优先保留原资料的释义。原资料缺少含义或将不同形式的含义混在一起时，采用参考资料中适用于该条目的英文含义。 |
| `class` | string | 统一后的类别：`root`、`prefix`、`suffix`、`combining_form`（构词形式）、`historical_stem`（历史词干）或 `lookup_alias`（查找别名）。别名不一定是独立的古典语词素；来源类别与细分标记见[类别记录](notes/class-provenance.json)。 |
| `origin` | string | 词源语言，例如 `Latin`、`Greek`。 |
| `example` | string[] | 当前词根写法对应的去重单词列表，可以为空。不同同族条目的列表允许重叠。 |
| `family_id` | string | 词根分组的标识；同一分组的写法及确认补充的同族写法共享此值。 |
| `related_root_ids` | string[] | 同一分组内其他词根条目的 `id`，不包含当前条目自身。 |
| `source_entry` | string | 作为基础的来源分组名称，例如 `ped1, pedi, -pede`；补充同族写法时可能沿用该名称。 |
| `pending_family_examples` | integer | 整理过程中记录的分组级待处理数量；该历史计数尚未全面重新核算，不能作为当前待处理总数，`0` 也不代表所有例词均已核实。 |

关联条目时使用 `id`，不要只用 `root`。`family_id` 和 `related_root_ids` 保留分组联系，不表示组内所有写法都可以互换。`example` 包含历史变体关系，不一定是现代单词中可以直接切分的字母片段；部分非字面联系及来源范围见[补充记录](notes/related-only.json)与[例词审核状态](notes/edge-audit.json)。

## 审核状态与已知限制

- [词根与例词审核状态](notes/edge-audit.json)与 `roots.json` 的 SHA-256 绑定，以词根 `id` 和例词为键。`supported_scoped` 表示指定词义或来源范围有依据；`historical_accept_scoped` 表示找到该范围的历史接受记录，不能视为对所有义项的保证；未列出或标记 `untraced` 表示尚未找到对应的逐条审核记录，并不等于错误。`related_pending_candidate` 表示有待核的相关来源候选，不自动代表当前关系有误。若同一条记录含 `later_resolution`，以后者说明为准。
- [待确认关系](notes/held-relations.json)记录了 **163 条目前从主表暂缓的例词关系**，并单独记录来源范围待核和整体暂缓的词根；暂缓不等于判定关系错误。其中保留原因和参考资料。另有 **2,364 条主表关系**未找到精确对应的逐条审核记录，不宜视为已逐条核实。
- 本次将旧条目 `lit`、`noun`、`opt`、`scen`（攀登义）和 `surr`（上升义）整体暂缓；原 ID 和原因保存在[待确认关系](notes/held-relations.json)。若已引用这些 ID，请先核对该记录。
- [修正与义项记录](notes/curation-corrections.json)包含来源错误修正、历史形式和同形词的适用范围、已迁移关系以及防护义 `para` 的重复条目对应。`porter` 的搬运工与守门人义项分别连接不同词根；`airport` 的机场义连接港口义 `port`。`tel` / `tele` 的远与终点已按义项拆分：原 ID 保留其中一个义项，引用旧例词关系时应查看迁移记录。
- 目前仍有 **2 个条目没有例词**。专名、古词和不同词形可出现在例词中，需按实际产品规则筛选；不要将每个例词的所有含义都归给该词根。

另对 **67 个单词的词根对应关系**补充了校验核实，相关记录和整理说明见 [notes](notes/README.md)。

## TODO

- [ ] 继续审核四个来源合并、去重后的词根与例词候选；本轮冻结队列共 14,262 条关系，已处理 9,134 条，仍有 **5,128 条待处理**。另有 10 条独立待确认记录；这些数量不等于主表未审核关系数量。候选包括已有关系、词缀、不同义项和证据不足的条目，不能直接视为可收录数据。
- [ ] 复核待确认关系，区分同形异义、同族变体、历史词形变化和跨越构词边界的字母匹配。
- [ ] 检查现有条目中沿用自来源的例词及英文 `meaning`，修正发现的问题；当前数据尚未全部逐词核实。
- [ ] 继续处理[待确认关系](notes/held-relations.json)和尚未关联到逐条审核记录的主表关系；不同来源的同形条目需要按词义与来源分别判断。
- [ ] 仅收录有独立构词依据的词根、前后缀及词基，继续处理没有例词的条目；按产品需要筛选专名、古词和不同词形。
- [ ] 后续发布时继续以 JSON 为准生成 CSV，并核对两个文件的一致性。

当前为整理中的阶段性数据；主 JSON 和 CSV 的例词字段不内嵌审核状态，使用时请同时参考上述状态文件。

原创整理成果采用 [CC BY-NC 4.0 非商业许可](LICENSE)，上游资料保留原许可，详见[来源与许可说明](notes/THIRD_PARTY_NOTICES.md)。
