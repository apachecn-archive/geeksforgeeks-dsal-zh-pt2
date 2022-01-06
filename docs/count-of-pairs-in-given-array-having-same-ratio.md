# 给定阵列中具有相同比率的对的计数

> 原文:[https://www . geesforgeks . org/给定阵列中具有相同比率的对的计数/](https://www.geeksforgeeks.org/count-of-pairs-in-given-array-having-same-ratio/)

给定一个由形式为 **{A，B}** 的 **N** 对组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是对索引对 **(i，j)** 进行计数，使得 **arr[i]** 和 **arr[j]** 对的比率相同。

**示例:**

> **输入:** arr[] = {{2，6}，{1，3}，{8，24}}
> **输出:** 3
> **解释:**
> 以下是比率相同的指数对:
> 
> 1.  (0，1):对 arr[0] = 2/6 = 1/3 的比值和对 arr[1] = 1/3 的比值，二者相同。
> 2.  (0，2):对 arr[0] = 2/6 = 1/3 的比值和对 arr[2] = 8/24 = 1/3 的比值，二者相同。
> 3.  (1，2):对 arr[1]的比值= 1/3，对 arr[2]的比值= 8/24 = 1/3，二者相同。
> 
> 因此，这种对的计数是 3。
> 
> **输入:** arr[] = {{4，5}，{7，8 } }
> T3】输出: 0

**天真方法:**解决给定问题的最简单方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能对，并计算那些比率相同的对。检查所有配对后，打印获得的配对总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of pairs
// having same ratio
long long pairsWithSameRatio(
    vector<pair<int, int> >& arr)
{
    // Stores the total count of pairs
    int count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < arr.size(); i++) {

        // Find the first ratio
        double ratio1
            = (double)arr[i].first
              / (double)arr[i].second;

        for (int j = i + 1; j < arr.size(); j++) {

            // Find the second ratio
            double ratio2 = (double)arr[j].first
                            / (double)arr[j].second;

            // Increment the count if
            // the ratio are the same
            if (ratio1 == ratio2) {
                count++;
            }
        }
    }

    // Return the total count obtained
    return count;
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr = {
        { 2, 6 }, { 1, 3 }, { 8, 24 }, { 4, 12 }, { 16, 48 }
    };
    cout << pairsWithSameRatio(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {
    static class pair {
        int first, second;

        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    // Function to find the count of pairs
    // having same ratio
    static long pairsWithSameRatio(pair[] arr)
    {

        // Stores the total count of pairs
        int count = 0;

        // Traverse the array arr[]
        for (int i = 0; i < arr.length; i++) {

            // Find the first ratio
            double ratio1 = (double) arr[i].first / (double) arr[i].second;

            for (int j = i + 1; j < arr.length; j++) {

                // Find the second ratio
                double ratio2 = (double) arr[j].first / (double) arr[j].second;

                // Increment the count if
                // the ratio are the same
                if (ratio1 == ratio2) {
                    count++;
                }
            }
        }

        // Return the total count obtained
        return count;
    }

    // Driver Code
    public static void main(String[] args) {
        pair[] arr = { new pair(2, 6), new pair(1, 3), new pair(8, 24), new pair(4, 12), new pair(16, 48) };
        System.out.print(pairsWithSameRatio(arr));

    }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the count of pairs
# having same ratio
def pairsWithSameRatio(arr):

    # Stores the total count of pairs
    count = 0

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Find the first ratio
        ratio1 = arr[i][0]//arr[i][1]

        for j in range(i + 1, len(arr), 1):

            # Find the second ratio
            ratio2 = arr[j][0]//arr[j][1]

            # Increment the count if
            # the ratio are the same
            if (ratio1 == ratio2):
                count += 1

    # Return the total count obtained
    return count

# Driver Code
if __name__ == '__main__':
    arr = [[2, 6],[1, 3],[8, 24],[4, 12],[16, 48]]
    print(pairsWithSameRatio(arr))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG {
    class pair {
        public int first, second;

        public pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
    }

    // Function to find the count of pairs
    // having same ratio
    static long pairsWithSameRatio(pair[] arr)
    {

        // Stores the total count of pairs
        int count = 0;

        // Traverse the array []arr
        for (int i = 0; i < arr.Length; i++) {

            // Find the first ratio
            double ratio1 = (double) arr[i].first / (double) arr[i].second;

            for (int j = i + 1; j < arr.Length; j++) {

                // Find the second ratio
                double ratio2 = (double) arr[j].first / (double) arr[j].second;

                // Increment the count if
                // the ratio are the same
                if (ratio1 == ratio2) {
                    count++;
                }
            }
        }

        // Return the total count obtained
        return count;
    }

    // Driver Code
    public static void Main(String[] args) {
        pair[] arr = { new pair(2, 6), new pair(1, 3), new pair(8, 24), new pair(4, 12), new pair(16, 48) };
        Console.Write(pairsWithSameRatio(arr));

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the count of pairs
        // having same ratio
        function pairsWithSameRatio(
            arr) {
            // Stores the total count of pairs
            let count = 0;

            // Traverse the array arr[]
            for (let i = 0; i < arr.length; i++) {

                // Find the first ratio
                let ratio1
                    = arr[i].first
                    / arr[i].second;

                for (let j = i + 1; j < arr.length; j++) {

                    // Find the second ratio
                    ratio2 = arr[j].first
                        / arr[j].second;

                    // Increment the count if
                    // the ratio are the same
                    if (ratio1 == ratio2) {
                        count++;
                    }
                }
            }

            // Return the total count obtained
            return count;
        }

        // Driver Code
        let arr = [
            { first: 2, second: 6 }, { first: 1, second: 3 }, { first: 8, second: 24 }, { first: 4, second: 12 }, { first: 16, second: 48 }
        ]
        document.write(pairsWithSameRatio(arr));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**通过存储给定数组中每个对的比率的频率，然后计算形成的对的总数，可以使用映射来优化上述方法。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说**和**为 **0** ，它存储具有相同比率的对的总数。
*   创建一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)，比如说**映射**，它将键存储为数组元素对的比率，将值存储为它们的频率。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每一对 **{A，B}** 将地图中 **A/B** 的频率增加 **1** 。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **地图**，对于每个**键值**对，如果任意键的频率大于 1，则将**频率*(频率–1)/2**的值添加到变量**和**中，以当前**键**作为比率存储结果对计数。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Returns factorial of N
int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Return the value of nCr
int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to count the number of pairs
// having the same ratio
int pairsWithSameRatio(
    vector<pair<int, int> >& arr)
{
    // Stores the frequency of the ratios
    unordered_map<double, int> mp;
    int ans = 0;

    // Filling the map
    for (auto x : arr) {
        mp[x.first / x.second] += 1;
    }

    for (auto x : mp) {
        int val = x.second;

        // Find the count of pairs with
        // current key as the ratio
        if (val > 1) {
            ans += nCr(val, 2);
        }
    }

    // Return the total count
    return ans;
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr = {
        { 2, 6 }, { 1, 3 }, { 8, 24 }, { 4, 12 }, { 16, 48 }
    };
    cout << pairsWithSameRatio(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Returns factorial of N
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Return the value of nCr
static int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to count the number of pairs
// having the same ratio
static int pairsWithSameRatio(
    pair []arr)
{

    // Stores the frequency of the ratios
    Map<Double, Integer> mp = new HashMap<Double, Integer>();
    int ans = 0;

    // Filling the map
    for (pair x : arr) {
        if(mp.containsKey((double) (x.first / x.second))){
            mp.put((double) (x.first / x.second), mp.get((double) (x.first / x.second))+1);
        }
        else{
            mp.put((double)(x.first / x.second), 1);
        }
    }

    for (Map.Entry<Double,Integer> x : mp.entrySet()){
        int val = x.getValue();

        // Find the count of pairs with
        // current key as the ratio
        if (val > 1) {
            ans += nCr(val, 2);
        }
    }

    // Return the total count
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    pair []arr = {
            new pair( 2, 6 ), new pair( 1, 3 ), new pair( 8, 24 ), new pair( 4, 12 ), new pair( 16, 48 )
    };
    System.out.print(pairsWithSameRatio(arr));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from collections import defaultdict

# Returns factorial of N
def fact(n):

    res = 1
    for i in range(2, n + 1):
        res = res * i
    return res

# Return the value of nCr
def nCr(n, r):

    return fact(n) // (fact(r) * fact(n - r))

# Function to count the number of pairs
# having the same ratio
def pairsWithSameRatio(arr):

    # Stores the frequency of the ratios
    mp = defaultdict(int)
    ans = 0

    # Filling the map
    for x in arr:
        mp[x[0] // x[1]] += 1

    for x in mp:
        val = mp[x]

        # Find the count of pairs with
        # current key as the ratio
        if (val > 1):
            ans += nCr(val, 2)

    # Return the total count
    return ans

# Driver Code
if __name__ == "__main__":

    arr = [[2, 6], [1, 3], [8, 24], [4, 12], [16, 48]]
    print(pairsWithSameRatio(arr))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
class pair
{
    public int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Returns factorial of N
static int fact(int n)
{
    int res = 1;
    for (int i = 2; i <= n; i++)
        res = res * i;
    return res;
}

// Return the value of nCr
static int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to count the number of pairs
// having the same ratio
static int pairsWithSameRatio(
    pair []arr)
{

    // Stores the frequency of the ratios
    Dictionary<Double, int> mp = new Dictionary<Double, int>();
    int ans = 0;

    // Filling the map
    foreach (pair x in arr) {
        if(mp.ContainsKey((double) (x.first / x.second))){
            mp[(double) (x.first / x.second)]=mp[(double) (x.first / x.second)]+1;
        }
        else{
            mp.Add((double)(x.first / x.second), 1);
        }
    }

    foreach (KeyValuePair<Double,int> x in mp){
        int val = x.Value;

        // Find the count of pairs with
        // current key as the ratio
        if (val > 1) {
            ans += nCr(val, 2);
        }
    }

    // Return the total count
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    pair []arr = {
            new pair( 2, 6 ), new pair( 1, 3 ), new pair( 8, 24 ), new pair( 4, 12 ), new pair( 16, 48 )
    };
    Console.Write(pairsWithSameRatio(arr));

}
}

// This code is contributed by 29AjayKumar
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)