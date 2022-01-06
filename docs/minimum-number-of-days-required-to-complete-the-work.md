# 完成工作所需的最短天数

> 原文:[https://www . geesforgeks . org/完成工作所需的最短天数/](https://www.geeksforgeeks.org/minimum-number-of-days-required-to-complete-the-work/)

给定从 1 到 N 的 N 个作品。给定两个数组，D1[]和 D2[]各有 N 个元素。另外，每个工作号 W(i)被分配了天数，D1[i]和 D2[i] ( *)这样，D2[I]<【I】*)中的任何一个都可以完成。
还有，提到每项工作都要按照【D1】阵**不减日完成。
任务是在 D1[]找到按非递减天数顺序完成工作所需的**最小天数**。**

**示例**:

> **输入:**
> N = 3
> D1[] = {5，3，4}
> D2[] = {2，1，2}
> **输出:** 2
> **说明:**
> 3 项工作待完成。第(I)行的第一个值是 D1(i)，第二个值是 D2(i)，其中 D2(i) < D1(i)。聪明的工人可以在第一天完成第二项工作，然后在第二天完成第三项工作和第一项工作，从而保持 D1[]，[3 4 5]的不递减顺序。
> 
> **输入:**T2】N = 6
> D1[]= { 3，3，4，4，5，5}
> D2[] = {1，2，1，2，4，4 }
> T6】输出: 4

### [推荐:请先在 ***<u>{IDE}</u>*** 上尝试您的方法，然后再进入解决方案。](https://ide.geeksforgeeks.org/)

**进场:**解是贪婪的。工作(I)可以通过增加 D1[i]，通过增加 D2[i]打破联系来分类。如果我们按照这个顺序考虑工作，我们可以试着尽早完成工作。首先完成 D2 的第一部作品[1]。转到第二部作品。如果我们能在 D2[2]日完成它，那么(D2[1] < =D2[2])，就去做。否则，在 D[2]天做这项工作。重复这个过程，直到我们完成第 N 个工作，保留当天最新的工作。
以下是上述办法的实施情况。

## C++

```
// C++ program to find the minimum
// number days required

#include <bits/stdc++.h>
using namespace std;
#define inf INT_MAX

// Function to find the minimum
// number days required
int minimumDays(int N, int D1[], int D2[])
{
    // initialising ans to least value possible
    int ans = -inf;

    // vector to store the pair of D1(i) and D2(i)
    vector<pair<int, int> > vect;

    for (int i = 0; i < N; i++)
        vect.push_back(make_pair(D1[i], D2[i]));

    // sort by first i.e D(i)
    sort(vect.begin(), vect.end());

    // Calculate the minimum possible days
    for (int i = 0; i < N; i++) {
        if (vect[i].second >= ans)
            ans = vect[i].second;
        else
            ans = vect[i].first;
    }

    // return the answer
    return ans;
}

// Driver Code
int main()
{
    // Number of works
    int N = 3;

    // D1[i]
    int D1[] = { 6, 5, 4 };

    // D2[i]
    int D2[] = { 1, 2, 3 };

    cout<<minimumDays(N, D1, D2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// number days required
import java.util.*;
import java.lang.*;
import java.io.*;

// pair class for number of days
class Pair
{
    int x, y;

    Pair(int a, int b)
    {
        this.x = a;
        this.y = b;
    }
}

class GFG
{
static int inf = Integer.MIN_VALUE;

// Function to find the minimum
// number days required
public static int minimumDays(int N, int D1[],
                              int D2[])
{
    // initialising ans to
    // least value possible
    int ans = -inf;

    ArrayList<Pair>
              list = new ArrayList<Pair>();

    for (int i = 0; i < N; i++)
    list.add(new Pair(D1[i], D2[i]));

    // sort by first i.e D(i)
    Collections.sort(list, new Comparator<Pair>()
    {
        @Override
        public int compare(Pair p1, Pair p2)
        {
            return p1.x - p2.x;
        }
    });

// Calculate the minimum possible days
for (int i = 0; i < N; i++)
{
    if (list.get(i).y >= ans)
        ans = list.get(i).y;
    else
        ans = list.get(i).x;
}

return ans;
}

// Driver Code
public static void main (String[] args)
{
    // Number of works
    int N = 3;

    // D1[i]
    int D1[] = new int[]{6, 5, 4};

    // D2[i]
    int D2[] = new int[]{1, 2, 3};

    System.out.print(minimumDays(N, D1, D2));
}
}

// This code is contributed by Kirti_Mangal
```

## java 描述语言

```
<script>

// Javascript program to find the minimum
// number days required

// Function to find the minimum
// number days required
function minimumDays(N, D1, D2)
{
    // initialising ans to least value possible
    var ans = -1000000000;

    // vector to store the pair of D1(i) and D2(i)
    var vect = [];

    for (var i = 0; i < N; i++)
        vect.push([D1[i], D2[i]]);

    // sort by first i.e D(i)
    vect.sort((a,b)=>a-b)

    // Calculate the minimum possible days
    for (var i = 0; i < N; i++) {
        if (vect[i][1] >= ans)
            ans = vect[i][1];
        else
            ans = vect[i][0];
    }

    // return the answer
    return ans;
}

// Driver Code
// Number of works
var N = 3;

// D1[i]
var D1 = [6, 5, 4 ];

// D2[i]
var D2 = [1, 2, 3 ];
document.write( minimumDays(N, D1, D2));

</script>
```

**Output:** 

```
6
```