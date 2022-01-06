# 单个资源预留的数据结构

> 原文:[https://www . geesforgeks . org/data-structure-for-future-reservations-for-single-resource/](https://www.geeksforgeeks.org/data-structure-for-future-reservations-for-a-single-resource/)

设计一个数据结构，在以下约束条件下，在单台机器上保留未来的作业。
1)每项工作都需要机器精确的 k 个时间单位。
2)机器一次只能做一项工作。
3)时间是系统的一部分。未来的工作会在不同的时间出现。只有当在 k 个时间范围内(在 T3 之前和之后)没有现有的预留时，才完成对未来作业的预留 4)每当作业完成时(或者其预留时间加上 k 等于当前时间)，它就从系统中移除。

示例:

```
Let time taken by a job (or k) be = 4

At time 0: Reservation request for a job at time 2 in 
           future comes in, reservation is done as machine 
           will be available (no conflicting reservations)
Reservations {2}

At time 3: Reservation requests at times 15, 7, 20 and 3.
           Job at 7, 15 and 20 can be reserved, but at 3 
           cannot be reserved as it conflicts with a 
           reserved at 2.
Reservations {2, 7, 15, 20}

At time 6: Reservation requests at times 30, 17, 35 and 45
           Jobs at 30, 35 and 45 are reserved, but at 17  
           cannot be reserved as it conflicts with a reserved 
           at 15.
Reservations {7, 15, 30, 35, 45}.
Note that job at 2 is removed as it must be finished by 6.

```

让我们为这个任务考虑不同的数据结构。

一种解决方案是将所有未来的预订按数组排序。检查冲突的时间复杂性可以使用[二分搜索法](http://geeksquiz.com/binary-search/)在 O(Logn)中完成，但是插入和删除需要 O(n)时间。

[哈希](http://geeksquiz.com/hashing-set-1-introduction/)不能在这里使用，因为搜索不是精确搜索，而是 k 时间范围内的搜索。

想法是使用[二叉查找树](http://geeksquiz.com/binary-search-tree-set-1-search-and-insertion/)来维护一组保留的作业。对于每个预订请求，仅在没有冲突预订时插入。插入作业时，进行“k 时间范围内检查”。如果从根插入路径上有 k 个远端节点，则拒绝预留请求，否则进行预留。

```
// A BST node to store future reservations
struct node
{
    int time; // reservation time
    struct node *left, *right;
};

// A utility function to create a new BST node
struct node *newNode(int item)
{
    struct node *temp =
        (struct node *)malloc(sizeof(struct node));
    temp->time = item;
    temp->left = temp->right = NULL;
    return temp;
}

/* BST insert to process a new reservation request at
   a given time (future time).  This function does
   reservation only if there is no existing job within
   k time frame of new job  */
struct node* insert(struct node* root, int time, int k)
{
    /* If the tree is empty, return a new node */
    if (root == NULL) return newNode(time);

    // Check if this job conflicts with existing
    // reservations
    if ((time-k < root->time) && (time+k > root->time))
        return root;

    /* Otherwise, recur down the tree */
    if (time < root->time)
        root->left  = insert(root->left, time, k);
    else
        root->right = insert(root->right, time, k);

    /* return the (unchanged) node pointer */
    return root;
}
```

作业的删除很简单 [BST 删除](http://geeksquiz.com/binary-search-tree-set-2-delete/)操作。

一个正常的 BST 需要 0(h)的时间进行插入和删除操作。我们可以使用像[AVL](https://www.geeksforgeeks.org/avl-tree-set-1-insertion/)[红黑](https://www.geeksforgeeks.org/red-black-tree-set-1-introduction-2/)这样的自平衡二分搜索法树，..在 O(Log n)时间内完成这两个操作。

这个问题是从[这个](http://courses.csail.mit.edu/6.006/fall09/lecture_notes/lecture03.pdf)麻省理工演讲中采纳的。

本文由**拉杰夫**供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论