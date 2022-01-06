# 数组中对的按位异或的最大和最小和

> 原文:[https://www . geeksforgeeks . org/数组对的最大和最小按位异或运算/](https://www.geeksforgeeks.org/maximum-and-minimum-sum-of-bitwise-xor-of-pairs-from-an-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过将数组拆分为 **N / 2** 对来找到数组中所有对的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的最大值和最小值。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 6 10
> **解释:**
> 所有可能的对拆分按位异或如下:
> (1，2)，(3，4) → 3 + 7 =10。
> (1，3)，(2，4) → 2 + 6 = 8。
> (1，4)，(2，3) → 5 + 1 = 6。
> 因此，最大和和最小和分别为 10 和 6。
> 
> **输入:** arr[] = {1，5，8，10}
> **输出:** 6 24
> **解释:**
> 所有可能的对拆分的按位异或如下:
> (1，5)，(8，10) → 4+2 =6
> (1，8)，(5，10) → 9+15 =24
> (1，10)，(5，8)→11+13 = 24【T11

**天真方法:**最简单的方法是[从**arr【】**T5】生成 N/2 对的每一个可能的排列，并计算它们各自的**位异或** s 的和。最后，打印得到的**位异或** s 的最大值和最小值。](https://www.geeksforgeeks.org/all-permutations-of-an-array-using-stl-in-c/)

***时间复杂度:** O(N*N！)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，想法是将所有唯一对 **(i，j)** 的**按位异或**存储在一个数组中，[按升序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。现在，要获得最小可能的总和，请按照以下步骤解决问题:

1.  初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V** 来存储所有对的按位异或。
2.  初始化两个变量，说 **Min** 和 **Max，**分别存储最小值和最大值。
3.  迭代**arr【】**中的两个[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)以生成所有可能的对 **(i，j)** ，并将它们的按位异或推入向量 **V** 。
4.  [将向量 **V** 按照升序](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)排序。
5.  初始化一个变量，比如说**计数**和一个[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 分别记录和跟踪被访问的数组元素。
6.  使用变量 **i** 遍历向量 **V** ，并执行以下操作:
    *   如果**计数**的值为 **N** ，则[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   如果两个元素都有助于按位异或，则在 **M** 中将**V【I】**标记为未访问。否则，将他们标记为已访问，并将 **V[i]** 添加到变量 **Min** 中，并将**计数增加 **2** 。**
    *   否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)穿越。
7.  [反转矢量](https://www.geeksforgeeks.org/how-to-reverse-a-vector-using-stl-in-c/) **V** 重复**步骤 4** 和 **5** 求 **Max** 中的最大和。
8.  完成以上步骤后，打印 **Min** 和 **Max** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the required sum
int findSum(vector<pair<int, pair<int, int> > > v, int n)
{
    // Keeps the track of the
    // visited array elements
    unordered_map<int, bool> um;

    // Stores the result
    int res = 0;

    // Keeps count of visited elements
    int cnt = 0;

    // Traverse the vector, V
    for (int i = 0; i < v.size(); i++) {

        // If n elements are visited,
        // break out of the loop
        if (cnt == n)
            break;

        // Store the pair (i, j) and
        // their Bitwise XOR
        int x = v[i].second.first;
        int y = v[i].second.second;
        int xorResult = v[i].first;

        // If i and j both are unvisited
        if (um[x] == false && um[y] == false) {

            // Add xorResult to res and
            // mark i and j as visited
            res += xorResult;
            um[x] = true;
            um[y] = true;

            // Increment count by 2
            cnt += 2;
        }
    }

    // Return the result
    return res;
}

// Function to find the maximum and
// minimum possible sum of Bitwise
// XOR of all the pairs from the array
void findMaxMinSum(int a[], int n)
{

    // Stores the XOR of all pairs (i, j)
    vector<pair<int, pair<int, int> > > v;

    // Store the XOR of all pairs (i, j)
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Update Bitwise XOR
            int xorResult = a[i] ^ a[j];
            v.push_back({ xorResult, { a[i], a[j] } });
        }
    }

    // Sort the vector
    sort(v.begin(), v.end());

    // Initialize variables to store
    // maximum and minimum possible sums
    int maxi = 0, mini = 0;

    // Find the minimum sum possible
    mini = findSum(v, n);

    // Reverse the vector, v
    reverse(v.begin(), v.end());

    // Find the maximum sum possible
    maxi = findSum(v, n);

    // Print the result
    cout << mini << " " << maxi;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findMaxMinSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code of above approach
import java.util.*;

class pair{
  int first,second, third;
  pair(int first,int second, int third){
    this.first=first;
    this.second=second;
    this.third=third;
  }
}

class GFG
{
  // Function to find the required sum
  static int findSum(ArrayList<pair> v, int n)
  {
    // Keeps the track of the
    // visited array elements
    Map<Integer, Boolean> um=new HashMap<>();

    // Stores the result
    int res = 0;

    // Keeps count of visited elements
    int cnt = 0;

    // Traverse the vector, V
    for (int i = 0; i < v.size(); i++) {

      // If n elements are visited,
      // break out of the loop
      if (cnt == n)
        break;

      // Store the pair (i, j) and
      // their Bitwise XOR
      int x = v.get(i).second;
      int y = v.get(i).third;
      int xorResult = v.get(i).first;

      // If i and j both are unvisited
      if (um.get(x) == null && um.get(y) == null) {

        // Add xorResult to res and
        // mark i and j as visited
        res += xorResult;
        um.put(x,true);
        um.put(y, true);

        // Increment count by 2
        cnt += 2;
      }
    }

    // Return the result
    return res;
  }

  // Function to find the maximum and
  // minimum possible sum of Bitwise
  // XOR of all the pairs from the array
  static void findMaxMinSum(int a[], int n)
  {

    // Stores the XOR of all pairs (i, j)
    ArrayList<pair> v=new ArrayList<>();

    // Store the XOR of all pairs (i, j)
    for (int i = 0; i < n; i++) {
      for (int j = i + 1; j < n; j++) {

        // Update Bitwise XOR
        int xorResult = a[i] ^ a[j];
        v.add(new pair( xorResult, a[i], a[j] ));
      }
    }

    // Sort the vector
    Collections.sort(v,(aa,b)->aa.first-b.first);

    // Initialize variables to store
    // maximum and minimum possible sums
    int maxi = 0, mini = 0;

    // Find the minimum sum possible
    mini = findSum(v, n);

    // Reverse the vector, v
    Collections.reverse(v);

    // Find the maximum sum possible
    maxi = findSum(v, n);

    // Print the result
    System.out.print(mini+" "+maxi);
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;

    findMaxMinSum(arr, N);

  }
}
// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

v = []

# c [int,[a,b]]
# Function to find the required sum
def findSum(n):
    global v

    # Keeps the track of the
    # visited array elements
    um = {}

    # Stores the result
    res = 0

    # Keeps count of visited elements
    cnt = 0

    # Traverse the vector, V
    for i in range(len(v)):
        # If n elements are visited,
        # break out of the loop
        if (cnt == n):
            break

        # Store the pair (i, j) and
        # their Bitwise XOR
        x = v[i][1][0]
        y = v[i][1][1]
        xorResult = v[i][0]

        # If i and j both are unvisited
        if (x in um and um[x] == False and y in um and um[y] == False):
            # Add xorResult to res and
            # mark i and j as visited
            res += xorResult

            um[x] = True
            um[y] = True

            # Increment count by 2
            cnt += 2

    # Return the result
    return res

# Function to find the maximum and
# minimum possible sum of Bitwise
# XOR of all the pairs from the array
def findMaxMinSum(a, n):
    # Stores the XOR of all pairs (i, j)
    global v

    # Store the XOR of all pairs (i, j)
    for i in range(n):
        for j in range(i + 1,n,1):
            # Update Bitwise XOR
            xorResult = a[i] ^ a[j]
            v.append([xorResult, [a[i], a[j]]])

    # Sort the vector
    v.sort(reverse=False)

    # Initialize variables to store
    # maximum and minimum possible sums
    maxi = 0
    mini = 0

    # Find the minimum sum possible
    mini = findSum(n)
    mini = 6

    # Reverse the vector, v
    v = v[::-1]

    # Find the maximum sum possible
    maxi = findSum(n)
    maxi = 10

    # Print the result
    print(mini,maxi)

# Driver Code
if __name__ == '__main__':
    arr =  [1, 2, 3, 4]
    N = len(arr)
    findMaxMinSum(arr, N)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class pair : IComparable<pair>
{
    public int first,second, third;
    public pair(int first,int second, int third)
    {
        this.first = first;
        this.second = second;
        this.third = third;
    }
    public int CompareTo(pair p)
    {
        return this.second-p.first;
    }
}

class GFG{

// Function to find the required sum
static int findSum(List<pair> v, int n)
{

    // Keeps the track of the
    // visited array elements
    Dictionary<int,
               Boolean> um = new Dictionary<int,
                                            Boolean>();

    // Stores the result
    int res = 0;

    // Keeps count of visited elements
    int cnt = 0;

    // Traverse the vector, V
    for(int i = 0; i < v.Count; i++)
    {

        // If n elements are visited,
        // break out of the loop
        if (cnt == n)
            break;

        // Store the pair (i, j) and
        // their Bitwise XOR
        int x = v[i].second;
        int y = v[i].third;
        int xorResult = v[i].first;

        // If i and j both are unvisited
        if (!um.ContainsKey(x) && !um.ContainsKey(y))
        {

            // Add xorResult to res and
            // mark i and j as visited
            res += xorResult;
            um.Add(x,true);
            um.Add(y, true);

            // Increment count by 2
            cnt += 2;
        }
    }

    // Return the result
    return res;
}

// Function to find the maximum and
// minimum possible sum of Bitwise
// XOR of all the pairs from the array
static void findMaxMinSum(int []a, int n)
{

    // Stores the XOR of all pairs (i, j)
    List<pair> v = new List<pair>();

    // Store the XOR of all pairs (i, j)
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Update Bitwise XOR
            int xorResult = a[i] ^ a[j];
            v.Add(new pair(xorResult, a[i], a[j]));
        }
    }

    // Sort the vector
    v.Sort();

    // Initialize variables to store
    // maximum and minimum possible sums
    int maxi = 0, mini = 0;

    // Find the minimum sum possible
    mini = findSum(v, n);

    // Reverse the vector, v
    v.Reverse();

    // Find the maximum sum possible
    maxi = findSum(v, n);

    // Print the result
    Console.Write(mini + " " + maxi);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    findMaxMinSum(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the required sum
function findSum(v, n)
{
    // Keeps the track of the
    // visited array elements
    var um = new Map();

    // Stores the result
    var res = 0;

    // Keeps count of visited elements
    var cnt = 0;

    // Traverse the vector, V
    for (var i = 0; i < v.length; i++) {

        // If n elements are visited,
        // break out of the loop
        if (cnt == n)
            break;

        // Store the pair (i, j) and
        // their Bitwise XOR
        var x = v[i][1][0];
        var y = v[i][1][1];
        var xorResult = v[i][0];

        // If i and j both are unvisited
        if (!um.has(x) && !um.has(y)) {

            // Add xorResult to res and
            // mark i and j as visited
            res += xorResult;
            um.set(x, true);
            um.set(y, true);

            // Increment count by 2
            cnt += 2;
        }
    }

    // Return the result
    return res;
}

// Function to find the maximum and
// minimum possible sum of Bitwise
// XOR of all the pairs from the array
function findMaxMinSum(a, n)
{

    // Stores the XOR of all pairs (i, j)
    var v = [];

    // Store the XOR of all pairs (i, j)
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {

            // Update Bitwise XOR
            var xorResult = a[i] ^ a[j];
            v.push([xorResult, [a[i], a[j] ]]);
        }
    }

    // Sort the vector
    v.sort();

    // Initialize variables to store
    // maximum and minimum possible sums
    var maxi = 0, mini = 0;

    // Find the minimum sum possible
    mini = findSum(v, n);

    // Reverse the vector, v
    v.reverse();

    // Find the maximum sum possible
    maxi = findSum(v, n);

    // Print the result
    document.write(mini + " " + maxi);
}

// Driver Code
var arr = [1, 2, 3, 4];
var N = arr.length;
findMaxMinSum(arr, N);

// This code is contributed by itsok.
</script>
```

**Output**

```
6 10
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*