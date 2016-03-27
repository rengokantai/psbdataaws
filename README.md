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
