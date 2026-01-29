Lab 5: Mini-MapReduce on Amazon EMR

Files:
mapper.py 
reducer.py

Download and Prepare Dataset:
wget https://github.com/LGDoor/Dump-of-Simple-English-Wiki/raw/refs/heads/master/corpus.tgz
tar -xvzf corpus.tgz

Setup HDFS directories:
hdfs dfs -mkdir -p /user/hadoop/input
hdfs dfs -put corpus.txt /user/hadoop/input/

Upload to HDFS
hdfs dfs -put corpus.txt /user/hadoop/input/

Basic Execution:
ssh -i your-key.pem hadoop@<master-public-dns>

Run MapReduce job:
hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar \
  -input /user/hadoop/input/corpus.txt \
  -output /user/hadoop/output/wordcount \
  -mapper mapper.py \
  -reducer reducer.py \
  -file mapper.py \
  -file reducer.py

Check Results:
hdfs dfs -ls /user/hadoop/output/wordcount-output/
hdfs dfs -cat /user/hadoop/output/wordcount-output/part-* | head -50
