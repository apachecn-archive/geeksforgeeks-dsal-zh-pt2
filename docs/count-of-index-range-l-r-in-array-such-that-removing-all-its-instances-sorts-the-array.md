# 数组中索引范围[L，R]的计数，移除其所有实例会对数组进行排序

> 原文:[https://www . geesforgeks . org/count-of-index-range-l-r-in-array-so-remove-all-it-instance-sort-the-array/](https://www.geeksforgeeks.org/count-of-index-range-l-r-in-array-such-that-removing-all-its-instances-sorts-the-array/)

给定一个长度为 **N、**的[阵](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在[阵](https://www.geeksforgeeks.org/array-data-structure/) **arr[]中找到**好射程**的数量。**

A **良好范围**定义为左右指标的范围，即[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**中的**【L . R】**，这样通过去掉[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的范围**【L，R】**中的所有数字以及范围外的那些元素的出现，[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**就变成了

**示例:**

> **输入:** N=3，arr[] = {9，8，7}
> **输出:** 3
> **说明:**好的范围是:(2，3)，(1，3)，(1，2)。
> (2，3)是一个很好的范围，因为结果数组[9]是排序的(我们删除了 8，7)。
> (1，3)是一个很好的范围，因为结果数组[]被排序(我们删除了 9，8，7)
> (1，2)是一个很好的范围，因为结果数组[7]被排序(我们删除了 9，8) **。**
> 
> **输入:** N=5，arr[] = {5，3，1，5，2}
> **输出:** 7
> **说明:**好的范围是:(1，2)、(1，3)、(1，4)、(1，5)、(2，4)、(2，5)、(3，5)。
> (1，2)是良好的范围，因为结果数组[1，2]被排序
> (1，3)是良好的范围，因为结果数组[2]被排序
> (1，4)是良好的范围
> (1，5)是良好的范围，因为结果数组[]被排序
> (2，4)是良好的范围，因为结果数组[2]被排序
> (2，5)是良好的范围，因为结果

**方式:**方式是找到每一个[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)**【l，r】**检查剩余的[阵](https://www.geeksforgeeks.org/array-data-structure/)是否排序。如果对[数组](https://www.geeksforgeeks.org/array-data-structure/)进行排序，那么，范围的左边部分在 **l** ，右边部分从 **r** 到最后，每个[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)都将是答案。下面是上述方法的实现:

*   将变量**计数**初始化为 **0** ，以存储此类[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量。
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-python/) **chk_sorted(l，r，a)** 来检查剩余的[数组](https://www.geeksforgeeks.org/array-data-structure/)**a【】**是否排序:
    *   [初始化列表](https://www.geeksforgeeks.org/python-initialize-list-with-empty-dictionaries/) **l** 以存储从 **l** 到 **r** 的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)在[阵列](https://www.geeksforgeeks.org/array-data-structure/) **a[]中的所有元素。**
    *   初始化[数组](https://www.geeksforgeeks.org/python-arrays/) **chk[]** 来存储[数组](https://www.geeksforgeeks.org/python-arrays/)**【**中不在**【l，r】范围内的元素。**
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
        *   如果 **a[i]** 不在[列表](https://www.geeksforgeeks.org/python-list/) **l、**中，则将元素存储在[数组](https://www.geeksforgeeks.org/python-arrays/) **chk[]中。**
    *   [初始化列表](https://www.geeksforgeeks.org/python-initialize-list-with-empty-dictionaries/) **chk1** 存储[数组](https://www.geeksforgeeks.org/array-data-structure/) **chk[]。**
    *   [对列表](https://www.geeksforgeeks.org/python-list-sort/) **chk1** 进行排序，检查 **chk1** 是否等于 **chk，**则返回 **true** 否则返回 **false。**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，N】**，并执行以下步骤:
        *   调用[函数](https://www.geeksforgeeks.org/functions-in-python/) **chk_sorted(i，j，a)** ，如果函数返回 **true，**则通过 **len(a)-j** 和**增加**计数**的值，断开**循环**。**
*   返回**的值，算**为答案。

下面是上述方法的实现。

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to chk array is sorted or not
bool chk_sorted(int l, int r, vector<int> a)
{

    // Taking range element separately
    // to be removed
    vector<int> temp;
    unordered_set<int> s;
    for(int i = l; i <= r; i++)
    {
        temp.push_back(a[i]);
        s.insert(a[i]);
    }

    vector<int> chk;
    for(int i = 0; i < a.size(); i++)
    {

        // Checking is all range element
        // occurrence is removed
        if (s.find(a[i]) == s.end())
        {
            chk.push_back(a[i]);
        }
    }

    vector<int> chk1 = chk;

    sort(chk1.begin(), chk1.end());

    // If array is sorted return true
    for(int i = 0; i < chk.size(); i++)
    {
        if (chk[i] != chk1[i])
        {
            return false;
        }
    }
    return true;
}

// Function to count all good ranges
int countp(vector<int> a)
{

    // Initial count 0
    int count = 0;

    // Nested loop implementation
    for(int i = 0; i < a.size(); i++)
    {
        for(int j = i + 1; j < a.size(); j++)
        {

            // Checking if range is good
            if (chk_sorted(i, j, a))
            {

                // According to observation as given
                // in approach
                count += a.size() - j;
                break;
            }
        }
    }
    return count;
}

// Driver code
int main()
{
    int N = 5;
    vector<int> A = { 5, 3, 1, 5, 2 };

    cout << (countp(A));
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.*;

class GFG{

// Function to chk array is sorted or not
static boolean chk_sorted(int l, int r, int []a)
{

    // Taking range element separately
    // to be removed
    Vector<Integer> temp = new Vector<Integer>();
    HashSet<Integer> s = new HashSet<Integer>();
    for(int i = l; i <= r; i++)
    {
        temp.add(a[i]);
        s.add(a[i]);
    }

    Vector<Integer> chk=new Vector<Integer>();
    for(int i = 0; i < a.length; i++)
    {

        // Checking is all range element
        // occurrence is removed
        if (!s.contains(a[i]))
        {
            chk.add(a[i]);
        }
    }

    Vector<Integer> chk1 = new Vector<Integer>(chk);

    Collections.sort(chk1);

    // If array is sorted return true
    for(int i = 0; i < chk.size(); i++)
    {
        if (chk.get(i) != chk1.get(i))
        {
            return false;
        }
    }
    return true;
}

// Function to count all good ranges
static int countp(int []a)
{

    // Initial count 0
    int count = 0;

    // Nested loop implementation
    for(int i = 0; i < a.length; i++)
    {
        for(int j = i + 1; j < a.length; j++)
        {

            // Checking if range is good
            if (chk_sorted(i, j, a))
            {

                // According to observation as given
                // in approach
                count += a.length - j;
                break;
            }
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int N = 5;
    int [] A = { 5, 3, 1, 5, 2 };

    System.out.print(countp(A));
}
}
// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program to implement the above approach

# function to chk array is sorted or not
def chk_sorted(l, r, a):

    # taking range element separately
    # to be removed
    l = list(a[l:r + 1])

    chk = []
    for i in a:
        # checking is all range element
        # occurrence is removed
        if(i not in l):
            chk.append(i)
    chk1 = list(chk)
    chk1.sort()
    # if array is sorted return true
    if(chk1 == chk):
        return True
    else:
        return False

# function to count all good ranges
def countp(a):

    # initial count 0
    count = 0

    # nested loop implementation
    for i in range(len(a)):
        for j in range(i + 1, len(a)):

            # checking if range is good
            if(chk_sorted(i, j, a)):

                # according to observation as given
                # in approach
                count += len(a)-j
                break
    return count

# Driver code
N = 5
A = [5, 3, 1, 5, 2]
print(countp(A))
```

## C#

```
// C# program to implement the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to chk array is sorted or not
    static bool chk_sorted(int l, int r, int[] a)
    {

        // Taking range element separately
        // to be removed
        List<int> temp = new List<int>();
        HashSet<int> s = new HashSet<int>();
        for (int i = l; i <= r; i++) {
            temp.Add(a[i]);
            s.Add(a[i]);
        }

        List<int> chk = new List<int>();
        for (int i = 0; i < a.Length; i++) {

            // Checking is all range element
            // occurrence is removed
            if (!s.Contains(a[i])) {
                chk.Add(a[i]);
            }
        }

        List<int> chk1 = new List<int>(chk);

        chk1.Sort();

        // If array is sorted return true
        for (int i = 0; i < chk.Count; i++) {
            if (chk[i] != chk1[i]) {
                return false;
            }
        }
        return true;
    }

    // Function to count all good ranges
    static int countp(int[] a)
    {

        // Initial count 0
        int count = 0;

        // Nested loop implementation
        for (int i = 0; i < a.Length; i++) {
            for (int j = i + 1; j < a.Length; j++) {

                // Checking if range is good
                if (chk_sorted(i, j, a)) {

                    // According to observation as given
                    // in approach
                    count += a.Length - j;
                    break;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int[] A = { 5, 3, 1, 5, 2 };

        Console.WriteLine(countp(A));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// function to chk array is sorted or not
function chk_sorted(l, r, a){

    // taking range element separately
    // to be removed
    l = a.slice(l, r + 1)

    let chk = []
    for (let i of a){
        // checking is all range element
        // occurrence is removed
        if(!l.includes(i)){
            chk.push(i)
        }
    }

    let chk1 = [...chk]

    chk1.sort()

    // if array is sorted return true

    if(chk1.every((val, index) => val == chk[index]))
        return true
    else
        return false
}

// function to count all good ranges
function countp(a){

    // initial count 0
    let count = 0

    // nested loop implementation
    for (let i  = 0; i < a.length; i++){
        for(let j = i + 1; j < a.length; j++){

            // checking if range is good
            if(chk_sorted(i, j, a)){

                // according to observation as given
                // in approach
                count += a.length - j
                break
            }
        }
    }
    return count
}

// Driver code
let N = 5
let A = [5, 3, 1, 5, 2]
document.write(countp(A))

</script>
```

**Output**

```
7
```

***时间复杂度:**O(N * N * N)*
T5**辅助空间:** O(N)