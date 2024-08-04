
# Hacker web crawler

## Design decisions
- consistent hashing
- save cralwed content on memory, then disk
- deduplicate using hash map

## Design deep dive
- How to detect a server is down? all-to-all multi casting/gossip protocol
- What to do when a server is down? Forward to the next servers
- What do do when a server is up?
- Data partitition/replication 2 copies
- How to de-duplicate?
- What if some servers are overloaded? virtual nodes
- How to minimize communication between servers? batch urls before assigning to other machines

