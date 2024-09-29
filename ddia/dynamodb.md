---
title: Dynamo DB Paper Explained
tags:
  - databases
  - nosql
  - dynamodb
---
### Why DynamoDB?

- In 2023, during 66 hour of prime day sales:
	- Trillions of calls to DynamoDB 
	- Peak 89.2 mil APS
	- High Availability with single digit millisecond performance!
- Almost all major services in Amazon use DDB along with external customers.

### Goals of DynamoDB Design:
- DynamoDB was conceptualised with this one goal in mind:
	- Provide consistent performance at any scale
	- i.e low single-digit millisecond latency for most cases less than 5 ms.

### Workload Pattern:
- Multi-tenant -> load of one customer should not affect another.
- High resource utilisation
- Boundless scale of tables.
- Predictable performance -> MB or TB.
- Highly Available -> Replication and Recovery.
- Flexible usecase support -> schemaless with basic enforcement to support large number of tables.

### Architecture:
- DynamoDB has multiple tables.
- Each table is a collection of items.
- Each item is uniquely identified by its 'primary key'.
- The primary key needs to be specified during the table creation:
	- Partition Key -> **Required.
	- Sort Key -> *Optional
	- these determine where and ho the data is stored.
- Due to the partition key, this clearly indicates that the data would be partitioned and stored across nodes.
	- item -> f(k) (partition key) -> partition1/ partition2 
- i.e multiple data partitions.
- Note that it is okay to not have a sort key. Here in this case partition key becomes the primary key.
- DynamoDB also supports secondary indexes scan -> to prevent us from doing a full table scan.
	- DynamoDB tables with 2 columns , one with an indexed value and also an primary key.
	- secondary indexes are present as tables with 2 columns(and other configurations are available).
	- Eg: index on age : 10 -> {1}, 10 -> {2}, 10 -> {91}
- DynamoDB table is divide into partitions:
	- Each partition is disjoint (no two partition would share the data),subset of the entire data and holds contiguous key-range (range functions).
	- Eg: partition1 {apple,banana,cat}, partition2{dog,elephant},partition3{fan,grapes,house}
	- Each partition has multiple replicas, distributed across multiple availability zones -> Highly Available. (for making it highly available, replicas the data into the multiple partitions.)
- Replicas of a partition for a "replication group"
	- one of them is a leader
	- others are pure replicas 
	- multi-paxos for consensus and  leader election.
- Any replicas can trigger the election.When a leader is elected, it can continue to extend its leadership lease. -> this is at the partition replica level , not at data node level.
	- when the leader is down, one of the other nodes will start the process of electing the leader.

- In terms of parition, the role of the leader is to manage the rights of the 