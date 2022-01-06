# 两个列表公共元素的最小指数和

> 原文:[https://www . geesforgeks . org/minimum-index-sum-common-elements-two-list/](https://www.geeksforgeeks.org/minimum-index-sum-common-elements-two-lists/)

拉姆和希亚姆想选择一个网站学习编程，他们都有一个用字符串表示的最喜欢的网站列表。
你需要用最少的指标和帮助他们找出共同的兴趣。如果答案之间有选择关系，打印所有答案，不需要订单。假设总有一个答案。

**示例:**

```
Input : ["GeeksforGeeks", "Udemy", "Coursera", "edX"]
        ["Codecademy", "Khan Academy", "GeeksforGeeks"]
Output : "GeeksforGeeks"
Explanation : GeeksforGeeks is the only common website 
              in two lists

Input : ["Udemy", "GeeksforGeeks", "Coursera", "edX"]
        ["GeeksforGeeks", "Udemy", "Khan Academy", "Udacity"]
Output : "GeeksforGeeks" "Udemy"
Explanation : There are two common websites and index sum
              of both is same.
```

**天真法:**

想法是尝试从 0 到大小总和的所有索引总和。对于每个和，检查是否有给定和的对。一旦我们找到一对或多对，我们就打印它们并返回。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to print common strings with minimum index sum
void find(vector<string> list1, vector<string> list2)
{
    vector<string> res; // resultant list
    int max_possible_sum = list1.size() + list2.size() - 2;

    // iterating over sum in ascending order
    for (int sum = 0; sum <= max_possible_sum ; sum++)
    {
        // iterating over one list and check index
        // (Corresponding to given sum) in other list
        for (int i = 0; i <= sum; i++)

            // put common strings in resultant list 
            if (i < list1.size() &&
                (sum - i) < list2.size() &&
                list1[i] == list2[sum - i])
                res.push_back(list1[i]);        

        // if common string found then break as we are
        // considering index sums in increasing order.
        if (res.size() > 0)
            break;
    }

    // print the resultant list
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
}

// Driver code
int main()
{
    // Creating list1
    vector<string> list1;
    list1.push_back("GeeksforGeeks");
    list1.push_back("Udemy");
    list1.push_back("Coursera");
    list1.push_back("edX");

    // Creating list2
    vector<string> list2;
    list2.push_back("Codecademy");
    list2.push_back("Khan Academy");
    list2.push_back("GeeksforGeeks");

    find(list1, list2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG
{

// Function to print common Strings with minimum index sum
static void find(Vector<String> list1, Vector<String> list2)
{
    Vector<String> res = new Vector<>(); // resultant list
    int max_possible_sum = list1.size() + list2.size() - 2;

    // iterating over sum in ascending order
    for (int sum = 0; sum <= max_possible_sum ; sum++)
    {
        // iterating over one list and check index
        // (Corresponding to given sum) in other list
        for (int i = 0; i <= sum; i++)

            // put common Strings in resultant list
            if (i < list1.size() &&
                (sum - i) < list2.size() &&
                list1.get(i) == list2.get(sum - i))
                res.add(list1.get(i));        

        // if common String found then break as we are
        // considering index sums in increasing order.
        if (res.size() > 0)
            break;
    }

    // print the resultant list
    for (int i = 0; i < res.size(); i++)
        System.out.print(res.get(i)+" ");
}

// Driver code
public static void main(String[] args)
{
    // Creating list1
    Vector<String> list1 = new Vector<>();
    list1.add("GeeksforGeeks");
    list1.add("Udemy");
    list1.add("Coursera");
    list1.add("edX");

    // Creating list2
    Vector<String> list2= new Vector<>();
    list2.add("Codecademy");
    list2.add("Khan Academy");
    list2.add("GeeksforGeeks");

    find(list1, list2);

}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Function to print common strings
# with minimum index sum
def find(list1, list2):
    res = [] # resultant list
    max_possible_sum = len(list1) + len(list2) - 2

    # iterating over sum in ascending order
    for sum in range(max_possible_sum + 1):

        # iterating over one list and check index
        # (Corresponding to given sum) in other list
        for i in range(sum + 1):

            # put common strings in resultant list
            if (i < len(list1) and
               (sum - i) < len(list2) and
                list1[i] == list2[sum - i]):
                res.append(list1[i])

        # if common string found then break as we are
        # considering index sums in increasing order.
        if (len(res) > 0):
            break

    # print the resultant list
    for i in range(len(res)):
        print(res[i], end = " ")

# Driver code

# Creating list1
list1 = []
list1.append("GeeksforGeeks")
list1.append("Udemy")
list1.append("Coursera")
list1.append("edX")

# Creating list2
list2 = []
list2.append("Codecademy")
list2.append("Khan Academy")
list2.append("GeeksforGeeks")

find(list1, list2)

# This code is contributed by Mohit Kumar
```

## C#

```
using System;
using System.Collections.Generic;

class GFG
{

// Function to print common Strings with minimum index sum
static void find(List<String> list1, List<String> list2)
{
    List<String> res = new List<String>(); // resultant list
    int max_possible_sum = list1.Count + list2.Count - 2;

    // iterating over sum in ascending order
    for (int sum = 0; sum <= max_possible_sum ; sum++)
    {
        // iterating over one list and check index
        // (Corresponding to given sum) in other list
        for (int i = 0; i <= sum; i++)

            // put common Strings in resultant list
            if (i < list1.Count &&
                (sum - i) < list2.Count &&
                list1[i] == list2[sum - i])
                res.Add(list1[i]);

        // if common String found then break as we are
        // considering index sums in increasing order.
        if (res.Count > 0)
            break;
    }

    // print the resultant list
    for (int i = 0; i < res.Count; i++)
        Console.Write(res[i]+" ");
}

// Driver code
public static void Main(String[] args)
{
    // Creating list1
    List<String> list1 = new List<String>();
    list1.Add("GeeksforGeeks");
    list1.Add("Udemy");
    list1.Add("Coursera");
    list1.Add("edX");

    // Creating list2
    List<String> list2= new List<String>();
    list2.Add("Codecademy");
    list2.Add("Khan Academy");
    list2.Add("GeeksforGeeks");

    find(list1, list2);

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Function to print common Strings with minimum index sum
    function find(list1, list2)
    {
        let res = []; // resultant list
        let max_possible_sum = list1.length + list2.length - 2;

        // iterating over sum in ascending order
        for (let sum = 0; sum <= max_possible_sum ; sum++)
        {
            // iterating over one list and check index
            // (Corresponding to given sum) in other list
            for (let i = 0; i <= sum; i++)

                // put common Strings in resultant list
                if (i < list1.length &&
                    (sum - i) < list2.length &&
                    list1[i] == list2[sum - i])
                    res.push(list1[i]);

            // if common String found then break as we are
            // considering index sums in increasing order.
            if (res.length > 0)
                break;
        }

        // print the resultant list
        for (let i = 0; i < res.length; i++)
            document.write(res[i]+" ");
    }

    // Creating list1
    let list1 = [];
    list1.push("GeeksforGeeks");
    list1.push("Udemy");
    list1.push("Coursera");
    list1.push("edX");

    // Creating list2
    let list2= [];
    list2.push("Codecademy");
    list2.push("Khan Academy");
    list2.push("GeeksforGeeks");

    find(list1, list2);

// This code is contributed by mukesh07.
</script>
```

**输出:**

```
GeeksforGeeks
```

**时间复杂度:**O((l<sub>1</sub>+l<sub>2</sub>)<sup>2</sup>* x)，其中 l <sub>1</sub> 和 l <sub>2</sub> 分别为 list1 和 list2 的长度，x 为字符串长度。
**辅助空格:** O(l*x)，其中 x 为结果列表长度，l 为最大大小字长度。

**使用哈希:**

1.  遍历列表 1，为哈希表中列表 1 的每个元素创建一个索引条目。
2.  遍历列表 2，对于每个元素，检查相同的元素是否已经作为关键字存在于地图中。如果是，这意味着该元素存在于两个列表中。
3.  找出两个列表中公共元素对应的索引之和。如果该总和小于迄今为止获得的最小总和，则更新结果列表。
4.  如果总和等于到目前为止获得的最小总和，则在结果列表中添加一个对应于列表 2 中元素的额外条目。

## C++

```
// Hashing based C++ program to find common elements
// with minimum index sum.
#include <bits/stdc++.h>
using namespace std;

// Function to print common strings with minimum index sum
void find(vector<string> list1, vector<string> list2)
{
    // mapping strings to their indices
    unordered_map<string, int> map;
    for (int i = 0; i < list1.size(); i++)
        map[list1[i]] = i;

    vector<string> res; // resultant list

    int minsum = INT_MAX;
    for (int j = 0; j < list2.size(); j++)
    {
        if (map.count(list2[j]))
        {
            // If current sum is smaller than minsum
            int sum = j + map[list2[j]];
            if (sum < minsum)
            {
                minsum = sum;
                res.clear();
                res.push_back(list2[j]);
            }

            // if index sum is same then put this
            // string in resultant list as well 
            else if (sum == minsum)
                res.push_back(list2[j]);
        }
    }

    // Print result
    for (int i = 0; i < res.size(); i++)
        cout << res[i] << " ";
}

// Driver code
int main()
{
    // Creating list1
    vector<string> list1;
    list1.push_back("GeeksforGeeks");
    list1.push_back("Udemy");
    list1.push_back("Coursera");
    list1.push_back("edX");

    // Creating list2
    vector<string> list2;
    list2.push_back("Codecademy");
    list2.push_back("Khan Academy");
    list2.push_back("GeeksforGeeks");

    find(list1, list2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Hashing based Java program to find common elements
// with minimum index sum.
import java.util.*;

class GFG
{

    // Function to print common Strings with minimum index sum
    static void find(Vector<String> list1, Vector<String> list2)
    {
        // mapping Strings to their indices
        Map<String, Integer> map = new HashMap<>();
        for (int i = 0; i < list1.size(); i++)
            map.put(list1.get(i), i);

        Vector<String> res = new Vector<String>(); // resultant list

        int minsum = Integer.MAX_VALUE;
        for (int j = 0; j < list2.size(); j++)
        {
            if (map.containsKey(list2.get(j)))
            {
                // If current sum is smaller than minsum
                int sum = j + map.get(list2.get(j));
                if (sum < minsum)
                {
                    minsum = sum;
                    res.clear();
                    res.add(list2.get(j));
                }

                // if index sum is same then put this
                // String in resultant list as well
                else if (sum == minsum)
                    res.add(list2.get(j));
            }
        }

        // Print result
        for (int i = 0; i < res.size(); i++)
            System.out.print(res.get(i) + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        // Creating list1
        Vector<String> list1 = new Vector<String>();
        list1.add("GeeksforGeeks");
        list1.add("Udemy");
        list1.add("Coursera");
        list1.add("edX");

        // Creating list2
        Vector<String> list2 = new Vector<String>();
        list2.add("Codecademy");
        list2.add("Khan Academy");
        list2.add("GeeksforGeeks");

        find(list1, list2);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Hashing based Python3 program to find
# common elements with minimum index sum
import sys

# Function to print common strings
# with minimum index sum
def find(list1, list2):

    # Mapping strings to their indices
    Map = {}
    for i in range(len(list1)):
        Map[list1[i]] = i

    # Resultant list
    res = []

    minsum = sys.maxsize

    for j in range(len(list2)):
        if list2[j] in Map:

            # If current sum is smaller
            # than minsum
            Sum = j + Map[list2[j]]

            if (Sum < minsum):
                minsum = Sum
                res.clear()
                res.append(list2[j])

            # If index sum is same then put this 
            # string in resultant list as well  
            elif (Sum == minsum):
                res.append(list2[j])

    # Print result
    print(*res, sep = " ")

# Driver code

# Creating list1
list1 = []
list1.append("GeeksforGeeks")
list1.append("Udemy")
list1.append("Coursera")
list1.append("edX")

# Creating list2
list2 = []
list2.append("Codecademy")
list2.append("Khan Academy")
list2.append("GeeksforGeeks")
find(list1, list2)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// Hashing based C# program to find common elements
// with minimum index sum.
using System;
using System.Collections.Generic;

class GFG
{

    // Function to print common Strings with minimum index sum
    static void find(List<String> list1, List<String> list2)
    {
        // mapping Strings to their indices
        Dictionary<String, int> map = new Dictionary<String, int>();
        for (int i = 0; i < list1.Count; i++)
            map.Add(list1[i], i);

        List<String> res = new List<String>(); // resultant list

        int minsum = int.MaxValue;
        for (int j = 0; j < list2.Count; j++)
        {
            if (map.ContainsKey(list2[j]))
            {
                // If current sum is smaller than minsum
                int sum = j + map[list2[j]];
                if (sum < minsum)
                {
                    minsum = sum;
                    res.Clear();
                    res.Add(list2[j]);
                }

                // if index sum is same then put this
                // String in resultant list as well
                else if (sum == minsum)
                    res.Add(list2[j]);
            }
        }

        // Print result
        for (int i = 0; i < res.Count; i++)
            Console.Write(res[i] + " ");
    }

    // Driver code
    public static void Main(String[] args)
    {
        // Creating list1
        List<String> list1 = new List<String>();
        list1.Add("GeeksforGeeks");
        list1.Add("Udemy");
        list1.Add("Coursera");
        list1.Add("edX");

        // Creating list2
        List<String> list2 = new List<String>();
        list2.Add("Codecademy");
        list2.Add("Khan Academy");
        list2.Add("GeeksforGeeks");

        find(list1, list2);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Hashing based Javascript program to
// find common elements with minimum
// index sum.

// Function to print common Strings
// with minimum index sum
function find(list1, list2)
{

    // Mapping Strings to their indices
    let map = new Map();
    for(let i = 0; i < list1.length; i++)
        map.set(list1[i], i);

    // Resultant list
    let res = [];

    let minsum = Number.MAX_VALUE;
    for(let j = 0; j < list2.length; j++)
    {
        if (map.has(list2[j]))
        {

            // If current sum is smaller than minsum
            let sum = j + map.get(list2[j]);
            if (sum < minsum)
            {
                minsum = sum;
                res = [];
                res.push(list2[j]);
            }

            // If index sum is same then put this
            // String in resultant list as well
            else if (sum == minsum)
                res.push(list2[j]);
        }
    }

    // Print result
    for(let i = 0; i < res.length; i++)
        document.write(res[i] + " ");
}

// Driver code

// Creating list1
let list1 = [];
list1.push("GeeksforGeeks");
list1.push("Udemy");
list1.push("Coursera");
list1.push("edX");

// Creating list2
let list2 = [];
list2.push("Codecademy");
list2.push("Khan Academy");
list2.push("GeeksforGeeks");

find(list1, list2);

// This code is contributed by rameshtravel07

</script>
```

**输出:**

```
GeeksforGeeks
```

**时间复杂度:** O(l <sub>1</sub> +l <sub>2</sub> ，其中 l <sub>1</sub> 和 l <sub>2</sub> 分别为 list1 和 list2 的长度。
**辅助空格:** O(l <sub>1</sub> *x)，其中 x 为结果列表长度，l 为最大大小字长度。

本文由 **Aakash Pal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。