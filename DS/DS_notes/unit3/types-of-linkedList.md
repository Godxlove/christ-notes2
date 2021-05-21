#mynotes #linkedlist

# 4 types of linked lists
resource - [Jenny's lectures](https://www.youtube.com/watch?v=DWpVGpNfDmM)

1. Singly linked list
2. Doubly linked list
3. Circular linked list
4. Doubly circular linked list

---

### Singly linked list

```c
struct node
{
	int data;
	struct node *next;
};
```

### doubly linked list

```c
struct node
{
	int data;
	struct node *next;
	struct node *previous;
};
```

### circular linked list

The last node in the list points to the address of the first node in the linked list. It's a variation of singly linked list.

```c
struct node
{
	int data;
	struct node *next;
};
```

### doubly circular linked list

Combination of doubly and circular linked list.
The last node will have the \*next ptr address of the first node. The \*previous of the first node will have the address of the last node.

```c
struct node
{
	int data;
	struct node *next;
	struct node *previous;
};
```
