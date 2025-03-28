+++
date = '2025-03-27T22:11:14-04:00'
draft = true
title = 'Big Data Technologies: Lecture 2 - MapReduce and Data Processing'
+++


## Overview of mapreduce

Prerequisite:
- hadoop common: 3.3.0
- hadoop-mapreduce-client-core - 3.3.0

In hadoop block size : 128 MB by default

Mapper processes input data into small chunks.

What is longwritable and text?
- Hadoop works on distributed system and we travel data over network which needs `serialization`.
- For long we have `LongWritable` and Int we have `IntWritable` 
- Context object helps the mapper and reducer to interact with rest of hadoop system and it has interfaces which can help to emit output
- StringTokenizer helps to break the line words
- After writing map reduce code in driver class we will initialize a new map reduce `Job`
- 
**(K,V) -> Mapper -> (K,V) -> (K, List<V>) -> Reducer -> (K,V)**

[Return to Lecture 1: HDFS Fundamentals]({{< ref "lecture1.md" >}})