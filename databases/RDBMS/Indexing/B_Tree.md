# B-Tree in DBMS

## Introduction
Indexing is the first thing that comes to mind when we consider a database's performance. In this article, we'll learn about B-trees and how database indexing using B-tree in DBMS can improve the databases' performance.

## What is a B-Tree?

**Definition**: A B-tree is an m-way tree that self-balances itself.

**Use**: Due to their balanced structure, such trees are frequently used to manage and organize enormous databases and facilitate searches.

**Properties**: In a B-tree, each node can have a maximum of m child nodes. Leaf nodes and internal nodes will both have record references. B-Tree is called a Balanced stored tree as all the leaf nodes are at the same levels.

## What is an m-way Tree?
The m-way search trees are multi-way trees which are generalised versions of binary trees where each node contains multiple elements. In m-way tree each node can have at most m-1 elements and m children.

The value of m determines the branching factor ( or order ) of the tree, influencing its height and the number of keys that each node can contain.

In the context of B-trees, this multi-way structure helps in maintaining balance, optimizing search operations, and ensuring that the tree remains short and wide, thus reducing the overall height and improving access times.


## What is Self-Balancing in B-Tree and How Does it Work?
### What Does Self-Balancing Mean?
Self-balancing in the context of B-trees means that the tree maintains its balance automatically during insertions and deletions. This ensures that the tree's height remains logarithmic relative to the number of elements, which guarantees efficient operations like search, insert, and delete.

### How Does Self-Balancing Work?
1. **Insertion**:
    - When a new key is inserted into the B-tree, it is always added to a leaf node. If the leaf node has fewer than m-1 keys, the key is simply inserted into the correct position to maintain sorted order.
    - If the leaf node already has m-1 keys, it splits into two nodes, and the middle key is moved up to the parent node. This process may propagate up the tree if necessary.

2. **Deletion**:
    - When a key is deleted from a B-tree, the tree ensures that the minimum number of keys per node is maintained. If a node falls below the minimum number of keys, it borrows a key from a sibling node or merges with a sibling node to maintain balance.
    - The deletion operation ensures that the tree remains balanced by redistributing or merging nodes as needed.

### Benefits of Self-Balancing
- **Efficient Searches**: Maintains a low tree height, ensuring that search operations can be performed in O(log n) time.
- **Consistent Performance**: Avoids the degradation of performance that can occur with unbalanced trees.
- **Optimized Disk Access**: Minimizes the number of disk accesses required for operations, which is crucial for large databases stored on disk.

By maintaining a balanced structure, B-trees ensure that the tree height grows logarithmically with the number of elements, providing efficient and predictable performance for database operations.


## B-trees vs BST
B-trees and BSTs have the same average Big-O complexity, but a BST’s worst case complexity for search, insert, and update is O(n)) versus B-tree’s O(log(n)).

## Properties of B-Tree
Following are some of the properties of B-tree in DBMS:
- A non-leaf node's number of keys is one less than the number of its children.
- The number of keys in the root ranges from one to (m-1) maximum. Therefore, the root has a minimum of two and a maximum of m children.
- The keys range from min([m/2]-1) to max(m-1) for all nodes (non-leaf nodes) besides the root. Thus, they can have between m and [m/2] children.
- The level of each leaf node is the same.

## Why B-Trees are Needed?
- For having optimized searching, we cannot increase a tree's height. Therefore, we want the tree to be as short as possible in height.
- B-tree in DBMS has more branches and hence shorter height, which decreases access time.
- The cost of accessing the disc is high when searching tables, so minimizing disc access is our goal.
- To decrease time and cost, B-trees are used for storing data as it makes the index fast.

## How Database B-Tree Indexing Works
When B-tree is used for database indexing, it becomes a little more complex because it has both a key and a value. The value serves as a reference to the particular data record. A payload is the collective term for the key and value.

For indexing data to a particular key and value, the database first constructs a unique random index or a primary key for each of the supplied records. The keys and record byte streams are then all stored on a B+ tree. The random index that is generated is used for indexing the data.

### Advantages
- This indexing helps to decrease the searching time of data.
- In a B-tree, all the data is stored on the leaf nodes, now for accessing a particular data index, the database can make use of binary search on the leaf nodes as the data is stored in sorted order.
- If indexing is not used, the database reads each and every record to locate the requested record, increasing time and cost for searching the records, so B-tree indexing is very efficient.

## How Searching Happens in an Indexed Database?
The database does a search in the B-tree for a given key and returns the index in O(log(n)) time. The record is then obtained by running a second B+tree search in O(log(n)) time using the discovered index. So overall approx time taken for searching a record in a B-tree in DBMS-indexed databases is O(log(n)).

## Example of B-Tree
Suppose there are some numbers that need to be stored in a database, so if we store them in a B-tree in DBMS, they will be stored in a sorted order so that the searching time can be logarithmic.

![](https://scaler.com/topics/images/b-tree-example.webp)

### B-Tree Example
The above data is stored in sorted order according to the values. If we want to search for the node containing the value 48, the following steps will be applied:
1. First, the parent node with a key having data 100 is checked, as 48 is less than 100, so the left children node of 100 is checked.
2. In left children, there are 3 keys, so it will check from the leftmost key as the data is stored in sorted order.
3. The leftmost element is having key value as 48 which matches the element to be searched, that we wanted to search.

## Conclusion
- An m-way tree that self-balances itself is called a “B-tree”.
- Due to their balanced structure, such trees are frequently used to manage and organize enormous databases and facilitate searches.
- B-tree is an example of multilevel indexing.
- Use of B-tree is needed for storing data as searching and accessing time is decreased.
- B-trees can be used for database indexing to improve searching and storing time of database.
- While using B-tree, the database can make use of binary search on the leaf nodes as the data is stored in sorted order.

## What's Next?
### Related Topics
- B+ Tree in Data Structure
- AVL Trees
- Red-Black Trees

### Topics for Deeper Understanding
- Detailed implementation of B-Tree in various programming languages.
- Advanced operations on B-Trees (Insertion, Deletion, Merging).
- Comparison between B-Tree and B+ Tree.
- Real-world applications and performance analysis of B-Trees in DBMS.

# Resources

https://www.scaler.com/topics/data-structures/b-tree-in-data-structure/

https://www.geeksforgeeks.org/introduction-of-b-tree-2/?ref=lbp