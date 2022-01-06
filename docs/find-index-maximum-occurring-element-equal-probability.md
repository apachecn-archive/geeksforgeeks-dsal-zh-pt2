# 等概率找到最大出现元素的索引

> 原文:[https://www . geesforgeks . org/find-index-最大出现元素-等概率/](https://www.geeksforgeeks.org/find-index-maximum-occurring-element-equal-probability/)

给定一个整数数组，找到数组中出现次数最多的元素，并以相等的概率随机返回它的任何一个索引。
示例:

```
Input: 
arr[] = [-1, 4, 9, 7, 7, 2, 7, 3, 0, 9, 6, 5, 7, 8, 9]

Output:  
Element with maximum frequency present at index 6
OR
Element with maximum frequency present at Index 3
OR
Element with maximum frequency present at index 4
OR
Element with maximum frequency present at index 12

All outputs above have equal probability.
```

其思想是遍历数组一次，找出最大出现元素及其出现频率 n，然后我们生成一个 1 到 n 之间的随机数 r，最后返回数组中最大出现元素的第 r 次出现。
以下是上述想法的实现–

## C++

```
// C++ program to return index of most occurring element
// of the array randomly with equal probability
#include <iostream>
#include <unordered_map>
#include <climits>
using namespace std;

// Function to return index of most occurring element
// of the array randomly with equal probability
void findRandomIndexOfMax(int arr[], int n)
{
    // freq store frequency of each element in the array
    unordered_map<int, int> freq;
    for (int i = 0; i < n; i++)
        freq[arr[i]] += 1;

    int max_element; // stores max occurring element

    // stores count of max occurring element
    int max_so_far = INT_MIN;

    // traverse each pair in map and find maximum
    // occurring element and its frequency
    for (pair<int, int> p : freq)
    {
        if (p.second > max_so_far)
        {
            max_so_far = p.second;
            max_element = p.first;
        }
    }

    // generate a random number between [1, max_so_far]
    int r = (rand() % max_so_far) + 1;

    // traverse array again and return index of rth
    // occurrence of max element
    for (int i = 0, count = 0; i < n; i++)
    {
        if (arr[i] == max_element)
            count++;

        // print index of rth occurrence of max element
        if (count == r)
        {
            cout << "Element with maximum frequency present "
                 "at index " << i << endl;
            break;
        }
    }
}

// Driver code
int main()
{
    // input array
    int arr[] = { -1, 4, 9, 7, 7, 2, 7, 3, 0, 9, 6, 5,
                  7, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // randomize seed
    srand(time(NULL));

    findRandomIndexOfMax(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to return index of most occurring element
// of the array randomly with equal probability
import java.util.*;

class GFG
{

// Function to return index of most occurring element
// of the array randomly with equal probability
static void findRandomIndexOfMax(int arr[], int n)
{
    // freq store frequency of each element in the array
    HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();
    for (int i = 0; i < n; i++)
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }

    int max_element = Integer.MIN_VALUE; // stores max occurring element

    // stores count of max occurring element
    int max_so_far = Integer.MIN_VALUE;

    // traverse each pair in map and find maximum
    // occurring element and its frequency
    for (Map.Entry<Integer, Integer> p : mp.entrySet())
    {
        if (p.getValue() > max_so_far)
        {
            max_so_far = p.getValue();
            max_element = p.getKey();
        }
    }

    // generate a random number between [1, max_so_far]
    int r = (int) ((new Random().nextInt(max_so_far) % max_so_far) + 1);

    // traverse array again and return index of rth
    // occurrence of max element
    for (int i = 0, count = 0; i < n; i++)
    {
        if (arr[i] == max_element)
            count++;

        // print index of rth occurrence of max element
        if (count == r)
        {
            System.out.print("Element with maximum frequency present "
                +"at index " + i +"\n");
            break;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    // input array
    int arr[] = { -1, 4, 9, 7, 7, 2, 7, 3, 0, 9, 6, 5,
                7, 8, 9 };
    int n = arr.length;
    findRandomIndexOfMax(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to return index of most occurring element
# of the array randomly with equal probability
import random

# Function to return index of most occurring element
# of the array randomly with equal probability
def findRandomIndexOfMax(arr, n):

    # freq store frequency of each element in the array
    mp = dict()
    for i in range(n) :
        if(arr[i] in mp):
            mp[arr[i]] = mp[arr[i]] + 1

        else:
            mp[arr[i]] = 1

    max_element = -323567
    # stores max occurring element

    # stores count of max occurring element
    max_so_far = -323567

    # traverse each pair in map and find maximum
    # occurring element and its frequency
    for p in mp :

        if (mp[p] > max_so_far):
            max_so_far = mp[p]
            max_element = p

    # generate a random number between [1, max_so_far]
    r = int( ((random.randrange(1, max_so_far, 2) % max_so_far) + 1))

    i = 0
    count = 0

    # traverse array again and return index of rth
    # occurrence of max element
    while ( i < n ):

        if (arr[i] == max_element):
            count = count + 1

        # Print index of rth occurrence of max element
        if (count == r):

            print("Element with maximum frequency present at index " , i )
            break
        i = i + 1

# Driver code

# input array
arr = [-1, 4, 9, 7, 7, 2, 7, 3, 0, 9, 6, 5, 7, 8, 9]
n = len(arr)
findRandomIndexOfMax(arr, n)

# This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript program to return index of most occurring element
// of the array randomly with equal probability

// Function to return index of most occurring element
// of the array randomly with equal probability
function findRandomIndexOfMax(arr,n)
{
    // freq store frequency of each element in the array
    let mp = new Map();
    for (let i = 0; i < n; i++)
        if(mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }

    let max_element = Number.MIN_VALUE; // stores max occurring element

    // stores count of max occurring element
    let max_so_far = Number.MIN_VALUE;

    // traverse each pair in map and find maximum
    // occurring element and its frequency
    for (let [key, value] of mp.entries())
    {
        if (value > max_so_far)
        {
            max_so_far = value;
            max_element = key;
        }
    }

    // generate a random number between [1, max_so_far]

    let r = Math.floor(((Math.random() * max_so_far)% max_so_far)+ 1)

    // traverse array again and return index of rth
    // occurrence of max element
    for (let i = 0, count = 0; i < n; i++)
    {
        if (arr[i] == max_element)
            count++;

        // print index of rth occurrence of max element
        if (count == r)
        {
            document.write("Element with maximum frequency present "
                +"at index " + i +"<br>");
            break;
        }
    }
}

// Driver code
let arr=[-1, 4, 9, 7, 7, 2, 7, 3, 0, 9, 6, 5,
                7, 8, 9 ];
let n = arr.length;
findRandomIndexOfMax(arr, n);

// This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Element with maximum frequency present at index 4
```

**上述解的时间复杂度**为 O(n)。
**辅助空间**所使用的程序是 O(n)。
本文由 **Aditya Goel** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。