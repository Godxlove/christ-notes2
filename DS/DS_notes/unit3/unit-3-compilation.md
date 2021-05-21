# index of linked list chapter

| Name | notes |
| :---:| :----:|
| Intro |[intro-to-linkedList](intro-to-linkedList.md) |
| Handling errors while debugging | [handling-error](handling-error.md) |
| Ma'am's starting out coding of LL | [linkedList-codes](linkedList-codes.md) |


Types of LL [types-of-linkedList](types-of-linkedList.md) #mynotes 

---

## Intro

![](linkedList_intro.png)
![](linkedList_vs_array.png)

<br>

![](linkedList_vs_array_pic.png)
Check this out too in Jenny's [lectures](https://www.youtube.com/watch?v=qauEA64G1Ds) -> makes notes on it.

<br>

![](nodes_visualise.png)

---

## how compiler behaves when error happens

![](error_for_line_20.png)

here, a semicolon is missing in line 19.
But the compiler error is in line 20.

#### What to learn from this
- Dont go finding for the error after line 20 only.
- atleast check for errors in the 10 lines before the stated line having the error. 

---

#linkedlist 

![](linked_list_program.png)

```c
#include <stdio.h>

struct NODE
{
	int data;
	struct NODE *next;
};

int main()
{
	struct NODE *head, *first, *i;
	head = (struct NODE *)malloc(sizeof(struct NODE));  // size of the data type used
	// malloc needs a return type

	head->data = 10;
	head->next = NULL;

	printf("%d\n", head->data);


	first = (struct NODE *)malloc(sizeof(struct NODE));  // size of the data type used
	// malloc needs a return type

	first->data = 20;
	first->next = NULL;  // very important, if not there then loop runs infinitely.

	head->next = first;

	for(i = head; i != NULL; i = i->next)
	{
		printf("->%d\t", i->data);
	}
}
	
	
output: 
- >10			- >20
}
```

---

modified the code with typedef ->
**name the structure accordingly with typedef too**

```c
#include <stdio.h>

typedef struct NODE node;
struct NODE
{
    int data;
    struct NODE *next;
};

int main()
{
    node *head, *first, *i;
    head = (struct NODE *)malloc(sizeof(struct NODE));  // size of the data type used
    // malloc needs a return type

    head->data = 10;
    head->next = NULL;

    printf("%d\n", head->data);


    first = (struct NODE *)malloc(sizeof(struct NODE));  // size of the data type used
    // malloc needs a return type

    first->data = 20;
    first->next = NULL;  // very important, if not there then loop runs infinitely.

    head->next = first;

    for(i = head; i != NULL; i = i->next)
    {
        printf("->%d\t", i->data);
    }
}
```

---

### new thing
function prototype declaration is known as forward declaration

---

#### Created a function

```c

#include <stdio.h>

typedef struct NODE node;
struct NODE
{
    int data;
    struct NODE *next;
};

node* createNode();

int main()
{
    node *head, *first, *i;
    //head = (struct NODE *)malloc(sizeof(struct NODE));  // size of the data type used
    // malloc needs a return type

    //head->data = 10;
    //head->next = NULL;

    head = createNode();
    
    printf("%d\n", head->data);


    first = (struct NODE *)malloc(sizeof(struct NODE));  // size of the data type used
    // malloc needs a return type

    first->data = 20;
    first->next = NULL;  // very important, if not there then loop runs infinitely.

    head->next = first;

    for(i = head; i != NULL; i = i->next)
    {
        printf("->%d\t", i->data);
    }
}


node* createNode()
{
    node *temp;
    temp = (node *)malloc(sizeof(node));

    printf("\nEnter the data: \n");
    scanf("%d", temp->data);
    temp->next=NULL;

    return temp;
}
```

---

how I did -

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct NODE node;
struct NODE
{
    int data;
    struct NODE *next;
};

node* createNode();

int main()
{
    node *head, *first, *i;

    first = (node *)malloc(sizeof(node));
    head = createNode();

    head->next = first;

    first->data = 98;
    first->next = NULL;

    for(i = head; i != NULL; i = i->next)
    {
        printf("->%d\t", i->data);
    }
}


node* createNode()
{
    node *temp;
    temp = (node *)malloc(sizeof(node));

    printf("\nEnter the data: \n");
    scanf("%d", &temp->data);
    temp->next=NULL;

    return temp;
}

```

![](my_code_output.png)

---

#pointstoremember

1. In a linked list (singly), binary search is not possible.
2. Traversal is in the order of O(n) time complexity as compared to O(1) in arrays since we have to traverse the whole list in order to reach the element we want to. So, traversal takes more time in LL than in arrays.
3. Insertion and deletion in a LL is faster and easier than deletion in arrays since we have to only deal with 3 nodes in the LL to update the nodes/ their position. While in the latter, we have to move the whole elements for the respective operations. 

---

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
