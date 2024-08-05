# System design for top k heavy hitters

## Design points
### Design
1. Counter + Min Heap

- How to scale? Replica, snapshot to blob storage

2. Count Min Sketch + Min Heap
3. File Storage and Map Reduce Job

### Design deep dive
Given the significant volume of events, further optimisations include
1. Performing aggregation of events at the API gateway level before forwarding them to the Kafka queue.
2. Using a Data Partitioner to read batches of events from Kafka and partition them into individual events. The partitioner will use a key derived from the event and time window to hash the events into different partitions. These partitioned events will then be sent to another Kafka queue. A Partition Processor will handle all events and write them in the same order.


