# English Wordroot Collection

英语词根、前缀、后缀及其他构词形式的数据集。每条记录提供英文含义和对应例词，可用于词根检索、词汇学习及选词。

数据共收录 **9,191 条词根及词缀记录**、**35,646 个不同例词或词组**和 **51,306 条词根与例词关系**。例词按大小写精确去重；同一单词出现在多个词根下时，在例词总数中只计一次。

本项目将来源中多个词根共用一组例词的记录，整理为每个词根写法对应自己的例词列表。同族变体可以共享例词；拼写相同但含义不同的词根分别记录，并用 `id` 区分。

## 数据文件

- [JSON](json/)：包含全部字段及同族关联。
- [CSV](csv/)：包含常用字段，例词以 ` | ` 分隔；文件使用 UTF-8 BOM。
- [单词到词根的反向索引](word-roots/)：通过单词或词组查找对应的词根 ID。

词根 JSON 和 CSV 均按词根（忽略大小写）和 `id` 排序，依次编号为 `roots-001` 至 `roots-010`。每份最多 1,000 条，最后一份包含 191 条。按编号拼接 JSON 数组即可得到完整数据；合并 CSV 时只保留一份表头。

下面的 Python 示例读取全部 JSON 分片，并查找展示写法为 `port` 的记录：

```python
import json
from pathlib import Path

roots = []
for path in sorted(Path("json").glob("roots-*.json")):
    roots.extend(json.loads(path.read_text(encoding="utf-8")))

for item in roots:
    if item["root"].casefold() == "port":
        print(item["id"], item["meaning"], item["example"])
```

`root` 可以重复，例如 `port` 包含不同含义；保存或关联记录时请使用 `id`。

## 从单词查词根

反向索引将每个例词或词组映射到词根 `id` 列表。例如 `airport` 对应 `air` 和港口义的 `port`。一个词可以对应多个词根，也可以对应相同写法的不同义项。

索引按原词形精确匹配，保留大小写、空格和标点；不在例词库中的词不会自动推断词根。索引共 36 个 JSON 分片，每份最多 1,000 个词；[manifest.json](word-roots/manifest.json) 记录各分片的词数、首尾词和校验值，首尾词按 Unicode 码点排序，可用于定位分片。

配合上面的 `roots` 列表，可以加载索引并查询：

```python
word_roots = {}
for path in sorted(Path("word-roots").glob("word-roots-*.json")):
    word_roots.update(json.loads(path.read_text(encoding="utf-8")))

roots_by_id = {item["id"]: item for item in roots}
for root_id in word_roots.get("airport", []):
    item = roots_by_id[root_id]
    print(item["root"], item["meaning"])
```

## JSON 字段

每个分片的顶层是数组，每个对象代表一条词根记录。

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `id` | string | 条目唯一标识。 |
| `root` | string | 用于展示的词根写法，不保证唯一。 |
| `source_form` | string | 采用的来源写法，可能包含连字符或义项编号。 |
| `meaning` | string | 词根的英文含义。 |
| `class` | string | 类别，如 `root`、`prefix`、`suffix`、`combining_form`；其他值包括历史词干和检索形式。 |
| `origin` | string | 词源或来源说明。 |
| `example` | string[] | 对应该记录的例词或词组。 |
| `family_id` | string | 词族分组标识。 |
| `related_root_ids` | string[] | 同一分组中其他条目的 `id`。 |
| `source_entry` | string | 基础来源条目或分组名称。 |
| `pending_family_examples` | integer | 历史分组待处理计数，未全面重新核算，不能用作当前待核总数。 |

CSV 包含 `id`、`root`、`source_form`、`meaning`、`class`、`origin`、`source_entry` 和 `example`。如需词族关联，请使用 JSON。

## 使用说明

- `meaning` 描述词根含义；`example` 没有逐词标注使用了该词根的哪个含义，也不意味着该单词的所有含义都与词根相关。
- 部分例词是有来源依据的历史同族或变体关系，不一定能按现代英语直接拆分；同一 `family_id` 下的写法也不一定可以互换。具体关系的来源与范围可查阅[例词审核状态](notes/edge-audit.json)。
- 例词中包含专名、古词和专业词汇，使用时可根据需要筛选。数据仍可能存在错误或遗漏。
- 未确认的具体来源关系另见[待确认关系](notes/held-relations.json)和[来源归属待核关系](notes/legacy-pending-relations.json)；同一个词在其他词义下的关系可能有独立依据。

## 数据来源

主要整理自 [ECDICT](https://github.com/skywind3000/ECDICT)、[morphemes](https://github.com/colingoldberg/morphemes)、[generated-english-roots-list](https://github.com/WithEnglishWeCan/generated-english-roots-list)、[engra](https://github.com/eslsoft/engra) 和 [LexiRoot](https://github.com/tcyeee/lexiroot)。

整理时还参考了 [MorphoLex-en](https://github.com/hugomailhot/MorphoLex-en)、[MorphyNet](https://github.com/kbatsuren/MorphyNet)、[etymology-db](https://github.com/droher/etymology-db)、[Wiktionary / Kaikki.org](https://kaikki.org/dictionary/English/)、[Merriam-Webster 构词词典](https://www.spellingbee.com/sites/default/files/inline-files/Merriam-Webster%27s%20Dictionary%20of%20Prefixes%2C%20Suffixes%2C%20and%20Combining%20Forms.pdf)、[WHO 药物命名资料](https://www.who.int/teams/health-product-policy-and-standards/inn)及其他词典和学术资料。逐条来源与补充记录见 [notes](notes/README.md)。

## 许可

本项目有权单独许可的原创整理贡献采用 [CC BY-NC 4.0](LICENSE)。上游资料适用的署名、相同方式共享或其他许可条件不因此改变；各来源及其许可见[来源与许可说明](notes/THIRD_PARTY_NOTICES.md)。
