# 在 C 中使用双链表的员工管理系统

> 原文:[https://www . geesforgeks . org/employee-management-system-use-double-link-list-in-c/](https://www.geeksforgeeks.org/employee-management-system-using-doubly-linked-list-in-c/)

在 [C](https://www.geeksforgeeks.org/c-programming-language/) 中设计并实现[菜单驱动程序](https://www.geeksforgeeks.org/menu-driven-program-using-switch-case-c/)，对员工数据 DLL 进行如下操作，字段: **SSN** 、**姓名**、**部门**、**名称**、**工资**、**电话号码**:

*   使用结束插入创建 **N 员工的**数据的动态链接库。
*   显示 DLL 的状态，并统计其中的节点数。
*   在 DLL 的末尾执行插入和删除。
*   在 DLL 的前面执行插入和删除。
*   演示该 DLL 如何用作双端[队列](https://www.geeksforgeeks.org/queue-data-structure/)。

**进场:**

*   为了存储员工的数据，创建一个用户定义的数据类型来存储关于员工的信息。下面是数据类型的声明:

```
struct node {
    struct node* prev;
    int ssn;
    long int phno;
    float sal;
    char name[20], dept[10], desg[20];
    struct node* next;
}
```

*   **构建员工表:**构建员工表的想法是使用上面的**结构数据类型**，它将用于存储关于员工的信息，每个新员工的详细信息将作为**链接列表节点**添加。
*   **在记录中删除:**由于使用双链表存储数据，因此删除任何索引处的数据只需将被删除数据的下一个**链接到下一个**，并将被删除节点的**下一个数据**的**上一个节点**链接到其**上一个数据**。****
*   **在记录中搜索:**对于基于任何参数在记录中搜索，其思想是遍历数据，如果在任何索引处值参数与存储的记录匹配，则打印该员工的所有信息。

以下是使用[双向链表](https://www.geeksforgeeks.org/doubly-linked-list/)演示雇主详细信息的 C 程序:

## C

```
// C-program to demonstrate employer
// details using a Doubly-linked list
#include <conio.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Global declaration
int count = 0;

// Structure declaration
struct node {
    struct node* prev;
    int ssn;
    long int phno;
    float sal;
    char name[20], dept[10], desg[20];
    struct node* next;
} * h, *temp, *temp1, *temp2, *temp4;

// Function to create node
void create()
{
    int ssn;
    long int phno;
    float sal;
    char name[20], dept[10], desg[20];
    temp = (struct node*)malloc(sizeof(struct node));
    temp->prev = NULL;
    temp->next = NULL;
    printf("\n enter ssn, name, depart"
           "ment, designation, salary "
           "and phno of employee:\n");
    scanf("%d %s %s %s %f %ld",
          &ssn, name, dept, desg,
          &sal, &phno);
    temp->ssn = ssn;
    strcpy(temp->name, name);
    strcpy(temp->dept, dept);
    strcpy(temp->desg, desg);
    temp->sal = sal;
    temp->phno = phno;
    count++;
}

// Function to insert at beginning
void insertbeg()
{
    // If DLL is empty
    if (h == NULL) {
        create();
        h = temp;
        temp1 = h;
    }

    // Else create a new node and
    // update the links
    else {
        create();
        temp->next = h;
        h->prev = temp;
        h = temp;
    }
}

// Function to insert at end
void insertend()
{
    // If DLL is empty
    if (h == NULL) {
        create();
        h = temp;
        temp1 = h;
    }

    // Else create a new node and
    // update the links
    else {
        create();
        temp1->next = temp;
        temp->prev = temp1;
        temp1 = temp;
    }
}

// Function to display from beginning
void displaybeg()
{
    temp2 = h;
    if (temp2 == NULL) {
        printf("\n list is empty\n");
        return;
    }
    printf("\n linked list elements "
           "from beginning:\n");
    while (temp2 != NULL) {
        printf("%d %s %s %s %f %ld\n",
               temp2->ssn, temp2->name,
               temp2->dept, temp2->desg,
               temp2->sal, temp2->phno);
        temp2 = temp2->next;
    }

    // Print the count
    printf("number of employees=%d", count);
}

// Function to delete at end
int deleteend()
{
    struct node* temp;
    temp = h;
    if (temp == NULL) {
        printf("list is empty\n");
        return 0;
    }
    if (temp->next == NULL) {
        printf("%d %s %s %s %f %ld\n",
               temp->ssn, temp->name,
               temp->dept, temp->desg,
               temp->sal, temp->phno);
        free(temp);
        h = NULL;
    }
    else {
        temp = temp1;
        temp2 = temp1->prev;
        temp2->next = NULL;
        printf("%d %s %s %s %f %ld\n",
               temp->ssn, temp->name,
               temp->dept, temp->desg,
               temp->sal, temp->phno);
        free(temp);
        temp1 = temp2;
    }
    count--;
    return 0;
}

// Function to delete from beginning
int deletebeg()
{
    struct node* temp;
    temp = h;
    if (temp == NULL) {
        printf("list is empty\n");
        return 0;
    }
    if (temp->next == NULL) {
        printf("%d %s %s %s %f %ld\n",
               temp->ssn, temp->name,
               temp->dept, temp->desg,
               temp->sal, temp->phno);
        free(temp);
        h = NULL;
    }
    else {
        h = h->next;
        h->prev = NULL;
        printf("%d %s %s %s %f %ld\n",
               temp->ssn, temp->name,
               temp->dept, temp->desg,
               temp->sal, temp->phno);
        free(temp);
    }
    count--;
    return 0;
}

// Function displaying menus
void employerDetails()
{
    int ch, n, i;
    h = NULL;
    temp = temp1 = NULL;
    printf("--------Menu------------\n");
    printf("\n 1.create a DLL of n emp");
    printf("\n 2.display from beginning");
    printf("\n 3.insert at end");
    printf("\n 4.delete at end");
    printf("\n 5.insert at beginning");
    printf("\n 6.delete at beginning");
    printf("\n 7.to show DLL as queue");
    printf("\n 8.exit\n");
    printf("----------------------\n");
    while (1) {
        printf("\n enter choice : ");
        scanf("%d", &ch);

        // Switch statements begins
        switch (ch) {
        case 1:
            printf("\n enter number of"
                   " employees:");
            scanf("%d", &n);
            for (i = 0; i < n; i++)
                insertend();
            break;
        case 2:
            displaybeg();
            break;
        case 3:
            insertend();
            break;
        case 4:
            deleteend();
            break;
        case 5:
            insertbeg();
            break;
        case 6:
            deletebeg();
            break;
        case 7:
            printf(
                "\n to show DLL as queue"
                " \n1.perform insert and"
                " deletion operation by "
                "calling insertbeg() and "
                "deleteend() respectively\n "
                "\t OR \n 2.perform insert "
                "and delete operations by 
                "calling  insertend() and "
                "deletebeg() respectively\n");
            break;
        case 8:
            exit(0);
        default:
            printf("wrong choice\n");
        }
    }
}

// Driver Code
int main()
{
    // Function Call
    employerDetails();

    return 0;
}
```