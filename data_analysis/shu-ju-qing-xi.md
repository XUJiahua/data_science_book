# 数据清洗

缺失值处理（策略）：删除row，删除column，填充均值、众数

```text
dropna()
```



数据集按大小分，有小数据集、大数据集。大小的界定，一般以数据是否能在单机处理为硬边界。实际大小之分，可按照每个人自己对数据的理解。

#### Pandas（小数据集）

1. Pandas
2. Juypter Notebook
3. matplotlib/seaborn/plotly

#### Spark（大数据集，通用）

有如下特点：

1. 并行计算（多核，多机并行执行子任务，空间换时间）
2. 内存计算（相对于MapReduce而言）
3. 懒计算，懒加载，Lazy。（与之相对的是Eager模型，马上计算）
4. 容错（一个节点出错，调度器会将任务重新发配给新节点）。
5. SQL。比dataframe的API好记忆得多。
6. 兼容HDFS文件系统。

#### Pandas的扩展工具

1. pandas：是先驱，但是计算能力已经不够了。
2. Dask: pandas on multiple CPUs
3. cuDF\(RAPIDS\): pandas on GPU（门槛是NVIDIA显卡）
4. Dask\_cuDF: pandas on multiple GPUs

### 自助式数据处理工具

#### Paxata



#### bamboolib









