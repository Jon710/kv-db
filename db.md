This is a simple disk-based key-value database.
Pages are the smallest unit of data exchanged by a db and the disk. Related data is put in proximity so it can be fetched all at once. (PG has a default page size of 8kb)
DB pages are stored contiguously on the disk to minimize disk seeks.
DBs use different data structures to organize pages on the disk. This uses B-Tree since it's easier to implement.

Flow: Database -> Data Access Layer -> SSD/HDD

Database runs our program and is responsible for orchestrating transactions. It faces the programmers using it and serves their requests.
DAL handles disk operations and how data is organized on the disk. It manages underlying data structure, writes pages to disk and reclaims free pages to avoid fragmentation.

- Database must be persisted to the disk. This means it can restore its previous state between restarts. It also supports reading and writing pages to the disk. (dal, freelist...)
- How do we organize data? Database must take care of the bookkeeping of data: in other words, when fetching an item from the database, we must remember where it was inserted. (BST)
BST: data structure used for storing data in an ordered way. Each node in the tree is identified by a key, a value associated with this key, and two pointers (hence the name binary) for the child nodes. The invariant states that the left child node must be less than its direct parent, and the right child node must be greater than its immediate parent.
BST offers slower writing in favor of better reading if we compare it to an append-only data structure. It's ideal for general-use dbs.
Another consideration is disk access. It is costly, so it has to be kept to a minimum when designing a data structure that resides on the disk. 
B-Tree addresses this: it's a generalization of a binary search tree, allowing for nodes with more than two children. By having more children in each node, the tree’s height gets smaller, thus requiring fewer disk accesses.

reference: https://betterprogramming.pub/build-a-nosql-database-from-the-scratch-in-1000-lines-of-code-8ed1c15ed924