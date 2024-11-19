# 基于jieba库分词和roberta进行词频统计-词典法应用

## 项目简介

使用jieba库进行中文文本分词，并结合RoBERTa模型计算词频和词向量相似度，最终生成AI关键词词频统计和近似词列表。
本项目主要方法路径来自于姚加权等（2024）的研究：
姚加权、张锟澎、郭李鹏、冯绪，2024：《人工智能如何提升企业生产效率？——基于劳动力技能结构调整的视角》，《管理世界》第2期。

- 默认提供的停用词表来自Wuhan Zhang整合的停用词库，具体可见 [https://github.com/endNone/stopwords](https://github.com/endNone/stopwords)

- 默认种子词文件为人工智能相关种子词

本项目旨在方便在经济学（或者其他学科）的研究中应用相关NLP模型开展词典法的应用

## 环境与依赖项

- Python 3.11.5
- pandas
- jieba
- tqdm
- transformers
- torch

## 使用方法

1. 确保所有文本文件和词典文件已放置在`cipingdata`目录下。
   并保证结构为：
cipingdata
├── seed_dict.csv # 种子词词典
├── stopwords.txt # 停用词文件
├── txt # 文本文件目录
│ ├── 企业名或编号1
│ │ ├── 年份1.txt
│ │ ├── 年份2.txt
│ │ └── ...
│ ├── 企业名或编号2
│ │ ├── 年份1.txt
│ │ ├── 年份2.txt
│ │ └── ...
│ └── ...
├── word_freq.csv # 词频统计结果（生成）
├── similar_words.csv # 近似词列表（生成）
└── words_all.csv # 所有近似词（生成）

运行`ciping_main.ipynb`中的代码单元格，完成以下步骤：
    - 加载停用词和种子词词典
    - 并发处理目录下的文本文件，统计词频
    - 删除频次小于5的词语，删除包含%或.的词语
    - 使用RoBERTa模型计算词向量相似度，生成近似词列表
    - 输出所有近似词并保存结果

结果文件：
    - `cipingdata/word_freq.csv`：词频统计结果
    - `cipingdata/similar_words.csv`：近似词列表
    - `cipingdata/words_all.csv`：所有近似词
    - `words_count_result.xlsx`：关键词词频统计结果

## 注意事项

- 请根据需要自行筛选和优化近似词列表。
- 默认垃圾词列表为AI词典中的词语，请视情况使用。
- 请一定确保文本文件目录格式正确

## 模型选择

本项目默认使用hfl/RoBERTa-wwm 模型进行词向量计算，用户可以根据需要在transformers库中选取其他模型。
