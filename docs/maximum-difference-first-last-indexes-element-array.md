# 数组中元素的第一个和最后一个索引之间的最大差异

> 原文:[https://www . geesforgeks . org/maximum-difference-first-last-indexes-element-array/](https://www.geeksforgeeks.org/maximum-difference-first-last-indexes-element-array/)

给定 n 个整数的数组。任务是找出每个不同元素的第一个和最后一个索引的差异，从而使差异最大化。

示例:

```
Input : {2, 1, 3, 4, 2, 1, 5, 1, 7}
Output : 6
Element 1 has its first index = 1
and last index = 7
Difference = 7 - 1 = 6
Other elements have a smaller first and last
index difference

Input : {2, 2, 1, 1, 8, 8, 3, 5, 3} 
Output : 2
Maximum difference is for indexes of element 3.

```

一种简单的方法是运行两个循环，找出每个元素的差异，并相应地更新 **max_diff** 。它的时间复杂度为 0(n<sup>2</sup>)，并且该方法还需要跟踪已经访问过的元素，以便不会不必要地计算它们的差异。

一种有效的方法使用散列。它有以下步骤。

1.  从左到右遍历输入数组。
2.  对于每个不同的元素，映射它在哈希表中的第一个和最后一个索引。
3.  遍历哈希表，计算每个元素的第一个和最后一个索引差。
4.  相应地更新 **max_diff** 。

在下面的实现中[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)被用于散列，因为整数的范围是未知的。

## C++

```
// C++ implementation to find the maximum difference 
// of first and last index of array elements
#include <bits/stdc++.h>

using namespace std;

// function to find the
// maximum difference
int maxDifference(int arr[], int n)
{
    // structure to store first and last
    // index of each distinct element
    struct index
    {
        int f, l;
    };

    // maps each element to its
    // 'index' structure
    unordered_map<int, index> um;

    for (int i=0; i<n; i++)
    {
        // storing first index
        if (um.find(arr[i]) == um.end())
            um[arr[i]].f = i;

        // storing last index    
        um[arr[i]].l = i;    
    }

    int diff, max_diff = INT_MIN;

    unordered_map<int, index>::iterator itr;

    // traversing 'um'
    for (itr=um.begin(); itr != um.end(); itr++)
    {   
        // difference of last and first index
        // of each element
        diff = (itr->second).l - (itr->second).f;

        // update 'max_dff'
        if (max_diff < diff)
            max_diff = diff;
    }

    // required maximum difference
    return max_diff;
}

// Driver program to test above
int main()
{
    int arr[] = {2, 1, 3, 4, 2, 1, 5, 1, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Difference = " 
         <<maxDifference(arr, n);
    return 0;     
} 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the maximum difference 
// of first and last index of array elements
import java.util.HashMap;
import java.util.Map;

public class MaxDiffIndexHashing {

    static class Element {
        int first;
        int second;

        public Element() {
            super();
        }

        public Element(int first, int second) {
            super();
            this.first = first;
            this.second = second;
        }
    }

    public static void main(String[] args) {

        int arr[]={2, 1, 3, 4, 2, 1, 5, 1, 7};
        System.out.println("Maximum Difference= "+ maxDiffIndices(arr));
    }

    private static int maxDiffIndices(int[] arr) {
        int n = arr.length;
        int maxDiffIndex = 0;
        Map<Integer, Element> map = new HashMap<Integer, Element>();

        for (int i = 0; i < n; i++) {
            if (map.containsKey(arr[i])) {
                Element e = map.get(arr[i]);
                e.second = i;
            } else {
                Element e = new Element();
                e.first = i;
                map.put(arr[i], e);
            }

        }

        for (Map.Entry<Integer, Element> entry : map.entrySet()) {
            Element e = entry.getValue();
            if ((e.second - e.first) > maxDiffIndex)
                maxDiffIndex = e.second - e.first;
        }

        return maxDiffIndex;
    }

}        
```

## C#

```
// C# implementation to find the maximum difference 
// of first and last index of array elements 
using System;
using System.Collections.Generic;

public class MaxDiffIndexHashing 
{ 

    class Element { 
        public int first; 
        public int second; 

        public Element() { 
        } 

        public Element(int first, int second) { 
            this.first = first; 
            this.second = second; 
        } 
    } 

    public static void Main(String[] args) { 

        int []arr={2, 1, 3, 4, 2, 1, 5, 1, 7}; 
        Console.WriteLine("Maximum Difference= "+ maxDiffIndices(arr)); 
    } 

    private static int maxDiffIndices(int[] arr) { 
        int n = arr.Length; 
        int maxDiffIndex = 0; 
        Dictionary<int, Element> map = new Dictionary<int, Element>(); 

        for (int i = 0; i < n; i++) { 
            if (map.ContainsKey(arr[i])) { 
                Element e = map[arr[i]]; 
                e.second = i; 
            } else { 
                Element e = new Element(); 
                e.first = i; 
                map.Add(arr[i], e); 
            } 

        } 

        foreach(KeyValuePair<int, Element> entry in map) { 
            Element e = entry.Value; 
            if ((e.second - e.first) > maxDiffIndex) 
                maxDiffIndex = e.second - e.first; 
        } 

        return maxDiffIndex; 
    } 
}     

// This code is contributed by 29AjayKumar
```

**Output:**

```
Maximum Difference = 6

```

时间复杂度:0(n)

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。