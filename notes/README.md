# 整理说明

以 ECDICT 的词根、英文 meaning 和例词为基础，参考 morphemes、generated-english-roots-list、engra 的相关条目进行对照整理。

1. 将一个分组中的词根写法分别列出，保留原分组和同族关联。
2. 整理对应单词并去重；同族变体允许共享例词，同形异义词根分别保留。
3. 保留原始英文 meaning；有历史拼写变化的关系单独记录，不强行按字符串匹配。
4. 另对 67 个单词的词根对应关系补充校验核实，记录依据、义项限制及必要修正。
5. 按词根分批对照各库，补充缺失词根写法和例词，分别保留确认关系、非字面联系、错拼、错误分组及待确认项。

补充记录：

- [67 条关系核实 JSON](adjudications.json) / [CSV](adjudications.csv)：逐条对应关系、说明和来源。
- [历史及非字面关系](related-only.json)：保留未直接放入主词表的关系及适用限制。
- [排除记录](excluded.json)：保留原库中被排除的关系及原因。
- [port、duc/duct、brev 跨库补充](batches/01-port-duc-brev.md)：本批新增例词、词根写法及逐条处理结果。
- [词根及例词补充](batches/02-supported-additions.md)：来源、适用范围及已补充的对应关系。
- [来源与许可说明](THIRD_PARTY_NOTICES.md)。
