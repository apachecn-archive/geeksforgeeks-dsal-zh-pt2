# 为使每个字符的频率唯一，需要删除的最少字符数

> 原文:[https://www . geeksforgeeks . org/最小字符-需要删除以使每个字符的频率唯一/](https://www.geeksforgeeks.org/minimum-characters-required-to-be-removed-to-make-frequency-of-each-character-unique/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是找到需要从字符串中删除的最小字符数，使得字符串中每个字符的[频率是唯一的。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)

**示例:**

> **输入:** str = "ceabaacb"
> **输出:** 2
> **解释:**
> 每个不同字符的频率如下:
> c—>2
> e—>1
> a—>3
> b—>2
> 通过最小移动次数使每个字符的频率唯一的可能方法有:
> 
> *   删除两次出现的**‘c’**将字符串修改为“eabaab”
> *   删除出现的**‘c’**和**‘e’**将 str 改为“abaacb”
> 
> 因此，所需的最小清除量为 2。
> 
> **输入:**S = " abbcccd "
> T3】输出: 2

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。想法是使用[地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)和[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)，比如 **mp** ，以[存储字符串](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)的每个不同字符的频率。
*   初始化一个变量，比如 **cntChar** 来存储需要删除的字符数，以使字符串中每个字符的频率唯一。
*   创建一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，比如说 **pq** 来存储每个字符的频率，使得获得的最大频率出现在优先级队列 **pq** 的[顶端。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
*   [遍历 priority_queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) 直到 **pq** 为空，检查 **pq** 元素的[最顶端是否等于 **pq** 的第二个最顶端元素。如果发现为真，则将 **pq** 最顶端元素的值递减 **1** ，将 **cntChar** 的值递增 **1** 。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
*   否则，[弹出 pq 最上面的元素](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)。
*   最后打印 **cntChar** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of
// characters required to be deleted to make
// frequencies of all characters unique
int minCntCharDeletionsfrequency(string& str,
                                 int N)
{
    // Stores frequency of each
    // distinct character of str
    unordered_map<char, int> mp;

    // Store frequency of each distinct
    // character such that the largest
    // frequency is present at the top
    priority_queue<int> pq;

    // Stores minimum count of characters
    // required to be deleted to make
    // frequency of each character unique
    int cntChar = 0;

    // Traverse the string
    for (int i = 0; i < N; i++) {

        // Update frequency of str[i]
        mp[str[i]]++;
    }

    // Traverse the map
    for (auto it : mp) {

        // Insert current
        // frequency into pq
        pq.push(it.second);
    }

    // Traverse the priority_queue
    while (!pq.empty()) {

        // Stores topmost
        // element of pq
        int frequent
            = pq.top();

        // Pop the topmost element
        pq.pop();

        // If pq is empty
        if (pq.empty()) {

            // Return cntChar
            return cntChar;
        }

        // If frequent and topmost
        // element of pq are equal
        if (frequent == pq.top()) {

            // If frequency of the topmost
            // element is greater than 1
            if (frequent > 1) {

                // Insert the decremented
                // value of frequent
                pq.push(frequent - 1);
            }

            // Update cntChar
            cntChar++;
        }
    }

    return cntChar;
}

// Driver Code
int main()
{

    string str = "abbbcccd";

    // Stores length of str
    int N = str.length();
    cout << minCntCharDeletionsfrequency(
        str, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the minimum count of
// characters required to be deleted to make
// frequencies of all characters unique
static int minCntCharDeletionsfrequency(char[] str,
                                        int N)
{
  // Stores frequency of each
  // distinct character of str
  HashMap<Character,
          Integer> mp =
          new HashMap<>();

  // Store frequency of each distinct
  // character such that the largest
  // frequency is present at the top
  PriorityQueue<Integer> pq =
          new PriorityQueue<>((x, y) ->
          Integer.compare(y, x));

  // Stores minimum count of characters
  // required to be deleted to make
  // frequency of each character unique
  int cntChar = 0;

  // Traverse the String
  for (int i = 0; i < N; i++)
  {
    // Update frequency of str[i]
    if(mp.containsKey(str[i]))
    {
      mp.put(str[i],
      mp.get(str[i]) + 1);
    }
    else
    {
      mp.put(str[i], 1);
    }
  }

  // Traverse the map
  for (Map.Entry<Character,
                 Integer> it :
                 mp.entrySet())
  {
    // Insert current
    // frequency into pq
    pq.add(it.getValue());
  }

  // Traverse the priority_queue
  while (!pq.isEmpty())
  {
    // Stores topmost
    // element of pq
    int frequent = pq.peek();

    // Pop the topmost element
    pq.remove();

    // If pq is empty
    if (pq.isEmpty()) {

      // Return cntChar
      return cntChar;
    }

    // If frequent and topmost
    // element of pq are equal
    if (frequent == pq.peek())
    {
      // If frequency of the topmost
      // element is greater than 1
      if (frequent > 1)
      {
        // Insert the decremented
        // value of frequent
        pq.add(frequent - 1);
      }

      // Update cntChar
      cntChar++;
    }
  }

  return cntChar;
}

// Driver Code
public static void main(String[] args)
{
  String str = "abbbcccd";

  // Stores length of str
  int N = str.length();
  System.out.print(minCntCharDeletionsfrequency(
         str.toCharArray(), N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum count of
# characters required to be deleted to make
# frequencies of all characters unique
def minCntCharDeletionsfrequency(str, N):

    # Stores frequency of each
    # distinct character of str
    mp = {}

    # Store frequency of each distinct
    # character such that the largest
    # frequency is present at the top
    pq = []

    # Stores minimum count of characters
    # required to be deleted to make
    # frequency of each character unique
    cntChar = 0

    # Traverse the string
    for i in range(N):

        # Update frequency of str[i]
        mp[str[i]] = mp.get(str[i], 0) + 1

    # Traverse the map
    for it in mp:

        # Insert current
        # frequency into pq
        pq.append(mp[it])

    pq = sorted(pq)

    # Traverse the priority_queue
    while (len(pq) > 0):

        # Stores topmost
        # element of pq
        frequent = pq[-1]

        # Pop the topmost element
        del pq[-1]

        # If pq is empty
        if (len(pq) == 0):

            # Return cntChar
            return cntChar

        # If frequent and topmost
        # element of pq are equal
        if (frequent == pq[-1]):

            # If frequency of the topmost
            # element is greater than 1
            if (frequent > 1):

                # Insert the decremented
                # value of frequent
                pq.append(frequent - 1)

            # Update cntChar
            cntChar += 1

        pq = sorted(pq)

    return cntChar

# Driver Code
if __name__ == '__main__':

    str = "abbbcccd"

    # Stores length of str
    N = len(str)

    print(minCntCharDeletionsfrequency(str, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum count of
// characters required to be deleted to make
// frequencies of all characters unique
static int minCntCharDeletionsfrequency(char[] str,
                                        int N)
{

    // Stores frequency of each
    // distinct character of str
    Dictionary<char,
               int> mp = new Dictionary<char,
                                        int>();

    // Store frequency of each distinct
    // character such that the largest
    // frequency is present at the top
    List<int> pq = new List<int>();

    // Stores minimum count of characters
    // required to be deleted to make
    // frequency of each character unique
    int cntChar = 0;

    // Traverse the String
    for(int i = 0; i < N; i++)
    {

        // Update frequency of str[i]
        if (mp.ContainsKey(str[i]))
        {
            mp[str[i]]++;
        }
        else
        {
            mp.Add(str[i], 1);
        }
    }

    // Traverse the map
    foreach(KeyValuePair<char, int> it in mp)
    {

        // Insert current
        // frequency into pq
        pq.Add(it.Value);
    }
    pq.Sort();
    pq.Reverse();

    // Traverse the priority_queue
    while (pq.Count != 0)
    {

        // Stores topmost
        // element of pq
        pq.Sort();
        pq.Reverse();
        int frequent = pq[0];

        // Pop the topmost element
        pq.RemoveAt(0);

        // If pq is empty
        if (pq.Count == 0)
        {

            // Return cntChar
            return cntChar;
        }

        // If frequent and topmost
        // element of pq are equal
        if (frequent == pq[0])
        {

            // If frequency of the topmost
            // element is greater than 1
            if (frequent > 1)
            {

                // Insert the decremented
                // value of frequent
                pq.Add(frequent - 1);
                pq.Sort();
                // pq.Reverse();
            }

            // Update cntChar
            cntChar++;
        }
    }
    return cntChar;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "abbbcccd";

    // Stores length of str
    int N = str.Length;

    Console.Write(minCntCharDeletionsfrequency(
        str.ToCharArray(), N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the minimum count of
// characters required to be deleted to make
// frequencies of all characters unique
function minCntCharDeletionsfrequency(str,N)
{
    // Stores frequency of each
  // distinct character of str
  let mp = new Map();

  // Store frequency of each distinct
  // character such that the largest
  // frequency is present at the top
  let pq =[];

  // Stores minimum count of characters
  // required to be deleted to make
  // frequency of each character unique
  let cntChar = 0;

  // Traverse the String
  for (let i = 0; i < N; i++)
  {
    // Update frequency of str[i]
    if(mp.has(str[i]))
    {
      mp.set(str[i],
      mp.get(str[i]) + 1);
    }
    else
    {
      mp.set(str[i], 1);
    }
  }

  // Traverse the map
  for (let [key, value] of mp.entries())
  {
    // Insert current
    // frequency into pq
    pq.push(value);
  }

 pq.sort(function(a,b){return b-a;});

  // Traverse the priority_queue
  while (pq.length!=0)
  {
    // Stores topmost
    // element of pq
    let frequent = pq[0];

    // Pop the topmost element
    pq.shift();

    // If pq is empty
    if (pq.length==0) {

      // Return cntChar
      return cntChar;
    }

    // If frequent and topmost
    // element of pq are equal
    if (frequent == pq[0])
    {
      // If frequency of the topmost
      // element is greater than 1
      if (frequent > 1)
      {
        // Insert the decremented
        // value of frequent
        pq.push(frequent - 1);
        pq.sort(function(a,b){return b-a;});
      }

      // Update cntChar
      cntChar++;
    }
  }

  return cntChar;
}

// Driver Code
let str = "abbbcccd";
let N = str.length;
document.write(minCntCharDeletionsfrequency(
         str.split(""), N));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(256)