# Tree Specification
This document specifies the structure of the wasmchain merkle tree.
This tree includes features from [PPSP](https://tools.ietf.org/html/rfc7574#section-5.1) and [Merkle Mountain Ranges](https://github.com/mimblewimble/grin/blob/master/doc/mmr.md). The Merkle Tree differers from Ethereum merkle trie in that it does not store key/value entries. Instead it only stores data at given interger indexes.

## The Tree Structure
The Tree is a binary tree where all leaf nodes have a uniform depth. For Example
```
                                  7
                                 / \
                               /     \
                             /         \
                           /             \
                         3                11
                        / \              / \
                       /   \            /   \
                      /     \          /     \
                     1       5        9       13
                    / \     / \      / \      / \
                   0   2   4   6    8   10  12   14

```

The numbers repesent the order in which all the nodes where created, and the even nodes are the leaf nodes.

## Node
There are three types of nodes, The Root, Branches and Leafs

```
NODE := ROOT | BRANCH | LEAF
```

### ROOT
There is one root node per tree. The root node contains two elements: an "EDGE"  and METADATA

```
ROOT := EDGE, METADATA;
```

For now "METADATA" just contains a single element, the tree's "HEIGHT" which is encoded as an LEB128 unsigned integer

### BRANCH

Each branch node contains two "EDGE" elements: "left EDGE", "right EDGE".

```
BRANCH : = EDGE, EDGE;
```

### LEAF
The leaf node is an arbitary data pointed to by an EDGE.


## EDGE

The edge elements point to the next node in the tree using a merkle link.
A merkle link is defined by the first 20 bytes of the result SHA-256 of an encoded node.


```
EDGE := SHA2(encoded_node)[0..20]
```
