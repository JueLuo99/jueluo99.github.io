---
layout: post
title: 常用的中文 NLP 库整理
date: 2021-10-23 20:34
category: AI
tags: [nlp, chinese, deep learning, AI]
---

整理一些自己日常学习中常用到的中文 NLP 库

- [常用的中文 NLP 库整理](#常用的中文-nlp-库整理)
  - [各常见工具库功能对比](#各常见工具库功能对比)
  - [NLP 常见中英文对照](#nlp-常见中英文对照)
  - [词性标注标签含义（PKU 规范）](#词性标注标签含义pku-规范)
- [jieba](#jieba)
  - [安装](#安装)
  - [分词](#分词)
  - [强制调高调低词频](#强制调高调低词频)
  - [关键词提取（基于 TF-IDF 算法）](#关键词提取基于-tf-idf-算法)
  - [关键词提取（基于 TextRank 算法）](#关键词提取基于-textrank-算法)
  - [词性标注](#词性标注)
- [SnowNLP](#snownlp)
  - [安装](#安装-1)
  - [引用和准备](#引用和准备)
  - [分词](#分词-1)
  - [词性标注](#词性标注-1)
  - [情感分析（返回 positive 的概率）](#情感分析返回-positive-的概率)
  - [汉字转拼音](#汉字转拼音)
  - [关键词提取](#关键词提取)
  - [文本摘要](#文本摘要)
  - [自动分句](#自动分句)
- [Jiagu](#jiagu)
  - [安装](#安装-2)
  - [引用](#引用)
  - [中文分词](#中文分词)
  - [知识图谱关系抽取（作者仍在完善中）](#知识图谱关系抽取作者仍在完善中)
  - [关键词提取](#关键词提取-1)
  - [文本摘要](#文本摘要-1)
  - [情感分析](#情感分析)
- [Macropodus](#macropodus)
  - [安装](#安装-3)
  - [引用](#引用-1)
  - [分词](#分词-2)
  - [新词发现](#新词发现)
  - [文本摘要](#文本摘要-2)
  - [关键词抽取](#关键词抽取)
  - [文本相似度](#文本相似度)
  - [中文汉字转拼音](#中文汉字转拼音)
  - [中文繁简转换](#中文繁简转换)
  - [科学计算器](#科学计算器)
- [HanLP](#hanlp)
  - [安装](#安装-4)
  - [轻量级 RESTful API 使用](#轻量级-restful-api-使用)
  - [海量级 native API 使用](#海量级-native-api-使用)
  - [单独使用 native API 的单个功能](#单独使用-native-api-的单个功能)
- [LTP](#ltp)
  - [安装](#安装-5)
  - [导包与初始化](#导包与初始化)
  - [分词](#分词-3)
  - [词性标注（需要先分词）](#词性标注需要先分词)
  - [命名实体识别（需要先分词）](#命名实体识别需要先分词)
  - [语义角色标注（需要先分词）](#语义角色标注需要先分词)
  - [依存句法分析（需要先分词）](#依存句法分析需要先分词)
  - [语义依存分析（需要先分词）](#语义依存分析需要先分词)
- [THULAC](#thulac)
  - [安装](#安装-6)
  - [引用和初始化](#引用和初始化)
  - [Python 3.8 及以上版本的错误处理](#python-38-及以上版本的错误处理)
  - [分词及词性标注](#分词及词性标注)
- [pkuseg](#pkuseg)
  - [安装](#安装-7)
  - [引用](#引用-2)
  - [分词](#分词-4)
  - [词性标注](#词性标注-2)
- [zhconv](#zhconv)


# 常用的中文 NLP 库整理


下面准备两段文本以供下文演示使用

```python
TEXT = "自然语言处理是计算机科学领域与人工智能领域中的一个重要方向。"

TEXT2 = u'''
自然语言处理是计算机科学领域与人工智能领域中的一个重要方向。
它研究能实现人与计算机之间用自然语言进行有效通信的各种理论和方法。
自然语言处理是一门融语言学、计算机科学、数学于一体的科学。
因此，这一领域的研究将涉及自然语言，即人们日常使用的语言，
所以它与语言学的研究有着密切的联系，但又有重要的区别。
自然语言处理并不是一般地研究自然语言，
而在于研制能有效地实现自然语言通信的计算机系统，
特别是其中的软件系统。因而它是计算机科学的一部分。
'''
```


## 各常见工具库功能对比

以下内容根据各库官方文档整理而来，仅供参考，可能并不准确
| 库名                                                 | 分词 | 关键词提取 | 词性标注 | 情感分析 | 文本摘要 | 自定义词典 | 新词发现 | 依存句法分析 | 语义依存分析 | 语义角色标注 | 其他功能                                                                       |
| ---------------------------------------------------- | ---- | ---------- | -------- | -------- | -------- | ---------- | -------- | ------------ | ------------ | ------------ | ------------------------------------------------------------------------------ |
| [jieba](https://github.com/fxsjy/jieba)              | ✔    | ✔          | ✔        |          |          | ✔          | ✔        |              |              |              | 繁体分词                                                                       |
| [snownlp](https://github.com/isnowfy/snownlp)        | ✔    |            | ✔        | ✔        | ✔        |            |          |              |              |              | 繁体转简体、转换成拼音                                                         |
| [Jiagu](https://github.com/ownthink/Jiagu)           | ✔    | ✔          | ✔        | ✔        |          |            | ✔        |              |              |              | 文本聚类、知识图谱关系抽取                                                     |
| [Macropodus](https://github.com/yongzhuo/Macropodus) | ✔    | ✔          |          |          | ✔        |            | ✔        |              |              |              | 文本相似度、中文数字阿拉伯数字互转、罗马数字与阿拉伯数字互转、中文繁简拼音互转 |
| [HanLP](https://github.com/hankcs/pyhanlp)           | ✔    | ✔          | ✔        | ✔        | ✔        | ✔          | ✔        | ✔            | ✔            | ✔            | 感知机词法分析、拼音简繁                                                       |
| [LTP](https://github.com/HIT-SCIR/ltp)               | ✔    |            | ✔        |          |          |            |          | ✔            | ✔            | ✔            |                                                                                |
| [THULAC](https://github.com/thunlp/THULAC-Python)    | ✔    |            | ✔        |          |          | ✔          |          |              |              |              |                                                                                |
| [pkuseg](https://github.com/lancopku/pkuseg-python)  | ✔    |            | ✔        |          |          | ✔          |          |              |              |              |                                                                                |



## NLP 常见中英文对照

| 英文缩写 | 英文全称                           | 中文         |
| -------- | ---------------------------------- | ------------ |
| tok      | Tokenization                       | 分词         |
| pos      | Part-of-Speech Tagging             | 词性标注     |
| lem      | Lemmatization                      | 词干提取     |
| fea      | Features of Universal Dependencies | 词法语法特征 |
| ner      | Named Entity Recognition           | 命名实体识别 |
| dep      | Dependency Parsing                 | 依存句法分析 |
| con      | Constituency Parsing               | 短语成分分析 |
| srl      | Semantic Role Labeling             | 语义角色标注 |
| sdp      | Semantic Dependency Parsing        | 语义依存分析 |
| amr      | Abstract Meaning Representation    | 抽象意义表示 |



## 词性标注标签含义（PKU 规范）

| 词性 | 含义     |
| ---- | :------- |
| n    | 名词     |
| t    | 时间词   |
| s    | 处所词   |
| f    | 方位词   |
| m    | 数词     |
| q    | 量词     |
| b    | 区别词   |
| r    | 代词     |
| v    | 动词     |
| a    | 形容词   |
| z    | 状态词   |
| d    | 副词     |
| p    | 介词     |
| c    | 连词     |
| u    | 助词     |
| y    | 语气词   |
| e    | 叹词     |
| o    | 拟声词   |
| i    | 成语     |
| l    | 习惯用语 |
| j    | 简称     |
| h    | 前接成分 |
| k    | 后接成分 |
| g    | 语素     |
| x    | 非语素字 |
| w    | 标点符号 |
| nr   | 人名     |
| ns   | 地名     |
| nt   | 机构名称 |
| nx   | 外文字符 |
| nz   | 其它专名 |
| vd   | 副动词   |
| vn   | 名动词   |
| vx   | 形式动词 |
| ad   | 副形词   |



# jieba

项目主页：[fxsjy/jieba: 结巴中文分词](https://github.com/fxsjy/jieba)



## 安装

```bash
pip install jieba
```



## 分词

```python
import jieba

seg_list = jieba.cut(TEXT)
# 可以使用 HMM 自动新词发现
# seg_list = jieba.cut(TEXT, HMM=True)
print(" ".join(seg_list))
```
```bash
自然语言 处理 是 计算机科学 领域 与 人工智能 领域 中 的 一个 重要 方向 。
```



## 强制调高调低词频

```python
# 将词汇加入词典
jieba.add_word('自然语言处理')
# 将词汇移出词典
jieba.del_word('自然语言处理')
```



## 关键词提取（基于 TF-IDF 算法）

```python
jieba.analyse.extract_tags(TEXT2, topK=5)
```

```bash
['自然语言', '计算机科学', '语言学', '研究', '领域']
```



## 关键词提取（基于 TextRank 算法）

```python
jieba.analyse.textrank(TEXT2, topK=5)
```

```bash
['领域', '研究', '计算机科学', '实现', '处理']
```



## 词性标注

```python
import jieba.posseg as pseg

words = pseg.cut(TEXT)
for word, flag in words:
    print('%s %s' % (word, flag))
```

```bash
自然语言 l
处理 v
是 v
计算机科学 n
领域 n
与 p
人工智能 n
领域 n
中 f
的 uj
一个 m
重要 a
方向 n
。 x
```



# SnowNLP

项目主页：[isnowfy/snownlp: Python library for processing Chinese text](https://github.com/isnowfy/snownlp)



## 安装

```bash
pip install snownlp
```



## 引用和准备

```python
from snownlp import SnowNLP

s = SnowNLP(TEXT)
s2 = SnowNLP(TEXT2)
```



## 分词

```python
print(s.words)
```

```bash
['自然',
 '语言',
 '处理',
 '是',
 '计算机',
 '科学',
 '领域',
 '与',
 '人工',
 '智能',
 '领域',
 '中',
 '的',
 '一个',
 '重要',
 '方向',
 '。']
```



## 词性标注

```python
list(s.tags)
```

```bash
[('自然', 'n'),
 ('语言', 'n'),
 ('处理', 'v'),
 ('是', 'v'),
 ('计算机', 'n'),
 ('科学', 'n'),
 ('领域', 'n'),
 ('与', 'c'),
 ('人工', 'b'),
 ('智能', 'n'),
 ('领域', 'n'),
 ('中', 'f'),
 ('的', 'u'),
 ('一个', 'm'),
 ('重要', 'a'),
 ('方向', 'n'),
 ('。', 'w')]
```



## 情感分析（返回 positive 的概率）

```python
print(s.sentiments)
```

```bash
0.9999941826524298
```



## 汉字转拼音

```python
print(s.pinyin)
```

```bash
['Zi',
 'ran',
 'yu',
 'yan',
 'chu',
 'li',
 'shi',
 'ji',
 'suan',
 'ji',
 'ke',
 'xue',
 'ling',
 'yu',
 'yu',
 'ren',
 'gong',
 'zhi',
 'neng',
 'ling',
 'yu',
 'zhong',
 'de',
 'yi',
 'ge',
 'zhong',
 'yao',
 'fang',
 'xiang',
 '。']
```



## 关键词提取

```python
s2.keywords(3)
```

```bash
['语言', '自然', '计算机']
```



## 文本摘要

```python
print(s2.summary(3))
```

```bash
['因而它是计算机科学的一部分',
 '自然语言处理是计算机科学领域与人工智能领域中的一个重要方向',
 '自然语言处理是一门融语言学、计算机科学、数学于一体的科学']
```



## 自动分句

```python
print(s2.sentences)
```

```bash
['自然语言处理是计算机科学领域与人工智能领域中的一个重要方向',
 '它研究能实现人与计算机之间用自然语言进行有效通信的各种理论和方法',
 '自然语言处理是一门融语言学、计算机科学、数学于一体的科学',
 '因此',
 '这一领域的研究将涉及自然语言',
 '即人们日常使用的语言',
 '所以它与语言学的研究有着密切的联系',
 '但又有重要的区别',
 '自然语言处理并不是一般地研究自然语言',
 '而在于研制能有效地实现自然语言通信的计算机系统',
 '特别是其中的软件系统',
 '因而它是计算机科学的一部分']
```



# Jiagu

项目主页：[ownthink/Jiagu: Jiagu深度学习自然语言处理工具 知识图谱关系抽取 中文分词 词性标注 命名实体识别 情感分析 新词发现 关键词 文本摘要 文本聚类](https://github.com/ownthink/Jiagu)



## 安装

```bash
pip install jiagu
```



## 引用

```python
import jiagu
```



## 中文分词

```python
words = jiagu.seg(TEXT)
print(words)

# 两种加载自定义词典方式（文件和列表）
# jiagu.load_userdict('dict/user.dict')
# jiagu.load_userdict(['自然语言处理'])
```

```bash
['自然', '语言', '处理', '是', '计算机科学', '领域', '与', '人工智能', '领域', '中', '的', '一个', '重要', '方向', '。']
```



## 知识图谱关系抽取（作者仍在完善中）

```python
text = '姚明1980年9月12日出生于上海市徐汇区，祖籍江苏省苏州市吴江区震泽镇，前中国职业篮球运动员，司职中锋，现任中职联公司董事长兼总经理。'
knowledge = jiagu.knowledge(text)
print(knowledge)
```

```bash
[['姚明', '出生日期', '1980年9月12日'], 
['姚明', '出生地', '上海市徐汇区'], 
['姚明', '祖籍', '江苏省苏州市吴江区震泽镇']]
```



## 关键词提取

```python
keywords = jiagu.keywords(TEXT2, 5)
print(keywords)
```

```bash
['语言', '重要', '研究', '计算机科学', '领域']
```



## 文本摘要

```python
summarize = jiagu.summarize(TEXT2, 3) # 摘要
print(summarize)
```

```bash
['自然语言处理是计算机科学领域与人工智能领域中的一个重要方向。', 
'自然语言处理是一门融语言学、计算机科学、数学于一体的科学。', 
'自然语言处理并不是一般地研究自然语言，而在于研制能有效地实现自然语言通信的计算机系统，特别是其中的软件系统。']

```



## 情感分析

```python
sentiment = jiagu.sentiment(TEXT)
print(sentiment)
```

```bash
('positive', 0.5022491674491385)
```



# Macropodus

项目主页：[yongzhuo/Macropodus: 自然语言处理工具Macropodus，基于Albert+BiLSTM+CRF深度学习网络架构，中文分词，词性标注，命名实体识别，新词发现，关键词，文本摘要，文本相似度，科学计算器，中文数字阿拉伯数字(罗马数字)转换，中文繁简转换，拼音转换。tookit(tool) of NLP，CWS(chinese word segnment)，POS(Part-Of-Speech Tagging)，NER(name entity recognition)，Find(new words discovery)，Keyword(keyword extraction)，Summarize(text summarization)，Sim(text similarity)，Calculate(scientific calculator)，Chi2num(chinese number to arabic number)](https://github.com/yongzhuo/Macropodus)



## 安装

```bash
pip install macropodus
```



## 引用

```python
import macropodus
```



## 分词

```python
words = macropodus.cut(TEXT)
print(" ".join(words))
```

```bash
自然 语言 处理 是 计算机科学 领域 与 人工智能 领域 中的 一个 重要 方向 。
```



## 新词发现

```python
new_words = macropodus.find(TEXT)
print(new_words)
```

```bash
OrderedDict([('领域', {'a': 1.954304, 'r': 1.0, 'l': 1.0, 'f': 2, 'ns': 0.779392, 's': 3.046336})])
```



## 文本摘要

```python
sum = macropodus.summarize(TEXT2)
print(sum)
```

```bash
[(0.11166493879895197, '所以它与语言学的研究有着密切的联系，但又有重要的区别'), 
(0.111456788084211, '自然语言处理是计算机科学领域与人工智能领域中的一个重要方向'), 
(0.11142549186062257, 
'它研究能实现人与计算机之间用自然语言进行有效通信的各种理论和方法'), 
(0.11130109445110857, '而在于研制能有效地实现自然语言通信的计算机系统，'), 
(0.11121725232156135, '因此，这一领域的研究将涉及自然语言，即人们日常使用的语言，'), 
(0.11098393816916619, '因而它是计算机科学的一部分')]
```



## 关键词抽取


```python
keyword = macropodus.keyword(TEXT2)
print(keyword)
```

```bash
[(0.05564029050840573, '自然'), (0.054388064653720425, '语言'), (0.048799148883632536, '计算机科学'), (0.046954259386264845, '领域'), (0.04470438240778767, '研究'), (0.0390803472982575, '重要')]
```



## 文本相似度

```python
sim = macropodus.sim(sent1, sent2)
print(sim)
```

```bash
0.6502261253503653
```



## 中文汉字转拼音

```python
res_pinyin = macropodus.pinyin(TEXT)
print(res_pinyin)
```

```bash
['zi', 'ran', 'yu', 'yan', 'chu', 'li', 'shi', 'ji', 'suan', 'ji', 'ke', 'xue', 'ling', 'ren', 'gong', 'zhi', 'neng', 'ling', 'zhong', 'de', 'yi', 'ge', 'zhong', 'yao', 'fang', 'xiang']
```



## 中文繁简转换


```python
res_zh2han = macropodus.zh2han(TEXT)
print(res_zh2han)
res_han2zh = macropodus.han2zh(res_zh2han)
print(res_han2zh)
```

```bash
自然語言處理是計算機科學領域與人工智能領域中的一個重要方向。
自然语言处理是计算机科学领域与人工智能领域中的一个重要方向。
```



## 科学计算器

```python
sen_calculate = "23 + 13 * (25+(-9-2-5-2*3-6/3-40*4/(2-3)/5+6*3))加根号144你算得几多"
score_calcul = macropodus.calculate(sen_calculate)
print(score_calcul)
```

```bash
698.000000
```



# HanLP

项目主页：[hankcs/HanLP: 中文分词 词性标注 命名实体识别 依存句法分析 成分句法分析 语义依存分析 语义角色标注 指代消解 风格转换 语义相似度 新词发现 关键词短语提取 自动摘要 文本分类聚类 拼音简繁转换 自然语言处理](https://github.com/hankcs/HanLP)

在线演示：[HanLP在线演示 多语种自然语言处理](https://hanlp.hankcs.com/)

这个库现已升级至 2.X ，与旧版本 1.X 的 `pyhanlp` 库使用方式完全不同



## 安装

轻量级 RESTful API (使用官方服务器进行计算，[API 申请](https://bbs.hanlp.com/t/hanlp2-1-restful-api/53))
```bash
pip install hanlp_restful
```

海量级 native API （使用本机进行计算）

```bash
pip install hanlp
```



## 轻量级 RESTful API 使用

```python
from hanlp_restful import HanLPClient

# auth 不填则匿名，zh 中文，mul 多语种
HanLP = HanLPClient('https://www.hanlp.com/api', auth=None, language='zh') 
doc = HanLP.parse(TEXT)
doc.pretty_print()
```

![HanLP结果展示](.\常用的中文 NLP 库整理.assets\HanLP结果展示.png)

上图的结果可以看出结果包含了中文分词、词性标注、实体命名识别、依赖项解析、语义角色标记等内容



如果不使用 `pretty_print()` 函数，则会返回一个 `json` ，其中同样会包含上述内容，但需要自行解析以便查看



## 海量级 native API 使用

初次使用会下载一个略大于 1 GiB 的语料库，默认会保存至 `C:\Users\[USERNAME]\AppData\Roaming\hanlp\` 下

```python
import hanlp

# 世界最大中文语料库
HanLP = hanlp.load(hanlp.pretrained.mtl.UD_ONTONOTES_TOK_POS_LEM_FEA_NER_SRL_DEP_SDP_CON_XLMR_BASE)
doc = HanLP(TEXT)
doc.pretty_print()
```

输出结果与 RESTful API 完全一致，此处不再展示



## 单独使用 native API 的单个功能

```python
import hanlp

HanLP = hanlp.load(hanlp.pretrained.mtl.UD_ONTONOTES_TOK_POS_LEM_FEA_NER_SRL_DEP_SDP_CON_XLMR_BASE)
doc = HanLP(TEXT, tasks='tok')
doc.pretty_print()
```

```bash
自然 语言 处理 是 计算机 科学 领域 与 人工智能 领域 中 的一个 重要 方向 。
```

只需修改上方代码的第 4 行，即可选择需要执行的任务，例如修改为 `tasks='dep'` 则只会执行分词和依存句法分析（RESTful API 使用单个功能的方法与此相同）

同样地，如果不使用 `pretty_print()` 函数，则会返回一个 `json` ，可以自行解析结果使用



# LTP

项目主页：[HIT-SCIR/ltp: Language Technology Platform](https://github.com/HIT-SCIR/ltp)

开发者：哈工大社会计算与信息检索研究中心（HIT-SCIR）



## 安装

```bash
pip install ltp
```



## 导包与初始化

```python
from ltp import LTP

# 使用默认模型，也可指定自行下载的模型
ltp = LTP() 
```



## 分词

```python
seg, hidden = ltp.seg([TEXT])
print(seg)
```

```bash
[['自然语言', '处理', '是', '计算机', '科学', '领域', '与', '人工智能', '领域', '中', '的', '一个', '重要', '方向', '。']]
```



## 词性标注（需要先分词）

```python
pos = ltp.pos(hidden)
print(pos)
```

```bash
[['n', 'v', 'v', 'n', 'n', 'n', 'c', 'n', 'n', 'nd', 'u', 'm', 'a', 'n', 'wp']]
```



## 命名实体识别（需要先分词）

```python
ner = ltp.ner(hidden)
print(ner)
```

```bash
[[]]
```



## 语义角色标注（需要先分词）

```python
srl = ltp.srl(hidden)
print(srl)
```

```bash
[[[], [], [('A0', 0, 1), ('A1', 3, 13)], [], [], [], [], [], [], [], [], [], [], [], []]]
```



## 依存句法分析（需要先分词）

```python
dep = ltp.dep(hidden)
print(dep)
```

```bash
[[(1, 2, 'FOB'), (2, 3, 'SBV'), (3, 0, 'HED'), (4, 6, 'ATT'), (5, 6, 'ATT'), (6, 10, 'ATT'), (7, 9, 'LAD'), (8, 9, 'ATT'), (9, 6, 'COO'), (10, 14, 'ATT'), (11, 10, 'RAD'), (12, 14, 'ATT'), (13, 14, 'ATT'), (14, 3, 'VOB'), (15, 3, 'WP')]]
```



## 语义依存分析（需要先分词）

```python
sdp = ltp.sdp(hidden)
print(sdp)
```

```bash
[[(1, 2, 'FEAT'), (2, 3, 'dEXP'), (3, 0, 'Root'), (4, 6, 'FEAT'), (5, 6, 'FEAT'), (6, 9, 'eCOO'), (7, 9, 'mRELA'), (8, 9, 'FEAT'), (9, 14, 'LOC'), (10, 9, 'mDEPD'), (11, 9, 'mDEPD'), (12, 14, 'MEAS'), (13, 14, 'FEAT'), (14, 3, 'LINK'), (15, 3, 'mPUNC')]]
```



# THULAC

项目主页：[thunlp/THULAC-Python: 一个高效的中文词法分析工具包](https://github.com/thunlp/THULAC-Python)



## 安装

通过 pip 下载会同时下载一个模型文件
```bash
pip install thulac
```



## 引用和初始化

```python
import thulac

thu = thulac.thulac()
```



## Python 3.8 及以上版本的错误处理

因为 Python 3.8 开始不再拥有 `time.clock()`，所以直接使用会导致程序异常

可以通过添加以下代码解决

```python
import time
setattr(time, "clock", time.perf_counter)
```



## 分词及词性标注

```python
text = thu.cut(TEXT)
print(text)
```

```bash
[['自然', 'n'], ['语言', 'n'], ['处理', 'v'], ['是', 'v'], ['计算机', 'n'], ['科学', 'n'], ['领域', 'n'], ['与', 'p'], ['人工智能', 'n'], ['领域', 'n'], ['中', 'f'], ['的', 'u'], ['一个', 'm'], ['重要', 'a'], ['方向', 'n'], ['。', 'w']]
```



# pkuseg

项目主页：[lancopku/pkuseg-python: pkuseg多领域中文分词工具; The pkuseg toolkit for multi-domain Chinese word segmentation](https://github.com/lancopku/pkuseg-python)



## 安装

```bash
pip install pkuseg
```



## 引用

```python
import pkuseg
```



## 分词

```python
# 以默认配置加载模型
seg = pkuseg.pkuseg()
text = seg.cut(TEXT)
print(text)
```

```bash
['自然', '语言', '处理', '是', '计算机', '科学', '领域', '与', '人工', '智能', '领域', '中', '的', '一个', '重要', '方向', '。']
```



## 词性标注

```python
# 开启词性标注功能
seg = pkuseg.pkuseg(postag=True)
text = seg.cut(TEXT)
print(text)
```

```bash
[('自然', 'n'), ('语言', 'n'), ('处理', 'v'), ('是', 'v'), ('计算机', 'n'), ('科学', 'n'), ('领域', 'n'), ('与', 'p'), ('人工', 'b'), ('智能', 'n'), ('领域', 'n'), ('中', 'f'), ('的', 'u'), ('一个', 'm'), ('重要', 'a'), ('方向', 'n'), ('。', 'w')]
```



# zhconv

一个轻量级的繁简转换工具，支持地区词转换

TODO