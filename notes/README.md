# 来源与补充记录

本目录提供数据来源、词根与例词关系的适用范围，以及未纳入主表的记录。词根数据和字段说明见[项目首页](../README.md)。

- [来源与许可说明](THIRD_PARTY_NOTICES.md)：各来源的许可及使用说明。
- [Wiktionary 逐条归属](wiktionary-attribution.json)：相关词根记录对应的词条、义项和贡献者历史。
- [WHO 来源索引](who-references.json)：药物命名相关条目所参考的 WHO 文档。
- [例词审核状态索引](edge-audit.json)：按词根 `id` 和例词查询审核状态、来源和适用范围；具体关系及来源存放于 [json](json/) 分片。
- [修正与义项记录](curation-corrections.json)：词义修正、关系迁移及词根条目的补充依据。
- [类别来源](class-provenance.json)：`class` 字段的来源类别及部分细分说明。
- [待确认关系](held-relations.json)和[来源归属待核关系](legacy-pending-relations.json)：暂缓的关系及原因。已有独立依据的其他词义和关系可以保留。
- [未收录候选](unverified-candidates.json)和[隔离例词关系](isolated-example-relations.json)：因证据不足或不符合来源范围而未纳入的记录；未收录不等于判定单词或词源错误。
- [历史及非字面关系](related-only.json)、[排除记录](excluded.json)和[证据不足的关系](unconfirmed-relations-excluded.json)：保留来源范围与历史整理记录。
- [67 条关系核实记录](adjudications.json)：部分例词与词根对应关系的依据和说明，也提供 [CSV 格式](adjudications.csv)。

审核索引、待确认关系、修正记录和类别来源中的 `roots_sha256` 用于标识它们所对应的数据快照。审核状态只适用于记录注明的来源或义项，不代表单词的所有含义均已核实。
