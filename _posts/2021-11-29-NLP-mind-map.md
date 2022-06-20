---
layout: post
title: 自然语言处理的知识点框架图
date: 2021-11-29 19:24
category: AI
tags: [NLP, AI, python]
---

自然语言处理的知识点框架图


## 自然语言应用
（按技术层面划分）

### 基础技术

- 词法分析
- 句法分析
- 命名实体识别
- 语义分析
- 篇章分析
- 语言模型
- 词性标注

### 核心技术

- 机器翻译

	- BLEU 得分

- 文本摘要
- 文本分类
- 阅读理解
- 文本生成
- 情感分析

	- 基于词典的情感分析方法
	- 基于机器学习的情感分析方法
	- 分析的对象和结果

		- 文本

			- 句子
			- 段落
			- 文档

		- 情绪

			- 正面
			- 负面

- 智能问答

	- 按答案生成方式分类分类

		- 检索式问答系统
		- 生成式问答系统

	- 按求解问题分类

		- 事实型问题
		- 列表型问题
		- 定义型问题
		- 关系型问题
		- 观点型问题

### 应用

- 智能客服
- 搜索引擎
- 个人助理
- 推荐系统
- 舆情分析
- 知识图谱

## Python 适用的常见 NLP 工具

### 中文综合 NLP 工具包

- THULAC

- LTP

- BaiduLac

- HanLP

- FastNLP

- SnowNLP

- Tony-Wang/YaYaNLP

- SeanLee97/小明NLP

- rockingdingo/DeepNLP

- smilelight/lightNLP

- deepwel/Chinese-Annotator

- taozhijiang/chinese_nlp

- rockyzhengwu/FoolNLTK

- smoothnlp/SmoothNLP

- synyi/poplar

- ownthink/Jiagu

### 英语或多语言综合 NLP 工具包

- stanfordnlp/stanza

- NLTK

- spaCy

- BrikerMan/Kashgari

- chartbeat-labs/textacy

- RaRe-Technologies/gensim

### 中文分词

- Jieba 结巴中文分词

- 北大中文分词工具

- kcws 深度学习中文分词

- hankcs/ID-CNN-CWS

- Genius 中文分词

- loso 中文分词

- "哑哈"中文分词

- Moonshile/ChineseWordSegmentation

### 信息提取

### 问答和聊天机器人

### 中文语料库

- 开放知识图谱OpenKG.cn

- 开放中文知识图谱的schema

- 大规模中文概念图谱CN-Probase

- ownthink / 1.4亿中文知识图谱开源下载

- 农业知识图谱

- 中文 Wikipedia Dump

- 基于不同语料、不同模型（比如BERT、GPT）的中文预训练模型

- OpenCLaP 多领域开源中文预训练语言模型仓库

- to-shimo/chinese-word2vec

- Embedding/上百种预训练中文词向量

- 腾讯 AI - 超过 800 万个中文单词短语提供 200 维向量表示

- 中文预训练BERT with Whole Word Masking

- 中文 GPT2 训练代码 

- 中文语言理解测评基准 ChineseGLUE

- 中华新华字典数据库（歇后语、汉字、词语、成语）

- Synonyms 中文近义词工具包

- dgk_lost_conv 中文对白语料

- 中文突发事件语料库

- PTT 八卦版問答中文語料（繁体）

- 中文公开聊天语料库

- 中国股市公告信息爬取

- tushare 财经数据接口

- SmoothNLP 金融文本数据集

- 保险行业语料库

- 中华古诗词数据库

- DuReader Machine Reading Comprehension

- 中文语料小数据

- 中国文学文本的话语级命名实体识别和关系提取数据集

- 中文文本推断项目

- 大规模中文自然语言处理语料

- 中文人名语料库

- 中文敏感词词库

- 中文简称词库

- 公司名语料库

- 中文实体情感知识库

- 漢語拆字字典（繁体）

- 情感/观点/评论 倾向性分析

- 中文阅读理解数据库

## 常用于 NLP 的深度学习模型

### 循环模型

- RNN

	- 双向 RNN

- LSTM

	- 双向 LSTM

- GRU
- TextRNN

### 卷积模型

- TextCNN
- DCNN

### 递归模型

- Syntatically-Untied RNN

### Seq2seq
（2014）

### Transformer
（Google, 2017）

- Self-Attention
- Multi-Head Attention
- Masked Multi-Head Attention

### BERT
（Google, 2019）

- 自编码模型
（擅长自然语言理解）

### GPT-3
（OpenAI, 2020）

- 自回归模型
（擅长自然语言生成）

## 发展历史

### 基于规则

- 无法使用计算机进行泛化
- 鲁棒性差

### 基于统计

- 隐马尔可夫模型
Hidden Markov Model
- 朴素贝叶斯
Naive Bayes
- 条件随机场
Conditional Random Fields
- K-近邻算法
K-Nearest Neighbors algorithm, KNN
- 支持向量机
Support Vector Machine, SVM
- 决策树
Decision Tree
- K-均值
K-means

### 基于深度学习

## 一般应用处理流程

### 1. 语料获取

- 已有语料
- 公开数据集
- 爬虫

### 2. 数据预处理

- 语料清洗
- 分词
- 词性标注
- 去停用词

### 3. 特征工程

- 向量化

### 4. 特征选择

- 合适的
- 表达能力强的

### 5. 模型选择

- 机器学习模型
- 深度学习模型

### 6. 模型训练

- 模型微调

### 7. 模型评估

- 准确率
- 召回率
- 精准度
- F1 值
- ROC、AUC

### 8. 投产上线

- 线下训练后部署
- 在线持久化训练

## 自然语言应用
（按两端的类型来划分）

### 一对一

- 中文分词
- 词性标注
- 语义角色标注

### 一对多

- 文本生成
- 图像描述生成

### 多对一

- 文本分类
- 情感分析

### 多对多

- 机器翻译
- 自动摘要
- 聊天机器人

## Attention 机制
（2015）

### 保留隐态各状态提供给解码器

## 自然语言应用
（按照阅读和理解来分类）

### 自然语言理解 NLU

### 自然语言生成 NLG

- 文本到文本的生成

	- 文本摘要

		- 抽取式摘要

			- 论文自动生成摘要
			- 根据文字直播生成赛事报道

		- 生成式摘要

	- 古诗生成
	- 文本复述

		- 使用机器翻译的方法生成文本复述

- 数据到文本的生成

	- 新闻报道生成

- 图像到文本的生成

	- 为图像生成解释性文本
	- 故事生成
	- 基于图像的问答任务

