# LS3/NS3 球体生成算法及其实现

> 原文:[https://www . geesforgeks . org/ls3n S3-球体-生成-算法-实现/](https://www.geeksforgeeks.org/ls3ns3-sphere-generation-algorithm-implementation/)

给定球体的中心和半径。你的任务是高效地存储在像素的计算机屏幕上显示一个球体所需的所有整数点，这个算法将通过由它的幼稚弧创建体素来生成幼稚球体。NS3 用平方和代表幼稚球，LS3 用平方和代表格子球。

示例:

```
Input : Center(0, 0, 0) Radius 1
Output : (-1, 0, 0), (0, 0, 1), (0, 0, -1), (0, 1, 0), 
         (0, -1, 0), (1, 0, 0)
         6(Total no. of points)

Input : Center(0, 0, 0) Radius 2
Output :(-2, 0, 0)(-1, 1, 1)(-1, -1, 1)(-1, 1, -1)
        (-1, -1, -1)(0, 0, 2)(0, 0, -2)(0, 2, 0)
        (0, -2, 0)(0, 1, 2)(0, 2, 1)(0, -1, 2)
        (0, 1, -2)(0, -1, -2)(0, -2, 1)(0, 2, -1)
        (0, -2, -1)(1, 2, 0)(1, 0, 2)(1, -2, 0)
        (1, 2, 0)(1, -2, 0)(1, 0, -2)(1, 0, 2)
        (1, 0, -2)(1, 1, 1)(1, -1, 1)(1, 1, -1)
        (1, -1, -1)(2, 0, 0)(2, 0, 1)(2, 0, 1)
        (2, 0, -1)(2, 0, -1)(2, 1, 0)(2, -1, 0)
        (2, 1, 0)(2, -1, 0) 
         38 (Total no. of points)

```

我强烈建议你，如果你在这个领域没有任何先决条件，不如去下面的链接。这将帮助您获得理解以下实现和算法所需的一些先决条件和概念。

算法 LS3 主要集中在生成**原生正方形**的体素。当一个离散的球体被分成 48 个部分，使得所有 48 个部分都具有某种对称关系，并且它们都可以通过使用它的任何一个部分来生成时，就形成了 prima quadraginta。这一部分称为 prima quadraginta(见图 2)。类似地，quadraginta 八分之一被定义为与 prima qudraginta 相同，只是它被分成 8 个相等的部分，而不是 48 个。quadaginta 八分体包含 6 个 prima quadraginta，如下图所示。q 表示一元八分之一(q-八分之一)，C 表示一元八分之一(C-八分之一)。原始弧是那些在 prima quadraginta 中具有相同 x 坐标的体素集合(在上图中，红色体素正在形成原始弧)。

借助于 48 个对称性质，一个完整的离散球可以从它的素二次曲面展开。**使用 48 对称性的限制是 q-八分体的一些体素将被重复，因为它们与其他相邻的 prima quadraginta 共享一条边或体素。例如，在上图中，以灰色显示的体素属于两个或多个 q 八分之一**。

我们的算法将生成一些重复的体素，因此，我们需要对输入体素进行一些限制。
为了做到这一点，我在我的实现中包含了一些功能，它们是:

**所有这些方法主要集中在灰色体素上(见上图)，除了一个小像素()之外，它将通过使用 48°对称性而不受任何限制地产生除灰色体素之外的所有体素。**

**点像素 1** :这个函数将产生所有的体素，这些体素正好有一个坐标零点
，如果我们继续使用对称性来寻找另一个体素，并且相对于那个坐标零点
轴拍摄一个图像(如果我们相对于 x 轴拍摄一个图像，这个(0，2，-1)体素将有相同的图像)，那么这个体素
就是相同的体素。

**点像素 2** :这些具有 x 和 y 坐标的体素集合是相同的(见图 2 中的 prima quadraginta)。为了存储这些体素，我们必须寻找 q1 和 q2 八分之一之间的关系(见上表)。你可以通过先交换(x，y)再交换(y，z)来获得 q1 中 q2 中任意体素的一般坐标。

**putpixelsingle** :这些像素的数量非常少，它们位于四分之一八分之一(c 八分之一)的中间，并且与位于同一 c 八分之一的所有 q 八分之一共享。为了获得这些体素，我们可以看到上表，并写出与其 c-八分体对应的所有体素。

**putpixelddouble**:这些具有 y 和 z 坐标的体素集合是相同的(参见图 2 中的 prima qudraginta)。为了存储这些体素，我们需要找到 q1 和 q6 八分之一之间的关系(见表)。你可以通过先交换(y，z)再交换(x，y)来获得 q1 中 q6 中任意体素的通用坐标。

**putpixelmiddle** :这组体素位于正好两个坐标
值为 NULL 的点上，可以帮助我们查找得到这些体素的坐标(可以手动写出这些体素的坐标
)。

我们需要高效地存储所有整数点(体素)，这些点将由该算法形成。为了存储这些点，我们将使用 hashmap，hashmap 的键值将是点的 x 坐标，数据值将是 y 和 z 坐标对的链表。

```
#include <iostream>
#include <cmath>

// this header file contains get<0> and get<1> function
#include <utility>

#include <list>
#include <map>
using namespace std;

// map to store the voxels
map<int, list<pair<int, int> > > mymap;
map<int, list<pair<int, int> > >::iterator itr;

// this function will store single voxel
void putpixelone(int m, int n, int p)
{
    mymap[m].push_back(make_pair(n, p));
}

// function to store some particular type of voxel
void putpixelmiddle(int a, int b, int c, int x, int y, int z)
{
    putpixelone(a + x, b + y, c + z);
    putpixelone(a + x, b + y, -c + z);
    putpixelone(a + x, c + y, b + z);
    putpixelone(a + x, -c + y, b + z);
    putpixelone(c + x, a + y, b + z);
    putpixelone(-c + x, a + y, b + z);
}

// This program will generate 24 voxels
void putpixeldouble(int a, int b, int c, int x, int y, int z)
{
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, b + y, c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, b + y, c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, -b + y, c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, -b + y, c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, b + y, -c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, b + y, -c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, -b + y, -c + z);
        swap(b, c);
        swap(a, b);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, -b + y, -c + z);
        swap(b, c);
        swap(a, b);
    }
}

// Explained above
void putpixelsingle(int a, int b, int c, int x,
                    int y, int z)
{
    putpixelone(a + x, b + y, c + z);
    putpixelone(-a + x, b + y, c + z);
    putpixelone(a + x, -b + y, c + z);
    putpixelone(-a + x, -b + y, c + z);
    putpixelone(a + x, b + y, -c + z);
    putpixelone(-a + x, b + y, -c + z);
    putpixelone(a + x, -b + y, -c + z);
    putpixelone(-a + x, -b + y, -c + z);
}
// This program will generate 24 voxels.
void putpixeledge2(int a, int b, int c, int x,
                   int y, int z)
{

    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, b + y, c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, b + y, c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, -b + y, c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, -b + y, c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, b + y, -c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, b + y, -c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(a + x, -b + y, -c + z);
        swap(a, b);
        swap(b, c);
    }
    for (int j = 0; j < 3; j++) {
        putpixelone(-a + x, -b + y, -c + z);
        swap(a, b);
        swap(b, c);
    }
}
// after excluding the repeated pixels from the set all 48
// pixels we will left with only 24 pixels so, we have
// defined all the voxels given below.
void putpixeledge1(int a, int b, int c, int x, int y, int z)
{
    putpixelone(a + x, b + y, c + z);
    putpixelone(a + x, c + y, b + z);
    putpixelone(a + x, -b + y, c + z);
    putpixelone(a + x, b + y, -c + z);
    putpixelone(a + x, -b + y, -c + z);
    putpixelone(a + x, -c + y, b + z);
    putpixelone(a + x, c + y, -b + z);
    putpixelone(a + x, -c + y, -b + z);
    putpixelone(b + x, c + y, a + z);
    putpixelone(b + x, a + y, c + z);
    putpixelone(b + x, -c + y, a + z);
    putpixelone(b + x, c + y, -a + z);
    putpixelone(b + x, -c + y, -a + z);
    putpixelone(b + x, a + y, -c + z);
    putpixelone(b + x, -a + y, c + z);
    putpixelone(b + x, -a + y, -c + z);
    putpixelone(c + x, a + y, b + z);
    putpixelone(c + x, -a + y, b + z);
    putpixelone(c + x, a + y, -b + z);
    putpixelone(c + x, -a + y, -b + z);
    putpixelone(c + x, b + y, a + z);
    putpixelone(c + x, -b + y, a + z);
    putpixelone(c + x, b + y, -a + z);
    putpixelone(c + x, -b + y, -a + z);
}

// voxel formation by 48 symmetry.
void putpixelall(int a, int b, int c, int x,
                 int y, int z)
{
    putpixelone(a + x, b + y, c + z);
    putpixelone(b + x, a + y, c + z);
    putpixelone(c + x, b + y, a + z);
    putpixelone(a + x, c + y, b + z);
    putpixelone(c + x, a + y, b + z);
    putpixelone(b + x, c + y, a + z);
    putpixelone(-a + x, -b + y, c + z);
    putpixelone(-b + x, -a + y, c + z);
    putpixelone(c + x, -b + y, -a + z);
    putpixelone(-a + x, c + y, -b + z);
    putpixelone(c + x, -a + y, -b + z);
    putpixelone(-b + x, c + y, -a + z);
    putpixelone(a + x, -b + y, -c + z);
    putpixelone(-b + x, a + y, -c + z);
    putpixelone(-c + x, -b + y, a + z);
    putpixelone(a + x, -c + y, -b + z);
    putpixelone(-c + x, a + y, -b + z);
    putpixelone(-b + x, -c + y, a + z);
    putpixelone(-a + x, b + y, -c + z);
    putpixelone(b + x, -a + y, -c + z);
    putpixelone(-c + x, b + y, -a + z);
    putpixelone(-a + x, -c + y, b + z);
    putpixelone(-c + x, -a + y, b + z);
    putpixelone(b + x, -c + y, -a + z);
    putpixelone(-a + x, b + y, c + z);
    putpixelone(b + x, -a + y, c + z);
    putpixelone(c + x, b + y, -a + z);
    putpixelone(-a + x, c + y, b + z);
    putpixelone(c + x, -a + y, b + z);
    putpixelone(b + x, c + y, -a + z);
    putpixelone(a + x, -b + y, c + z);
    putpixelone(-b + x, a + y, c + z);
    putpixelone(c + x, -b + y, a + z);
    putpixelone(a + x, c + y, -b + z);
    putpixelone(c + x, a + y, -b + z);
    putpixelone(-b + x, c + y, a + z);
    putpixelone(a + x, b + y, -c + z);
    putpixelone(b + x, a + y, -c + z);
    putpixelone(-c + x, b + y, a + z);
    putpixelone(a + x, -c + y, b + z);
    putpixelone(-c + x, a + y, b + z);
    putpixelone(b + x, -c + y, a + z);
    putpixelone(-a + x, -b + y, -c + z);
    putpixelone(-b + x, -a + y, -c + z);
    putpixelone(-c + x, -b + y, -a + z);
    putpixelone(-a + x, -c + y, -b + z);
    putpixelone(-c + x, -a + y, -b + z);
    putpixelone(-b + x, -c + y, -a + z);
}

// detailed explanation of this algorithm is
// given in above link.
void drawsphere(int x, int y, int z, int r)
{
    int i = 0, j = 0;
    int k0 = r;
    int k = k0;
    int s0 = 0;
    int s = s0;
    int v0 = r - 1;
    int v = v0;
    int l0 = 2 * v0;
    int l = l0;

    // this while loop will form naive arcs
    while (i <= k) {

        // this while will form voxels in naive arcs
        while (j <= k) {
            if (s > v) {
                k = k - 1;
                v = v + l;
                l = l - 2;
            }
            if ((j <= k) && ((s != v) || (j != k))) {

                // this if, else and else if condition
                // can easily build using figure 2, 3
                if (i == 0 && j != 0)

                    // First naive arc pixels and each
                    // pixel is shared with two q-octants
                    putpixeledge1(i, j, k, x, y, z);

                // voxels shared between q1 and q2
                else if (i == j && j != k && i != 0)
                    putpixeledge2(i, j, k, x, y, z);

                // center voxel of c-octants
                else if (i == j && j == k)
                    putpixelsingle(i, j, k, x, y, z);

                // voxels shared between q1 and q6
                else if (j == k && i < k && i < j)
                    putpixeldouble(i, j, k, x, y, z);

                // starting voxel of q-octant
                else if (i == 0 && j == 0)
                    putpixelmiddle(i, j, k, x, y, z);

                // voxels inside the q-octant
                else
                    putpixelall(i, j, k, x, y, z);
            }
            s = s + 2 * j + 1;
            j = j + 1;
        }
        s0 = s0 + 4 * i + 2;
        i = i + 1;

        while ((s0 > v0) && (i <= k0)) {
            k0 = k0 - 1;
            v0 = v0 + l0;
            l0 = l0 - 2;
        }
        j = i;
        k = k0;
        v = v0;
        l = l0;
        s = s0;
    }
}
// Print out all the voxels of discrete sphere
void showallpoints(map<int, list<pair<int, int> > >& mymap)
{
    int count = 0;

    for (itr = mymap.begin(); itr != mymap.end(); ++itr) {
        list<pair<int, int> > l = itr->second;
        list<pair<int, int> >::iterator it;
        for (it = l.begin(); it != l.end(); ++it) {
            cout << itr->first << ", " << get<0>(*it)
                 << ", " << get<1>(*it) << endl;
            count += 1;
        }
    }
    cout << endl;
    cout << count << endl;
}
// Driver program
int main()
{
    int cx, cy, cz;
    cin >> cx >> cy >> cz;
    int r;
    cin >> r;
    drawsphere(cx, cy, cz, r);
    showallpoints(mymap);
}
```

输入:中心(0，0，0)半径 3
输出:

```
(-3, 0, 0)(-3, 1, 1)(-3, -1, 1)(-3, 1, -1)(-3, -1, -1)
(-2, 1, 2)(-2, 2, 1)(-2, -1, 2)(-2, -2, 1)(-2, 1, -2)
(-2, 2, -1)(-2, -1, -2)(-2, -2, -1)(-1, 1, 3)(-1, 3, 1)
(-1, -1, 3)(-1, -3, 1)(-1, 1, -3)(-1, 3, -1)(-1, -1, -3)
(-1, -3, -1)(-1, 2, 2)(-1, -2, 2)(-1, 2, -2)(-1, -2, -2)
(0, 0, 3)(0, 0, -3)(0, 3, 0)(0, -3, 0)(0, 1, 3)(0, 3, 1)
(0, -1, 3)(0, 1, -3)(0, -1, -3)(0, -3, 1)(0, 3, -1)
(0, -3, -1)(0, 2, 2)(0, 2, 2)(0, -2, 2)(0, 2, -2)
(0, -2, -2)(0, -2, 2)(0, 2, -2)(0, -2, -2)(1, 3, 0)
(1, 0, 3)(1, -3, 0)(1, 3, 0)(1, -3, 0)(1, 0, -3)(1, 0, 3)
(1, 0, -3)(1, 1, 3)(1, 3, 1)(1, -1, 3)(1, -3, 1)(1, 1, -3)
(1, 3, -1)(1, -1, -3)(1, -3, -1)(1, 2, 2)(1, -2, 2)(1, 2, -2)
(1, -2, -2)(2, 2, 0)(2, 0, 2)(2, -2, 0)(2, 2, 0)(2, -2, 0)
(2, 0, -2)(2, 0, 2)(2, 0, -2)(2, 0, 2)(2, 0, 2)(2, 0, -2)
(2, 0, -2)(2, 2, 0)(2, -2, 0)(2, 2, 0)(2, -2, 0)(2, 1, 2)
(2, 2, 1)(2, -1, 2)(2, -2, 1)(2, 1, -2)(2, 2, -1)(2, -1, -2)
(2, -2, -1)(3, 0, 0)(3, 0, 1)(3, 0, 1)(3, 0, -1)(3, 0, -1)
(3, 1, 0)(3, -1, 0)(3, 1, 0)(3, -1, 0)(3, 1, 1)(3, -1, 1)
(3, 1, -1)(3, -1, -1)
102 (Total no. of points)

```

**参考文献:**
[http://www . science direct . com/science/article/pii/S0304397515010178 # TL 0010](http://www.sciencedirect.com/science/article/pii/S0304397515010178#tl0010)

本文由**哈什·库马尔·辛格**投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。