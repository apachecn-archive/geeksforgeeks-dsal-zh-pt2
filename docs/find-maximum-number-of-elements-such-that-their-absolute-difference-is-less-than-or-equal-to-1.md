# 找到元素的最大数量，使其绝对差值小于或等于 1

> 原文:[https://www . geeksforgeeks . org/find-最大元素数-它们的绝对差值小于或等于 1/](https://www.geeksforgeeks.org/find-maximum-number-of-elements-such-that-their-absolute-difference-is-less-than-or-equal-to-1/)

给定 n 个元素的数组，找到要从数组中选择的元素的最大数量，使得任意两个所选元素之间的绝对差小于或等于 1。
**例**:

```
Input : arr[] = {1, 2, 3}
Output : 2
We can either take 1, 2 or 2, 3.
Both will have the count 2 so maximum count is 2

Input : arr[] = {2, 2, 3, 4, 5}
Output : 3
The sequence with maximum count is 2, 2, 3.
```

0 或 1 的绝对差意味着选择的数字可以是 x 和 x+1 类型。因此，其思想是存储数组元素的频率。因此，任务现在简化为寻找任意两个连续元素的最大和。
下面是上述方法的实现:

## C++

```
// CPP program to find maximum number of
// elements such that their absolute
// difference is less than or equal to 1
#include <bits/stdc++.h>
using namespace std;

// function to return maximum number of elements
int maxCount(int n,int a[])
{
    // Counting frequencies of elements
    map<int,int> freq;

    for(int i=0;i<n;++i){
        if(freq[a[i]])
            freq[a[i]] += 1;
        else
            freq[a[i]] = 1;
    }

    // Finding max sum of adjacent indices
    int ans = 0, key;

    map<int,int>:: iterator it=freq.begin();

    while(it!=freq.end())
    {
        key = it->first;

        // increment the iterator
        ++it;

        if(freq[key+1]!=0)
            ans=max(ans,freq[key]+freq[key+1]);

    }

    return ans;
}

// Driver Code
int main(){
    int n = 5;
    int arr[] = {2, 2, 3, 4, 5};

    // function call to print required answer
    cout<<maxCount(n,arr);

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum number
// of elements such that their absolute
// difference is less than or equal to 1
import java.util.HashMap;
import java.util.Map;
import java.lang.Math;

class GfG
{

    // function to return the maximum number of elements
    static int maxCount(int n,int a[])
    {
        // Counting frequencies of elements
        HashMap<Integer, Integer> freq = new HashMap<>();

        for(int i = 0; i < n; ++i)
        {
            if(freq.containsKey(a[i]))
                freq.put(a[i], freq.get(a[i]) + 1);
            else
                freq.put(a[i], 1);
        }

        // Finding max sum of adjacent indices
        int ans = 0;

        for (Integer key : freq.keySet())
        {
            if(freq.containsKey(key+1))
                ans = Math.max(ans, freq.get(key) + freq.get(key+1));
        }

        return ans;
    }

    // Driver code
    public static void main(String []args)
    {

        int n = 5;
        int arr[] = {2, 2, 3, 4, 5};

        // function call to print required answer
        System.out.println(maxCount(n,arr));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python program to find maximum number of
# elements such that their absolute
# difference is less than or equal to 1

def maxCount(a):

    # Counting frequencies of elements
    freq = {}
    for i in range(n):
        if (a[i] in freq):
            freq[a[i]] += 1
        else:
            freq[a[i]] = 1

    # Finding max sum of adjacent indices   
    ans = 0
    for key, value in freq.items():
        if (key+1 in freq) :   
            ans = max(ans, freq[key] + freq[key + 1])

    return ans

# Driver Code
n = 5
arr = [2, 2, 3, 4, 5]

print(maxCount(arr))
```

## C#

```
// C# program to find the maximum number
// of elements such that their absolute
// difference is less than or equal to 1
using System;
using System.Collections.Generic;

class GfG
{

    // function to return the maximum number of elements
    static int maxCount(int n,int []a)
    {
        // Counting frequencies of elements
        Dictionary<int,int> mp = new Dictionary<int,int>();

        // Increase the frequency of elements
        for (int i = 0 ; i < n; i++)
        {
            if(mp.ContainsKey(a[i]))
            {
                var val = mp[a[i]];
                mp.Remove(a[i]);
                mp.Add(a[i], val + 1);
            }
            else
            {
                mp.Add(a[i], 1);
            }
        }

        // Finding max sum of adjacent indices
        int ans = 0;

        foreach(KeyValuePair<int, int> e in mp)
        {
            if(mp.ContainsKey(e.Key+1))
                ans = Math.Max(ans, mp[e.Key] + mp[e.Key+1]);
        }

        return ans;
    }

    // Driver code
    public static void Main(String []args)
    {

        int n = 5;
        int []arr = {2, 2, 3, 4, 5};

        // function call to print required answer
        Console.WriteLine(maxCount(n,arr));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to find maximum number of
// elements such that their absolute
// difference is less than or equal to 1

// function to return maximum number of elements
function maxCount(n,a)
{
    // Counting frequencies of elements
    var freq = new Map();

    for(var i=0;i<n;++i){
        if(freq.has(a[i]))
            freq.set(a[i], freq.get(a[i])+1)
        else
            freq.set(a[i], 1)
    }

    // Finding max sum of adjacent indices
    var ans = 0, key;

    freq.forEach((value, key) => {

        if(freq.has(key+1))
            ans=Math.max(ans,freq.get(key)+freq.get(key+1));
    });

    return ans;
}

// Driver Code

var n = 5;
var arr =  [2, 2, 3, 4, 5];

// function call to print required answer
document.write( maxCount(n,arr));

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(n * log(n))*

***辅助空间:** O(n)*