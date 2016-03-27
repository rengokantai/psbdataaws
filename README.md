#### psbdataaws
#####Dynamodb
######concepts
Table contains primary key,(range key value is optional)  
Local secondry indexes(LSI): primary + secondary attributes  
Query with hash key value + second key value - secondary key value acts as an alternative range key  
  
Global secondary index(GSI) can query with secondary value alone.

######lab
create table first:  
Hash: OrderId  
sort: Linenumber  
Then create a index:  
Hash: CustomerId  
Sort: OrderId   
  
include attribute: Item Amount  
  
insert data:(Orderid andLinenumberId cannot be same)
```
{
  "OrderId": "1",
  "LineNumber": "1",
  "CustomerId": "1",
  "Item": "k",
  "Quantity": 11,
  "Amount": 22
}
```
```
{
  "OrderId": "1",
  "LineNumber": "2",
  "CustomerId": "1",
  "Item": "w",
  "Quantity": 11,
  "Amount": 22
}
```
```
{
  "OrderId": "1",
  "LineNumber": "3",
  "CustomerId": "1",
  "Item": "w",
  "Quantity": 11,
  "Amount": 22
}
```

Then
```
{
  "OrderId": "2",
  "LineNumber": "1",
  "CustomerId": "4",
  "Item": "ke",
  "Amount": 223
}
```
```
{
  "OrderId": "3",
  "LineNumber": "1",
  "CustomerId": "1",
  "Item": "q"
}
```
#####EMR
######Demo:Running streaming mapreduce
```
wget hadoop-streaming.jar http://central.maven.org/maven2/org/apache/hadoop/hadoop-streaming/2.6.0/hadoop-streaming-2.6.0.jar
mkdir streamingCode
wget -O ./streamingCode/wordSplitter.py http://s3.amazonaws.com/elasticmapreduce/samples/wordcount/wordSplitter.py
hadoop jar hadoop-streaming.jar -files streamingCode/wordSplitter.py -mapper wordSplitter.py -input s3://elasticmapreduce/samples/wordcount/input -output streamingCode/wordCountOut -reducer aggregate
```
//I still dont know how to use local path
```
hadoop fs -cat hdfs://ip-172.ec2.internal:8020/user/root/streamingCodeOut/*
hadoop fs -rm hdfs://ip-172.ec2.internal:8020/user/root/streamingCodeOut/*
hadoop fs -rmdir hdfs://ip-172.ec2.internal:8020/user/root/streamingCodeOut/*
rm streamingCode/*
rmdir streamingCode
```
#####Redshift
```
CREATE table data(...)
COPY data FROM 'dynamodb://xx' WITH CREDENTIALS AS 'aws_access_key_id=...;aws_secret_access_key= ' READRATIO 50
```

#####Data plpeline
######Troubleshooting the pipeline
```
select * from stl_load_errors order by starttime desc;
```
