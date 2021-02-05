---
layout:     post
title:      "Notebook: Apache Spark thoughts"
subtitle:   " \"\""
date:       2021-02-01 16:00:00
author:     "Ping"
header-img: "img/in-post/spark/spark.jpg"
catalog: true
tags:
    - Spark
    - Notebook
---

> This is a notebook of some thoughts when I played with Spark, thought this might be a good way to share.

### GroupByKey VS ReduceByKey VS AggregateByKey VS CombineByKey

* GroupByKey: group the dataset based on keys, resulting shuffling and thus heavy network communication. (__Try to avoid__)

* ReduceByKey: datasets are combined on each partition, ONLY one output per key on each partition is sent over network. (__shuffling less than GroupByKey__, use instead of AggregateByKey when input and output are same type.)

* CombineByKey: similar to AggregateByKey, it asks for 3 parameters(functions),  __createCombiner__, __mergeValue__, __mergeCombiners__, with the exception that the 1st parameters is a function to create the initial value for the accumulator on the key. The process works as follows: the CombineByKey goes through every element in a partition, if the key has not seen before, it calls the __createCombiner__ to create the initial value for the accumulator for that key, otherwise if the key has been seen before, it calls __mergeValue__ instead, with the current value for the accumulator and the new value.Once above work finished on all partitions independently, the __mergeCombiner__ merges the results from each partition, when two or more partitions have an accumulator for the same key, then they are merged.

* AggregateByKey: combined elements are of different type than the returned type. It requires an initial value as an accumulator, a sequential function to be performed in every partition, a combiner operation to be performed across different partitions. (Use when aggregation + input & output RDDs have different types)

### Partitioning
The core idea is to spread the data evenly across all partitions.
* Hash partitioning
For pair RDD:   
val purchase = purchaseRdd.map(p => (p.customerId, p.price)).groupByKey()

The partition p is calculated:   
p = k.hashcode() % nrPartitions


* Range partitioning
For RDDs which have an ordering keys defined, range partitioning might be more efficient to use.

Actually some functions use the RangePartitioner under the hood, for example, `sortByKey()`, check Spark source code below:

```scala
def sortByKey(ascending: Boolean = true, numPartitions: Int = self.partitions.length)
    : RDD[(K, V)] = self.withScope
{
val part = new RangePartitioner(numPartitions, self, ascending)
new ShuffledRDD[K, V, V](self, part)
    .setKeyOrdering(if (ascending) ordering else ordering.reverse)
}
```

>> Partitioned RDDs or Dataframes should be persisted, otherwise the repartitioning is repeatedly applied each time the partitioned RDDs or dataframes is used.

