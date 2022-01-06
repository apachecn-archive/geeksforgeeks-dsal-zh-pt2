# 以 n 元树形式排列的资源的锁定和解锁

> 原文:[https://www . geesforgeks . org/n 元树形式的资源锁定和解锁/](https://www.geeksforgeeks.org/locking-and-unlocking-of-resources-in-the-form-of-n-ary-tree/)

给定一个分层排列的 N 元资源树，树的高度为 0(对数 N)，其中 N 是节点(或资源)的总数。进程需要锁定资源节点才能使用它。但是，如果节点的任何后代或祖先被锁定，该节点就不能被锁定。
给定资源节点需要以下操作:

*   islock()-如果给定节点被锁定，则返回 true 如果没有被锁定，则返回 false。如果对节点成功执行了 lock()，则该节点被锁定。
*   Lock()-如果可能，锁定给定的节点并更新锁定信息。只有当前节点的祖先和后代没有被锁定，才有可能被锁定。
*   unLock()-解锁节点并更新信息。

如何设计资源节点并实现上述操作，从而实现以下时间复杂性。

```
    islock()  O(1)
    Lock()    O(log N)
    unLock()  O(log N)
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
假设资源需要以 n 元树的形式存储。现在的问题是，如何扩充树以达到上述复杂性界限。

**一些一般性问题:**

Q1。为什么单单设置 Lock = true 不能解决问题？
A1。因为对于我们移向父节点来检查锁定是否可能的方法，如果请求来自锁定节点和根节点之间的任何节点，那么就无法判断后代节点是否被锁定。因此，像 isLockable 这样的变量被用来维护这些信息。

Q2。为什么不锁定从当前节点到根的所有节点？
A2。因为锁定通常是资源密集型操作，对所有节点执行锁定直到根节点都是资源浪费。因此，使用了轻量级解决方案，如引入一个可隔离变量。

**方法 1(简单)**
一个简单的解决方案是将一个布尔变量**与每个资源节点存储在一起**。如果当前节点被锁定，布尔变量 isLocked 为真，否则为假。
让我们看看如何使用这种方法操作。

*   isLock():检查给定节点的**isLock**。
*   Lock():如果设置了**是锁定的**，则节点不能被锁定。否则检查该节点的所有后代和祖先，如果其中任何一个被锁定，则该节点也不能被锁定。如果以上条件都不成立，则通过将**设置为真来锁定该节点。**
*   unLock():如果给定节点的**被锁定**为假，则不做任何事情。否则设置**为假锁定**。

时间复杂性:

```
isLock()  O(1) 
Lock()    O(N)
unLock()  O(1)

Lock is O(N) because there can be O(N) descendants. 
```

**方法 2(根据问题的时间复杂性)**
想法是用以下三个字段扩充树:

1.  一个布尔字段**被锁定**(与上述方法相同)。
2.  **父指针**在 O(Log n)时间内访问所有祖先。
3.  **锁定后代的计数**。请注意，一个节点可以是许多后代的祖先。我们可以使用这个计数来检查是否有任何后代被锁定。

让我们看看如何使用这种方法操作。

*   isLock():检查给定节点的**isLock**。
*   Lock():遍历所有祖先。如果没有祖先被锁定，**锁定后代计数**为 0，**锁定**为假，则将当前节点的**锁定**设置为真。并为所有祖先增加**锁定后代计数**。时间复杂度为 0(对数 N)，因为最多可以有 0(对数 N)个祖先。
*   unLock():遍历所有祖先，减少所有祖先的**锁定后代计数**。将当前节点的**锁定**设置为假。时间复杂度为 0(对数 N)

感谢乌卡什·特里维迪提出这种方法。

**方法 3(根据问题的时间复杂性和更好的内存使用)想法是用以下三个字段扩充树:**

1.  布尔字段被锁定(与上述方法相同)。
2.  父指针，用于在 O(Log n)时间内访问所有祖先。
3.  可锁定。我们可以使用这个变量检查是否有任何后代被锁定。如果没有后代被锁定，则 isLockable 为真，否则为假。

让我们看看如何使用这种方法操作。

*   isLock():检查给定节点的 isLock。
*   Lock():遍历所有祖先。如果没有祖先被锁定，则 isLockable 为真，is locked 为假，将当前节点的 isLocked 设置为真。并为所有祖先标记一个可锁定的 false。时间复杂度为 0(对数 N)，因为最多可以有 0(对数 N)个祖先。
*   unLock():遍历所有祖先，并将所有祖先的 isLockable 标记为 true。将当前节点的 isLocked 设置为 false。时间复杂度为 0(对数 N)

## C++

```
#include <bits/stdc++.h>
using namespace std;

class narytree {
public:
    bool isLock;
    bool isLockable;
    narytree* parent;
    vector<narytree*> children;
    narytree()
    {
        isLock = false;
        isLockable = true;
        parent = NULL;
    }
    narytree(narytree* parent)
    {
        isLock = false;
        isLockable = true;
        this->parent = parent;
    }
};

bool isLock(narytree* node) { return node->isLock; }

void Lock(narytree* node)
{
    if (node->isLockable == false)
        return;

    narytree* T = node;
    bool flag = false;
    while (T != NULL) {
        if (T->isLock == true) {
            flag = true;
            break;
        }
        T = T->parent;
    }
    if (flag)
        return;
    else {
        node->isLock = true;
        T = node;
        // marking isLockable as false for ancestor nodes.
        while (T != NULL) {
            T->isLockable = false;
            T = T->parent;
        }
    }
}

void unLock(narytree* node)
{
    if (node->isLock == false)
        return;
    narytree* T = node;
    node->isLock = false;
    // marking isLoackable as true for ancestor nodes.
    while (T != NULL) {
        T->isLockable = true;
        T = T->parent;
    }
}

int main()
{
    // Creating N-Array Tree
    narytree* root = new narytree();

    narytree* t1 = new narytree(root);
    narytree* t2 = new narytree(root);
    narytree* t3 = new narytree(root);

    root->children.push_back(t1);
    root->children.push_back(t2);
    root->children.push_back(t3);

    narytree* t5 = new narytree(root->children[0]);
    root->children[0]->children.push_back(t5);
    narytree* t4 = new narytree(root->children[1]);
    root->children[1]->children.push_back(t4);

    // Locking t4 node.
    Lock(t4);
    //    Checking if the t4 node is locked.
    cout << "t4 node is locked:"
         << ((isLock(t4) == true) ? "true" : "false")
         << "\n";
    Lock(t2);
    cout << "t2 node is locked:"
         << ((isLock(t2) == true) ? "true" : "false")
         << "\n";
    // Unlocking t4 node.
    unLock(t4);
    //    Now we should be able to lock the tree.
    Lock(t2);
    cout << "t2 node is locked:"
         << ((isLock(t2) == true) ? "true" : "false");

    return 0;
}
```

感谢阿达什·辛格提出这种方法。

本文由**阿沛·拉提**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。