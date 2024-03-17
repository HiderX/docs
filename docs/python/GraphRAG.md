# GraphRAG 

## 对我们项目的作用

把地理知识库以图节点的方式存入数据库（图数据库NebulaGraph，检索速度快），数据库与大语言模型交互

## 大模型局限性 

1、领域信息不足

2、有可能产生误导

3、无法获取实时信息

4、预训练数据不可更改

5、缺乏长期记忆

## 什么是Graph RAG 

RAG（Retrieval Argumented Generation）指的是通过 RAG 模型来对搜索结果进行增强的过程。具体来说，它是将检索技术和语言生成技术相结合来增强生成过程的一种技术，可以帮助传统搜索引擎生成更加准确、相关和多样化的信息来满足用户的需求。

Graph RAG是一种基于知识图谱的检索增强技术，通过构建图模型的知识表达，将实体和关系之间的联系用图的形式进行展示，然后利用大语言模型 LLM进行检索增强。

Graph RAG 将知识图谱等价于一个超大规模的词汇表，而实体和关系则对应于单词。通过这种方式，Graph RAG 在检索时能够将实体和关系作为单元进行联合建模。

## 知识图谱的组成

- 顶点/节点：英文对应是 Vertex 和 Node，无论是顶点还是节点，都表示知识领域中的实体或对象。每个节点对应一个唯一的实体，并通过唯一标识符进行标识。例如，本例的棒球队知识图谱中，节点可能有“Philadelphia Phillies”和“Major League Baseball”。

- 边：表示两个节点之间的关系。例如，一条边 `compete in`（参赛）可能连接 “Philadelphia Phillies” 的节点和 “Major League Baseball” 的节点。

- 三元组：是知识图谱的基本数据单元，由三个部分组成：
  主体（Subject）：三元组所描述的节点
  客体（Object）：关系指向的节点
  谓词（Predicate）：主体和客体之间的关系

  ![img](https://img-blog.csdnimg.cn/img_convert/50fa726f82e821a1341ba85bc785474b.png)

## 图探索的 7 种方式 



![img](https://pic1.zhimg.com/80/v2-5d0e28dd54c1b3f2d397015c775fd080_720w.webp)



## 链接
- [x] 知乎：https://zhuanlan.zhihu.com/p/670703395
- [ ] ​			https://zhuanlan.zhihu.com/p/660722382
- [x] csdn：https://blog.csdn.net/c9Yv2cf9I06K2A9E/article/details/131545871
- [ ] siwei.io：https://siwei.io/graph-rag/
- [ ] github：https://github.com/wenqiglantz/llamaindex_nebulagraph_phillies

