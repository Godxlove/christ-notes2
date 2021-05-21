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



