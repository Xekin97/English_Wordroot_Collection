# port、duc/duct、brev 跨库补充

范围为 `port`（carry）、`duc/duct`（lead; draw along）和 `brev`（short）三组，对照 ECDICT、morphemes、generated-english-roots-list、engra，并结合词源词典整理。

| 分组 | 合并去重的候选词 | 纳入该组的词 | 本批新增到该组 |
| --- | ---: | ---: | ---: |
| port | 79 | 72 | 48 |
| duc/duct | 117 | 116 | 94 |
| brev | 15 | 9 | 9 |

主词表新增 **151 个去重单词、228 条词根—单词索引关系**。同族写法可共享单词，所以关系数不等于单词数。

补充写法：

- `-duce`：加入 `duc/duct` 分组，对应 `abduce`、`produce`、`reintroduce` 等结尾保留 duce 的相关动词。
- `brev`、`brevi`：新建分组，英文 meaning 沿用参考条目的 `short`，分别收录 9 个、7 个例词。

补入的例词包括 `importation`、`exportation`、`supporter`、`educational`、`conductivity`、`abbreviation`、`breviary` 等。保留参考资料收录的派生词及词形变化，不把同一基础词的不同拼写形式合并成一个词条。

关系修正与暂存：

- `portal`、`portcullis`、`portiere`、`portico` 对应 porta（门）；`opportune`、`passport` 对应 portus（港口）；`portion` 属于份额词族。这 7 项不并入 carry 义的 `port`。
- `microbrewery` 由 micro- 与 brewery 组成，排除其与 `brev` 的错误挂接。
- `condutor` 为源条目漏字，采用词典及其他条目收录的 `conductor`。
- `brief`、`briefer`、`briefing`、`briefly`、`briefness` 与 brevis 的历史联系单独保留，不加入 `brev/brevi` 的字面例词。
- `brevextensor` 在 [The Century Dictionary，第 676 页](https://archive.org/download/centurydictipt300whituoft/page/n135.jpg) 有收录，为罕见解剖术语，由 brevis extensor 缩合，只分配给 `brev`；其中的 e 属于 extensor，不能据此新增 `breve` 写法。
- `breve` 作为 `brev` 的例词保留；来源列出的 `breve-` 尚缺独立结合形式依据，本批不新增为词根条目。

同族写法是词源检索索引，不代表唯一的现代英语词素切分。例如 `brevity` 可同时关联 `brev` 和 `brevi`：词典支持 brevis/brevitas 的历史联系，[-ity 的词源](https://www.merriam-webster.com/dictionary/-ity)也说明其中 i 的词干元音来源；这与现代英语 `brev + -ity` 的分析可以并存。具体边界推断在逐条记录中注明。

基础词的词源和普通派生关系分别记录：`dictionary_headword` 表示查证了该词的词典条目，错拼项查证更正目标；`source_relation_and_verified_base` 表示结合参考库关系与已核实的基础词判断，并不声称每个派生词都有独立词源词典条目。多个库可能共享来源，不将收录次数当成独立证据数量。

逐条结果：[JSON](01-port-duc-brev.json) · [CSV](01-port-duc-brev.csv)。其中保留来源、分配到的词根、词源依据和义项限制；未纳入主表的候选也保留处理结果。
