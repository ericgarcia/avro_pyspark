
To build this, you need to first check out the latest spark source https://github.com/apache/spark and run `sbt/sbt publish-local`. This will put spark in maven's local repository.

You will also want to build this version of spark with `./make-distribution.sh --tgz`

Then from this repository, run `mvn package` to create `avro-0.1.jar`.

To start up pyspark with with this library, run `SPARK_CLASSPATH=/tmp/avro-0.1.jar bin/pyspark` from the distribution you created above.

To load in an Avro file in pyspark use:

    avroRdd = sc.newAPIHadoopFile("/tmp/data.avro", 
      "org.apache.avro.mapreduce.AvroKeyInputFormat", 
      "org.apache.avro.mapred.AvroKey", 
      "org.apache.hadoop.io.NullWritable",
      keyConverter="example.AvroGenericConverter")
