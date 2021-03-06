关于Graph Database
---
    
> Categories: 语义网  
> Time: 2012-12-03  
> Original url: <http://baojie.org/blog/2012/12/03/graph-databas/>
    
2012年4月到12月间一些关于Graph Database微博的汇总

<http://www.weibo.com/xiguadawanzitang/profile?is_tag=1&tag_name=GraphDB>

OWL推理一个思路是通过hypertableau，做模型构造。另一个思路是作为图论问题，通过图的构造，最大化可并行性任务(如“或”)。在推理任务的另一端，简单如 semantic wiki的推理，我们也发现推理的所有任务都可以归结到图的路径计算。http://t.cn/zjVMZsw 用图数据库做语义网的数据平台是很自然的

我个人最喜欢OrientDB，知识建模灵活，内置推理，查询语法易懂。唯一的问题是那个公司太小，还没有证明自己的稳定性，用的人很少。Titan如果发展好了，很有希望，阵容很强大，但是现在还早了点。Neo4j用的人最多，不过能力最弱//@卢小东-知识梳理: 如果要兼顾语义知识库管理的难度，不知道哪个更适合？

另外，图数据库往往和其他数据库结合，做多级存储，获得性能和表达力的折衷。其实数据库的大部分并不需要图查询。搞大点的内存，用内存模式跑图数据库，持久化非图结构数据到其他，比如mongodb或elastic aearh//@SiDT:使用Neo4j，规模大了，性能会有问题。ID不能指定，有其他更好推荐吗

回复@SiDT:看你的规模有多大。几十万用户的话，做适当的数据分割，neo4j应该可以拿下。orientdb的并行版本应该也可以。Titan并行支持最好，在cassandra和hbase上都能跑；不过太新，文档不全，各种编程接口也很初级 //@SiDT:使用Neo4j，规模大了，性能会有问题。ID不能指定，有其他更好推荐吗

关联图数据库和elastic search。甚至可能用gremlin或类似orientdb sql的语言直接检索索引//@SiDT:存取和关系计算是强项，但检索是难点，有好的方案么

图数据库比语义数据库好的四个原因 1 构造更简单，对字符串更友好，避免过早优化 2 对大规模并行支持好，有现成的解决方案 3 工具系统集成好，json数据交换 4 本身支持sparql甚至推理，所以相对语义数据库并没失去什么

回复@个体小知: pregel和hama之类，表达力有限，一般适合传统图论操作，和titan, orientdb, neo4j这种图形数据库比，上面还要再包装一层属性图查询语言才能好用。但是这种包装现在还没有。Titan在大规模分布式上已经做得很好了 //@个体小知:所以适合不大不小，夹在中间的公司

使用在各种图数据库里，Titan是个新生，不过貌似潜力惊人 http://t.cn/zlboiMo 。作者Marko Rodriguez就是图数据库标准Blueprint的奠基人

其实在这个三个里面, OrientDB算是最容易用的，。pregel现在支持硬盘模式吗？对小公司，prege，hama这些都有点重了。 //@个体小知: 貌似是夹在中间，论成熟文档易上手不如neo4j，论性能强大灵活不如pregel

OrientDB文档通读了一遍。几个感想1) 比Neo4j灵活，强大，但是文档不够全，bug不知道会不会多 2) 貌似比neo4j更能支持cluster，节点自动组网，每节点可以每秒15万条插入，100万用户以下应该都够用 3) 适合不懂语义、图DB，只懂SQL的程序员来学习 4） 内置推理，连推理机都不用了。 5）SPARQL可以去死了

RDF数据库由于三元组的无组织性(organization, context)，索引结构不免复杂和冗余。同样规模的数据，triple store和图数据库比，磁盘空间消耗常大10倍，相应的I/O和网络消耗都大，性能上不能满足需求也就可以理解了

数据冗余和实时一致性在Web应用中通常都不是问题。在数据源分布、用户行为被验证之前就明确（符合第三范式的）数据schema本质上是一种过早优化。RDF引入schema，特别是OWL，是推理的过早优化。图数据库则把存储结构和推理变成逐步验证的过程，优化用户需要部分，很适合lean startup的原则

RB+-tree在图形数据库中做索引，做局域索引，据说上可以和图本身的大小无关。很神奇

Web 1.0的模型是普通图。Web 3.0的模型可能是属性图(Property Graph)。肯定不是RDF Graph 其实RDF1.1努力的方向就是把RDF变得更像一个图数据库(graph database)语言。那为何不直接

用图数据库呢？工程的稳定性还更好些。Freebase底层就是图数据库

到底是OrientDB好呢，还是neo4j好？纠结，纠结

不允许字符串做主语subject是RDF让人很不爽的一个地方。有这限制是为了模型论语义——这是整个W3C体系的一个问题: 工程的方便性让位于模型论语义的精确性。在RDF OWL RIF SPARQL里我们反复看到这个主题。这大概是非W3C的graph database后来居上的原因吧

RDF用URL做节点和关系的名字困惑了很多人。很多场合下，没必要精确到URL这个级别，字符串就很好了。Property graph在这点上比RDF GRAPH方便很多

什么是图形数据库? 本质上是分布式索引。

最近在看Graph Database, 不禁想，搞这个的，其实也就是一小群hacker，和美国欧洲各大学校+公司+W3C不能比，结果两三年的功夫，把多少亿美元投入、成千上万的研究人员、上十个工作组在“语义网”上的工作生生得给比下去了。什么叫实事求是的力量啊，这就是

例证：<http://t.cn/zOKYqXR> 在Google Insights里，neo4j一家就单挑triple store和SPARQL了。

Blueprint技术堆栈比语义网的W3C蛋糕模型看起来要靠谱得多。 http://t.cn/zOKYPma 现在用Blueprint方案数据库的用户（比如neo4j）要远远多于RDF triple store。这还只是多种非W3C路线的语义网解决方案的一种。

更正：Neo4j的商业版本也要2.4万美元一年（或者AGPL，最严格的开源协议）。我一开始以为是免费的。

从web到semantic web，从数学上讲不过是从single relation graph到multi-relation graph。可这么一个”简单”的进步，在工程上大概要花30年才能完全实现。这个世界的进步，并没有想象的那么快

纯nerdness：Gremlin是一个图灵机完备的查询语言。从表达力上讲，啥都可以说。定义个SPARQL到Gremlin的转化理论上是可以做到的。所以所有的graph database都是SPARQL-ready

RDF Virtual Machine by Marko A. Rodriguez http://t.cn/zOK7kFT 有点意思。这位老哥是图形数据库的主要人物之一，Germlin的发明人。

语义网的数据库也该考虑支持支持Gremlin

Neo4j让我特别满意的一点是支持SPARQL。这样RDF数据库的灵活性和图数据库的强大性都有了。AllegroGraph也可以同时做到这两点，就是商业版本贵点。

开始：忍受不了RDB僵硬的表结构=>使用键,值数据库；发现完全没有结构也不好=>使用文档数据库；发现文档结构其实也很讨厌，特别是没join => 使用图数据库；发现其实上述其实都是图，但很快就有越来越多复杂的路径查询=>把这些查询写死在代码里；能不能不写死呢 =>恭喜，您现在是语义网的程序员了

最近在看AffinityDB和Neo4j。这些都可以算W3C路线之外的语义网的实现方法。特别是AffinityDB，真是该有的全有了，该没有的全没有     
    