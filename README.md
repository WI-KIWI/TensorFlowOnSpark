<!--
Copyright 2017 Yahoo Inc.
Licensed under the terms of the Apache 2.0 license.
Please see LICENSE file in the project root for terms.
-->
# TensorFlowOnSpark

## What's TensorFlowOnSpark?

TensorFlowOnSpark brings scalable deep learning to [Apache Hadoop](http://hadoop.apache.org) and [Apache Spark](http://spark.apache.org)
clusters. By combining salient features from deep learning framework
[TensorFlow](https://www.tensorflow.org) and big-data frameworks
Apache Spark and Apache Hadoop, TensorFlowOnSpark enables distributed
deep learning on a cluster of GPU and CPU servers.

TensorFlowOnSpark enables distributed TensorFlow training and
inference on Apache Spark clusters.  It seeks to minimize the amount
of code changes required to run existing TensorFlow programs on a
shared grid.  Its Spark-compatible API helps manage the TensorFlow
cluster with the following steps:

1. **Startup** - launches the Tensorflow main function on the executors, along with listeners for data/control messages.
1. **Data ingestion**
   - **Readers & QueueRunners** - leverages TensorFlow's [Reader](https://www.tensorflow.org/how_tos/reading_data/#reading_from_files) mechanism to read data files directly from HDFS.
   - **Feeding** - sends Spark RDD data into the TensorFlow nodes using the [feed_dict](https://www.tensorflow.org/how_tos/reading_data/#feeding) mechanism.  Note that we leverage the [Hadoop Input/Output Format](https://github.com/tensorflow/ecosystem/tree/master/hadoop) for access to TFRecords on HDFS.
1. **Shutdown** - shuts down the Tensorflow workers and PS nodes on the executors.

TensorFlowOnSpark was developed by Yahoo for large-scale distributed
deep learning on our Hadoop clusters in Yahoo's private cloud. 


## Why TensorFlowOnSpark?

TensorFlowOnSpark provides some important benefits (see [our
blog](http://yahoohadoop.tumblr.com/post/157196317141/open-sourcing-tensorflowonspark-distributed-deep))
over alternative deep learning solutions.
   * Easily migrate all existing TensorFlow programs with <10 lines of code change;
   * Support all TensorFlow functionalities: synchronous/asynchronous training, model/data parallelism, inferencing and TensorBoard;
   * Server-to-server direct communication achieves faster learning when available;
   * Allow datasets on HDFS and other sources pushed by Spark or pulled by TensorFlow; 
   * Easily integrate with your existing data processing pipelines and machine learning algorithms (ex. MLlib, CaffeOnSpark);
   * Easily deployed on cloud or on-premise: CPU & GPU, Ethernet and Infiniband. 


## Using TensorFlowOnSpark

Please check TensorFlowOnSpark [wiki site](https://github.com/yahoo/TensorFlowOnSpark/wiki) for detailed
documentations such as getting started guides for [YARN
cluster](https://github.com/yahoo/TensorFlowOnSpark/wiki/GetStarted_YARN) and [AWS EC2
cluster](https://github.com/yahoo/TensorFlowOnSpark/wiki/GetStarted_EC2). A [Conversion
Guide](https://github.com/yahoo/TensorFlowOnSpark/wiki/Conversion) has been provided to help you convert
your TensorFlow programs.

## Mailing List

Please join [TensorFlowOnSpark user group](https://groups.google.com/forum/#!forum/TensorFlowOnSpark-users) for discussions and questions.

## License

The use and distribution terms for this software are covered by the Apache 2.0 license.
See [LICENSE](LICENSE) file for terms.

## Modification for the original repo

As you noticed, I slightly hacked the original TensorFlowOnSpark code and generate two new directories [tensorflowonspark_gpu10p](https://github.com/WI-KIWI/TensorFlowOnSpark/tree/master/tensorflowonspark_gpu10p) and [tensorflowonspark_gpu20p](https://github.com/WI-KIWI/TensorFlowOnSpark/tree/master/tensorflowonspark_gpu20p). This makes the sharing of only one physical GPU possible in a Hadoop cluster, otherwise GPU memory will be occupied by one excuetor. Here, 10p means 10% and 20p means 20%, which infers each container only reserves 10% or 20% GPU memory.

