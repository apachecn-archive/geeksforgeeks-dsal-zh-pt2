# 未排序数组中每个元素的累计计数频率

> 原文:[https://www . geeksforgeeks . org/未排序数组中每个元素的累计计数频率/](https://www.geeksforgeeks.org/cumulative-frequency-of-count-of-each-element-in-an-unsorted-array/)

给定一个未排序的数组。任务是使用计数数组计算数组中每个元素的**累计频率**。

**示例:**

```
Input : arr[] = [1, 2, 2, 1, 3, 4]
Output :1->2
        2->4
        3->5
        4->6

Input : arr[] = [1, 1, 1, 2, 2, 2]
Output :1->3
        2->6 
```

一个**简单的解决方案**是使用两个嵌套循环。外部循环从左到右选取一个未被访问的元素。内部循环计算其出现次数并将出现次数标记为已访问。这个解的时间复杂度是 O(n*n)，需要的辅助空间是 O(n)。

一个**更好的解决方案**是使用排序。我们对数组进行排序，以便相同的元素聚集在一起。排序后，我们线性遍历元素并计算它们的频率。

一个有效的解决方案是使用散列法。将元素及其频率插入一组对中。由于集合以排序顺序存储唯一值，因此它将以排序顺序存储所有元素及其频率。迭代该集合，并通过在每一步添加前面的频率来打印频率。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to print the cumulative frequency according to
// the order given
void countFreq(int a[], int n)
{

    // Declaring a map so values get inserted in a sorted
    // manner
    map<int, int> m;

    // Inserting values into the map
    for (int i = 0; i < n; i++) {
        m[a[i]]++;
    }

    // Variable to store the count of previous number
    // cumulative frequency
    int cumul = 0;
    for (auto v : m) {
        cout << v.first << " " << v.second + cumul
             << endl;
        cumul += v.second;
    }
}

int main()
{
    int arr[] = { 1, 3, 2, 4, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    countFreq(arr, n);
    return 0;
}

// This code is contributed by Vinayak Pareek (Kargil)
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count cumulative
// frequencies of elements in an unsorted array.
import java.util.*;

class GFG
{
    static void countFreq(int[] a, int n)
    {

        // Insert elements and their
        // frequencies in hash map.
        HashMap<Integer,
                Integer> hm = new HashMap<>();
        for (int i = 0; i < n; i++)
            hm.put(a[i], hm.get(a[i]) == null ?
                     1 : hm.get(a[i]) + 1);

        // Declare a Map
        SortedMap<Integer, Integer> st = new TreeMap<>();

        // insert the element and
        // and insert its frequency in a set
        for (HashMap.Entry<Integer,
                           Integer> x : hm.entrySet())
        {
            st.put(x.getKey(), x.getValue());
        }

        int cumul = 0;

        // iterate the set and print the
        // cumulative frequency
        for (SortedMap.Entry<Integer,
                             Integer> x : st.entrySet())
        {
            cumul += x.getValue();
            System.out.println(x.getKey() + " " + cumul);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 1, 3, 2, 4, 2, 1 };
        int n = a.length;
        countFreq(a, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to count cumulative
# frequencies of elements in an unsorted array.
def countFreq(a, n):

    # Insert elements and their
    # frequencies in hash map.
    hm = {}
    for i in range(0, n):
        hm[a[i]] = hm.get(a[i], 0) + 1

    # Declare a set
    st = set()

    # Insert the element and
    # its frequency in a set
    for x in hm:
        st.add((x, hm[x]))

    cumul = 0

    # Iterate the set and print
    # the cumulative frequency
    for x in sorted(st):
        cumul += x[1]
        print(x[0], cumul)

# Driver Code
if __name__ == "__main__":

    a = [1, 3, 2, 4, 2, 1]
    n = len(a)
    countFreq(a, n)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count cumulative
// frequencies of elements in an
// unsorted array.
using System;
using System.Collections.Generic;
using System.Linq;

class GFG{

static void countFreq(int[] a, int n)
{

    // Insert elements and their
    // frequencies in hash map.
    Dictionary<int,
               int> hm = new Dictionary<int,
                                        int>();
    for(int i = 0; i < n; i++)
    {
        if (hm.ContainsKey(a[i]))
        {
            hm[a[i]]++;
        }
        else
        {
            hm[a[i]] = 1;
        }
    }

    int cumul = 0;

    // Iterate the set and print the
    // cumulative frequency
    foreach(KeyValuePair<int,
                         int> x in hm.OrderBy(key => key.Key))
    {
        cumul += x.Value;
        Console.Write(x.Key + " " + cumul + "\n");
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] a = { 1, 3, 2, 4, 2, 1 };
    int n = a.Length;

    countFreq(a, n);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to count cumulative
// frequencies of elements in an unsorted array.

    function countFreq(a,n)
    {
        // Insert elements and their
        // frequencies in hash map.
        let hm = new Map();
        for (let i = 0; i < n; i++)
            hm.set(a[i], hm.get(a[i]) == null ?
                     1 : hm.get(a[i]) + 1);

        // Declare a Map
        let st = new Set();

        // insert the element and
        // and insert its frequency in a set
        for (let [key, value] of hm.entries())
        {   
            st.add([key, value]);
        }
          st=[...st.entries()].sort()
        let cumul = 0;

        // iterate the set and print the
        // cumulative frequency
        for (let [key, value] of st.entries())
        {
            cumul += value[1][1];
            document.write(value[1][0] + " " + cumul+"<br>");
        }
    }

    // Driver Code
    let a=[1, 3, 2, 4, 2, 1];
    let n = a.length;
    countFreq(a, n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
1 2
2 4
3 5
4 6
```

解的时间复杂度为 **O(n log n)** 。

**如果我们按照第一次出现的顺序需要元素的频率呢？**
比如一个数组【2，4，1，2，1，3，4】，应该先打印 2 的频率，然后是 4 的频率，然后是 1，最后是 3。

**方法:**散列一个元素的出现次数。在数组中遍历并打印累计频率。打印完元素及其累积频率后，将该元素的出现散列为 0，这样，如果它在遍历时出现在数组的后半部分，就不会再次打印。

下面是上述方法的实现:

## C++

```
// C++ program to print the cumulative frequency
// according to the order given
#include <bits/stdc++.h>
using namespace std;

// Function to print the cumulative frequency
// according to the order given
void countFreq(int a[], int n)
{
    // Insert elements and their
    // frequencies in hash map.
    unordered_map<int, int> hm;
    for (int i=0; i<n; i++)
        hm[a[i]]++;
    int cumul = 0;

   // traverse in the array
   for(int i=0;i<n;i++)
   {
       // add the frequencies
       cumul += hm[a[i]];

       // if the element has not been
       // visited previously
       if(hm[a[i]])
       {
           cout << a[i] << "->" << cumul << endl;
       }
       // mark the hash 0
       // as the element's cumulative frequency
       // has been printed
       hm[a[i]]=0;
   }
}

// Driver Code
int main()
{
    int a[] = {1, 3, 2, 4, 2, 1};
    int n = sizeof(a)/sizeof(a[0]);
    countFreq(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the cumulative frequency
// according to the order given
class GFG
{

// Function to print the cumulative frequency
// according to the order given
static void countFreq(int a[], int n)
{
    // Insert elements and their
    // frequencies in hash map.
    int hm[] = new int[n];
    for (int i = 0; i < n; i++)
        hm[a[i]]++;
    int cumul = 0;

// traverse in the array
for(int i = 0; i < n; i++)
{
    // add the frequencies
    cumul += hm[a[i]];

    // if the element has not been
    // visited previously
    if(hm[a[i]] != 0)
    {
        System.out.println(a[i] + "->" + cumul);
    }
    // mark the hash 0
    // as the element's cumulative frequency
    // has been printed
    hm[a[i]] = 0;
}
}

// Driver Code
public static void main(String[] args)
{
    int a[] = {1, 3, 2, 4, 2, 1};
    int n = a.length;
    countFreq(a, n);
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print the cumulative
# frequency according to the order given

# Function to print the cumulative frequency
# according to the order given
def countFreq(a, n):

    # Insert elements and their
    # frequencies in hash map.
    hm = dict()
    for i in range(n):
        hm[a[i]] = hm.get(a[i], 0) + 1

    cumul = 0

    # traverse in the array
    for i in range(n):

    # add the frequencies
        cumul += hm[a[i]]

    # if the element has not been
    # visited previously
        if(hm[a[i]] > 0):
            print(a[i], "->", cumul)

    # mark the hash 0
    # as the element's cumulative
    # frequency has been printed
        hm[a[i]] = 0

# Driver Code
a = [1, 3, 2, 4, 2, 1]
n = len(a)
countFreq(a, n)

# This code is contributed by mohit kumar
```

## C#

```
// C# program to print the cumulative frequency
// according to the order given
using System;

class GFG
{

// Function to print the cumulative frequency
// according to the order given
static void countFreq(int []a, int n)
{
    // Insert elements and their
    // frequencies in hash map.
    int []hm = new int[n];
    for (int i = 0; i < n; i++)
        hm[a[i]]++;
    int cumul = 0;

// traverse in the array
for(int i = 0; i < n; i++)
{
    // add the frequencies
    cumul += hm[a[i]];

    // if the element has not been
    // visited previously
    if(hm[a[i]] != 0)
    {
        Console.WriteLine(a[i] + "->" + cumul);
    }

    // mark the hash 0
    // as the element's cumulative frequency
    // has been printed
    hm[a[i]] = 0;
}
}

// Driver Code
public static void Main(String[] args)
{
    int []a = {1, 3, 2, 4, 2, 1};
    int n = a.Length;
    countFreq(a, n);
}
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// Javascript program to print the cumulative frequency
// according to the order given

// Function to print the cumulative frequency
// according to the order given
function countFreq(a,n) {
    // Insert elements and their
    // frequencies in hash map.
    let hm = new Array(n);
    for(let i=0;i<hm.length;i++)
    {
        hm[i]=0;
    }
    for (let i = 0; i < n; i++)
        hm[a[i]]++;
    let cumul = 0;

    // traverse in the array
    for(let i = 0; i < n; i++)
    {
        // add the frequencies
        cumul += hm[a[i]];

        // if the element has not been
        // visited previously
        if(hm[a[i]] != 0)
        {
            document.write(a[i] + "->" + cumul+"<br>");
        }
        // mark the hash 0
        // as the element's cumulative frequency
        // has been printed
        hm[a[i]] = 0;
    }

}

// Driver Code
let a=[1, 3, 2, 4, 2, 1];
let n = a.length;
countFreq(a, n);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
1->2
3->3
2->5
4->6
```

本文由 [**喜马拉雅冉冉**](https://auth.geeksforgeeks.org/profile.php?user=himanshu_300) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。