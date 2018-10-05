### 初始 Hadoop

​	许多处理模式能与 Hadoop 协同工作，如：

- **Interactive SQL （交互式 SQL）**

  利用 MapReduce 进行分发并使用一个分布式查询引擎，使得在 Hadoop 上获得 SQL 查询低延迟响应的同时还能保持对大数据集规模的可扩展性。

- **Iterative processing （迭代处理）**

  许多算法自身具有迭代性，因此和那种每次迭代都从硬盘加载的方式相比，这种在内存中保存每次中间结果集的方式更加高效。 MapReduce 的架构不允许这样，但如果使用 Spark 就会比较直接，它在使用数据集方面展现了一种高度探究的风格。

- **Stream processing（流处理）**

  流系统，例如 Storm， Spark Streaming 或 Samza 使得在无边界数据流上运行实时，分布式的计算，并向 Hadoop 存储系统或外部系统发布结果成为可能。

- **Search（搜索）**

  Solr 搜索平台能够在 Hadoop 集群上运行，当文档加入 HDFS 后就可以对其进行索引，并且根据 HDFS 中存储的索引为搜索查询提供服务。