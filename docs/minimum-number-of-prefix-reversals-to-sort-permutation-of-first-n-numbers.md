# 对前 N 个数字的排列进行排序的最小前缀反转次数

> 原文:[https://www . geeksforgeeks . org/前缀反转排序排列第一 n 个数字的最小数量/](https://www.geeksforgeeks.org/minimum-number-of-prefix-reversals-to-sort-permutation-of-first-n-numbers/)

给定前 N 个数字排列的 N 个数字。在单个操作中，任何前缀都可以反转。任务是找到此类操作的最小数量，以便数组中的数字按递增顺序排列。
**例:**

```
Input : a[] = {3, 1, 2} 
Output : 2 
Step1: Reverse the complete array a, a[] = {2, 1, 3} 
Step2: Reverse the prefix(0-1) in s, a[] = {1, 2, 3} 

Input : a[] = {1, 2, 4, 3} 
Output : 3 
Step1: Reverse the complete array a, a[] = {3, 4, 2, 1} 
Step2: Reverse the prefix(0-1) in s, a[] = {4, 3, 2, 1} 
Step3: Reverse the complete array a, a[] = {1, 2, 3, 4} 
```

解决这个问题的方法是使用 [BFS](https://www.geeksforgeeks.org/applications-of-breadth-first-traversal/) 。

*   将给定的数字编码成字符串。对数组进行排序，并将其编码为字符串*目的地*。
*   然后根据初始排列做一个 BFS。每次，检查所有由当前置换的前缀反转引起的置换。
*   如果它没有被访问，将它放入队列，并完成反转计数。
*   当编码字符串的排列与目标字符串相同时，返回到达此处所需的反转次数。
*   也就是说，字符串的所有排列都已完成，其中最小的排列作为答案返回。

以下是上述方法的实现:

## C++

```
// C++ program to find
// minimum number of prefix reversals
// to sort permutation of first N numbers
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum prefix reversals
int minimumPrefixReversals(int a[], int n)
{
    string start = "";
    string destination = "", t, r;
    for (int i = 0; i < n; i++) {
        // converts the number to a character
        // and add  to string
        start += to_string(a[i]);
    }
    sort(a, a + n);
    for (int i = 0; i < n; i++) {
        destination += to_string(a[i]);
    }

    // Queue to store the pairs
    // of string and number of reversals
    queue<pair<string, int> > qu;
    pair<string, int> p;

    // Initially push the original string
    qu.push(make_pair(start, 0));

    // if original string is the destination string
    if (start == destination) {
        return 0;
    }

    // iterate till queue is empty
    while (!qu.empty()) {

        // pair at the top
        p = qu.front();

        // string
        t = p.first;

        // pop the top-most element
        qu.pop();

        // perform prefix reversals for all index and push
        // in the queue and check for the minimal
        for (int j = 2; j <= n; j++) {
            r = t;

            // reverse the string till prefix j
            reverse(r.begin(), r.begin() + j);

            // if after reversing the string from first i index
            // it is the destination
            if (r == destination) {
                return p.second + 1;
            }

            // push the number of reversals for string r
            qu.push(make_pair(r, p.second + 1));
        }
    }
}

// Driver Code
int main()
{

    int a[] = { 1, 2, 4, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    // Calling function
    cout << minimumPrefixReversals(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of prefix reversals to
// sort permutation of first N numbers
import java.util.*;

public class Main
{

    // function to find minimum prefix reversal through BFS
    public static int minimumPrefixReversals(int[] a)
    {
        // size of array
        int n = a.length;

        // string for initial and goal nodes
        String start = "", destination = "";

        // string for manipulation in while loop
        String original = "",modified = "";

        // node to store temporary values from front of queue
        Node temp = null;

        // create the starting string
        for (int i = 0; i < n; i++)
        start += a[i];

        // sort the array and prepare final destination string
        Arrays.sort(a);
        for (int i = 0; i < n; i++)
            destination += a[i];

        // this queue will store all the BFS siblings
        Queue<Node> q = new LinkedList<>();

        // place the starting node in queue
        q.add(new Node(start, 0));

        //base case:- if array is already sorted
        if (start == destination)
            return 0;

        // loop until the size of queue is empty
        while (q.size() != 0)
        {
            // put front node of queue in temporary variable
            temp = q.poll();

            // store the original string at this step
            original = temp.string;

            for (int j = 2; j <= n; j++)
            {
                // modified will be used to generate all
                // manipulation of original string
                // like if original = 1342
                // modified = 3142 , 4312 , 2431

                modified = original;

                // generate the permutation by reversing
                modified = reverse (modified , j);

                if (modified.equals(destination))
                {
                    // if string match then return
                    // the height of the current node
                    return temp.steps + 1;
                }

                // else put this node into queue
                q.add(new Node(modified,temp.steps + 1));
            }

        }

    // if no case match then default value
    return Integer.MIN_VALUE;
    }

    // function to reverse the string upto an index
    public static String reverse (String s , int index)
    {
        char temp []= s.toCharArray();
        int i = 0;
        while (i < index)
        {
            char c = temp[i];
            temp[i] = temp[index-1];
            temp[index-1] = c;
            i++;index--;
        }
        return String.valueOf(temp);
    }

    // Driver code
    public static void main(String []args)
    {
        int a[] = new int []{1,2,4,3};
        System.out.println(minimumPrefixReversals(a));
    }

    // Node class to store a combined set of values
    static class Node
    {
        public String string ;
        public int steps;

        public Node(String string,int steps)
        {
            this.string = string;
            this.steps= steps;
        }
    }
}

// This code is contributed by Sparsh Singhal
```

## C#

```
// C# program to find minimum
// number of prefix reversals to
// sort permutation of first N numbers
using System;
using System.Collections.Generic;            

class GFG
{
    // Node class to store a combined set of values
    public class Node
    {
        public String str;
        public int steps;

        public Node(String str,int steps)
        {
            this.str = str;
            this.steps= steps;
        }
    }

    // function to find minimum prefix reversal through BFS
    public static int minimumPrefixReversals(int[] a)
    {
        // size of array
        int n = a.Length;

        // string for initial and goal nodes
        String start = "", destination = "";

        // string for manipulation in while loop
        String original = "", modified = "";

        // node to store temporary values
        // from front of queue
        Node temp = null;

        // create the starting string
        for (int i = 0; i < n; i++)
        start += a[i];

        // sort the array and prepare
        // final destination string
        Array.Sort(a);
        for (int i = 0; i < n; i++)
            destination += a[i];

        // this queue will store all the BFS siblings
        Queue<Node> q = new Queue<Node>();

        // place the starting node in queue
        q.Enqueue(new Node(start, 0));

        //base case:- if array is already sorted
        if (start == destination)
            return 0;

        // loop until the size of queue is empty
        while (q.Count != 0)
        {
            // put front node of queue in temporary variable
            temp = q.Dequeue();

            // store the original string at this step
            original = temp.str;

            for (int j = 2; j <= n; j++)
            {
                // modified will be used to generate all
                // manipulation of original string
                // like if original = 1342
                // modified = 3142 , 4312 , 2431

                modified = original;

                // generate the permutation by reversing
                modified = reverse (modified , j);

                if (modified.Equals(destination))
                {
                    // if string match then return
                    // the height of the current node
                    return temp.steps + 1;
                }

                // else put this node into queue
                q.Enqueue(new Node(modified, temp.steps + 1));
            }
        }

        // if no case match then default value
        return int.MinValue;
    }

    // function to reverse the string upto an index
    public static String reverse (String s, int index)
    {
        char []temp = s.ToCharArray();
        int i = 0;
        while (i < index)
        {
            char c = temp[i];
            temp[i] = temp[index - 1];
            temp[index - 1] = c;
            i++;index--;
        }
        return String.Join("", temp);
    }

    // Driver code
    public static void Main(String []args)
    {
        int []a = new int []{1, 2, 4, 3};
        Console.WriteLine(minimumPrefixReversals(a));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

class Node
{
    constructor(string,steps)
    {
        this.string = string;
        this.steps= steps;
    }
}

function minimumPrefixReversals(a)
{
    // size of array
        let n = a.length;

        // string for initial and goal nodes
        let start = "", destination = "";

        // string for manipulation in while loop
        let original = "",modified = "";

        // node to store temporary values from front of queue
        let temp = null;

        // create the starting string
        for (let i = 0; i < n; i++)
            start += a[i];

        // sort the array and prepare final destination string
        a.sort(function(a,b){return a-b;});
        for (let i = 0; i < n; i++)
            destination += a[i];

        // this queue will store all the BFS siblings
        let q = [];

        // place the starting node in queue
        q.push(new Node(start, 0));

        //base case:- if array is already sorted
        if (start == destination)
            return 0;

        // loop until the size of queue is empty
        while (q.length != 0)
        {
            // put front node of queue in temporary variable
            temp = q.shift();

            // store the original string at this step
            original = temp.string;

            for (let j = 2; j <= n; j++)
            {
                // modified will be used to generate all
                // manipulation of original string
                // like if original = 1342
                // modified = 3142 , 4312 , 2431

                modified = original;

                // generate the permutation by reversing
                modified = reverse (modified , j);

                if (modified == (destination))
                {
                    // if string match then return
                    // the height of the current node
                    return temp.steps + 1;
                }

                // else put this node into queue
                q.push(new Node(modified,temp.steps + 1));
            }

        }

    // if no case match then default value
    return Number.MIN_VALUE;
}

function reverse (s,index)
{
    let temp = s.split("");
        let i = 0;
        while (i < index)
        {
            let c = temp[i];
            temp[i] = temp[index-1];
            temp[index-1] = c;
            i++;index--;
        }
        return (temp).join("");
}

let a = [1, 2, 4, 3];
document.write(minimumPrefixReversals(a));

// This code is contributed by rag2127
</script>
```

## 蟒蛇 3

```
# Python3 program to find
# minimum number of prefix reversals
# to sort permutation of [0] N numbers
from queue import Queue

# Function to return the minimum prefix reversals
def minimumPrefixReversals( a,  n):
    start = ""
    destination = ""
    for i in range(n):
        # converts the number to a character
        # and add  to
        start += str(a[i])

    a.sort()
    for i in range(n):
        destination += str(a[i])

    # Queue to store the pairs
    # of  and number of reversals
    qu=Queue()

    # Initially push the original
    qu.put((start, 0))

    # if original  is the destination
    if (start == destination) :
        return 0

    # iterate till queue is empty
    while qu.not_empty :
        # pair at the top
        p = qu.get()

        #
        t = p[0]

        # perform prefix reversals for all index and push
        # in the queue and check for the minimal
        for j in range(2,n+1) :
            r = t

            # reverse the  till prefix j
            tmpR=list(r)
            tmpR[:j]=tmpR[j-1::-1]
            r=''.join(tmpR)

            # if after reversing the  from [0] i index
            # it is the destination
            if (r == destination) :
                return p[1] + 1

            # push the number of reversals for  r
            qu.put((r, p[1] + 1))

# Driver Code
if __name__ == '__main__':

    a = [ 1, 2, 4, 3]
    n = len(a)

    # Calling function
    print(minimumPrefixReversals(a, n))
```

**Output:** 

```
3
```

**时间复杂度:** O(N！* N<sup>2</sup>)
T5】辅助空间: O(N！)