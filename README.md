# What are the uses of counters

• Hadoop MapReduce Counter provides a way to measure the progress or the number of
operations that occur within MapReduce programs.
• Basically, MapReduce framework provides a number of built-in counters to measure basic
I/O operations, such as FILE_BYTES_READ/WRITTEN and Map/Combine/Reduce
input/output records.
• These counters are very useful especially when you evaluate some MapReduce programs.
• Besides, the MapReduce Counter allows users to employ your own counters.
• Since MapReduce Counters are automatically aggregated over Map and Reduce phases, it
is one of the easiest way to investigate internal behaviors of MapReduce programs.
• To create user defined counter and increment it, use:
context.getCounter(<counter_group>, <counter_name>).increment(<value>);


# MR Unit testing is based on 

MapReduceDriver class:
• Harness that allows you to test a Mapper and a Reducer instance together (along with an
optional combiner).
• You provide the input key and value that should be sent to the Mapper, and outputs you
expect to be sent by the Reducer to the collector for those inputs.
• By calling runTest(), the harness will deliver the input to the Mapper, feed the
intermediate results to the Reducer (without checking them), and will check the
Reducer's outputs against the expected results.
• This is designed to handle the (k, v)* -> (k, v)* case from the Mapper/Reducer pair,
representing a single unit test.
• If a combiner is specified, then it will be run exactly once after the Mapper and before
the Reducer.

# How testing is useful in industry

- The main purpose of software Quality Assurance is to make sure that all the processes are being followed throughout all the development phases. QA is very important and useful to deliver the quality project to customer. QA is the backbone of product.
- In other words, we can say that QA is the gate keeper which give the sign off to the customer to deploy the final build of production on production environment.


# Mapreduce Task Counters,File system counters,Job Counter
 Mapreduce Task Counters:
Task counters gather information about tasks over the course of their execution, and the results are aggregated over all the tasks in a job. For example, the MAP_INPUT_RECORDS counter counts the input records read by each map task and aggregates over all map tasks in a job, so that the final figure is the total number of input records for the whole job. Etc

File system counters:
File system countres track 2 main details , number of bytes read by the file system and number of bytes written.

Job Counter:
Job counters are maintained by the jobtracker (or application master in
YARN), so they don’t need to be sent across the network, unlike all other counters, including user-defined ones. They measure job-level statistics, not values that change while a task is running. For example, TOTAL_LAUNCHED_MAPS counts the number of map tasks that were launched over the course of a job (including ones that failed).

# Raw comparator VS Writable Comparator:
WritableComparator
• A Comparator for WritableComparable
setSortComparatorClass(Class<? extends RawComparator> cls)
• Define the comparator that controls how the keys are sorted before they are passed to
the Reducer.
setGroupingComparatorClass(Class<? extends RawComparator> cls)
• Define the comparator that controls which keys are grouped together for a single call to
Reducer.reduce(Object, Iterable, org.apache.hadoop.mapreduce.Reducer.Context)

# Partitioner, Sort comparator, Group comparator
Partitioner-
Partitioner controls the partitioning of the keys of the intermediate map-outputs. The key (or a subset of the key) is used to derive the partition, typically by a hash function. The total number of partitions is the same as the number of reduce tasks for the job. Hence this controls which of the m reduce tasks the intermediate key (and hence the record) is sent for reduction.
Sort comparator-
SortComparator decides how map output keys are sorted.
Group comparator-
GroupComparator decides which map output keys within the Reducer go to the same reduce method call.
