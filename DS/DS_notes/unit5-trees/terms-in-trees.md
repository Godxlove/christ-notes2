## Intro to trees
A tree is a **nonlinear** data structure, They organize data hierarchically.
It can be empty with no nodes. A tree consisting of one node called the **root**.

It has following general properties:
- One node is distinguished as a root;
- Every node (exclude a root) is connected by a directed edge

<br>

**definition:** A tree can be defined as a collection of nodes linked together to simulate a hierarchy.

<br>
A tree is used to represent data items which have hierarchically relations of data items.
It grows from top to bottom (**unidirectional**).

Some terminologies -
1. root - top most element; has no parent node.
2. nodes - store some info; can have int, char or strings.
3. parent - immediate predecessor to a node is the parent to that node.
4. child node - immediate successor of a node is the child node for that node.
5. leaf node (external nodes) - nodes having no child.
6. non-leaf node (internal nodes) - nodes having atleast one child
7. path - sequence of consecutive edges from source node to destination node.
8. edge - link between two nodes
9. ancestor - any predecessor node on the path from root to that node.
10. descendents - any successor node on the path from root to that node.
11. sub tree - it contains a node and all its descendents.
12. sibling - all children of same parent
13. degree of a node - the number of children of that node. *Degree of leaf nodes are zero.*
14. Depth of a node - length of a path from root to that node. (no. of edges from root to that node). Depth of root node is zero.
15. height of a node - no. of edges in the longest path from that node to leaf node.
16. level - height of a tree.

#### If a tree has *n* nodes, it has (n - 1) edges.

```c
// how a binary tree struct looks like
struct node
{
	int data;
	struct node *left;
	struct node *right;
}
```