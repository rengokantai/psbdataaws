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
mkdir streamingCode
wget -O ./stramingCode/wordSplitter.py http://s3.amazonaws.com/elssticmapreduce/samples/wordcount/sordSplitter.py
hadoop jar contrib/streaming/hadoop-streaming.jar -files streamingCode/wordSplitter.py -mapper wordSplitter.py input s3://elasticmapreduce/samples/wordcount/input -output streamingCode/wordCount -reducer aggregate
```
```
hadoop fs -rm stramingCode/wordCountOut/*
hadoop fs -rmdir stramingCode/wordCountOut
rm streamingCode/*
rmdir streamingCode
```
