# Tree Specification
This document specifies the structure of the wasmchain Tree.
The Tree has features of [PPSP](https://tools.ietf.org/html/rfc7574#section-5.1) and [Merkle Mountain Ranges](https://github.com/mimblewimble/grin/blob/master/doc/mmr.md). The Tree differs from Ethereum's tree in that it does not store key/value entries. Instead, it only stores data at given integer indices.

## The Tree Structure
The Tree is a binary tree where all leaf nodes have a uniform depth. For example:
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
Addresses are generated serially, and hence the Tree indices represent the order of address creation. </br>
As a result of this property, all nodes with an even index are LEAF nodes. </br>
Another benefit of sequential address generation is its inherent amenability to serialization in an append-only flat file format. </br> 
The numbers represent the order in which all the nodes where created, and the even nodes are the leaf nodes.

## Tree Nodes
There are three types of nodes: ROOT, BRANCH, and LEAF. 

```
NODE := ROOT
      | BRANCH
      | LEAF
```

### ROOT
A Tree has at most one ROOT node. The root node contains two elements: an "EDGE" and METADATA.

```
ROOT := (EDGE, METADATA)
```

For now, "METADATA" just contains a single element, the tree's "HEIGHT" which is encoded as an LEB128 unsigned integer.

### BRANCH
Each branch node contains two "EDGE" elements: "left EDGE", "right EDGE".

```
BRANCH := (EDGE, EDGE)
```

### LEAF
The leaf node contains arbitary data pointed to by an EDGE.


## EDGE
The EDGE elements point to the next node in the tree using a merkle link.
A merkle link is defined by the first 20 bytes of the result SHA-256 of an encoded node.


```
EDGE := SHA2(encoded_node)[0..20]
```
