# 从前面选择元素，或从后面选择元素，或两者都选择，选择和为 K 的数组元素的最小操作

> 原文:[https://www . geeksforgeeks . org/最小操作-选择数组元素-通过选择元素-从前面或后面或两者都选择-将元素和为 k/](https://www.geeksforgeeks.org/minimum-operations-to-choose-array-elements-with-sum-as-k-by-choosing-element-from-front-or-rear-or-both/)

给定一个大小为 **N** 的正整数[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，以及一个整数 **K** 。任务是最小化所需的操作数量选择总和为 k 的数组元素。在一次操作中，一个元素可以从**前**或**后**移除，或者从**前**和**后**移除，并添加到总和**中。**如果不能达到期望的总和，返回 **-1** 。

**示例:**

> **输入:** arr[] = {3，5，4，2，1}，N = 5，K = 6
> **输出:** 2
> **解释:**
> 
> *   在操作 1 中，访问索引 0 和 4，选择两个元素(3 和 1)，从而使总和为 3 + 1 = 4
> *   在操作 2 中，访问索引 3(元素 2)，从而使总和为 4 + 2 = 6。
> 
> 因此，所需的最小操作数= 2
> 
> **输入:** arr[] = {4，7，2，3，1，9，8}，N = 6，K = 9
> **输出:** 3

**方法:**按照以下步骤解决问题:

1.  创建一个**图**，取两个变量分别表示 **m1** 和 **m2** 为**局部最大值**和**全局最小值**。
2.  遍历数组并检查以下条件:
    *   如果元素**大于**或**等于**等于 **k** ，则**继续，**因为当添加到任何其他元素时它不能产生 **k** ，因为所有元素**大于**大于**零**。
    *   如果元素正好是 **k** 的**一半**，那么也**继续**因为在这里，任务是找到两个**不同的**元素。
    *   如果**地图**的位置已经被填充，也就是说，如果**相同的**元素被更早地找到，那么检查那个是否是更靠近的**到任何**末端**或者这个新元素是更靠近**的**，并且**用那个**键**更新**的值，否则简单地检查从哪个末端是更靠近**的元素**并将其放入**地图**。**
    *   如果找到了一个在地图中较早填充的元素，并且该元素与当前元素的和为 **k** ，则在填充**地图**时，选择这两个元素所花费的时间将是**最大值**，而 **m2** 是所有这些不同对的和为 **k** 的**最小值**，其中每对每个数字都是已经选择的**。**
3.  **穿越后，检查 **m2** 的值。如果 **m2** 仍然是 **INT_MAX** ，则返回 **-1** ，否则返回 **m2** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum time required
// to visit array elements to get the
// sum equal to k
int minimumTime(int arr[], int N, int k)
{
    // Create a map
    map<int, int> mp;

    // m1 is to keep the local maxima
    int m1 = 0;

    // m2 is to keep the global minima
    int m2 = INT_MAX;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If the element is greater than
        // or equal to k then continue
        if (arr[i] >= k)
            continue;

        // If the element is exactly the
        // half of k, then also continue
        if (arr[i] == k / 2 && k - arr[i] == k / 2)
            continue;

        // If the position at the map is already filled,
        // i.e if the same element was found earlier
        // then check if that was nearer to any end
        // or this new element is nearer and update
        // the value with that key, else check from
        // which end is the element closer and put it
        // in the map
        mp[arr[i]] = mp[arr[i]] ? min(mp[arr[i]],
                                      min(i + 1, N - i))
                                : min(i + 1, N - i);

        // If an element is found which was filled
        // earlier in the map, which makes the sum
        // to k with the current element then the
        // time taken will be maximum of picking
        // both elements because it is visited
        // simultaneously
        if (mp[k - arr[i]]) {
            m1 = max(mp[arr[i]], mp[k - arr[i]]);

            // m2 is the minimal of all such distinct
            // pairs that sum to k where in each pair
            // each number was optimally chosen already
            // while filling the map
            m2 = min(m1, m2);
        }
    }
    // If m2 is still INT_MAX, then there is no such pair
    // else return the minimum time
    return m2 != INT_MAX ? m2 : -1;
}

// Driver Code
int main()
{
    int arr[] = { 4, 7, 2, 3, 1, 9, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 6;

    cout << minimumTime(arr, N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum time required
// to visit array elements to get the
// sum equal to k
static int minimumTime(int arr[], int N, int k)
{
    // Create a map
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // m1 is to keep the local maxima
    int m1 = 0;

    // m2 is to keep the global minima
    int m2 = Integer.MAX_VALUE;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If the element is greater than
        // or equal to k then continue
        if (arr[i] >= k)
            continue;

        // If the element is exactly the
        // half of k, then also continue
        if (arr[i] == k / 2 && k - arr[i] == k / 2)
            continue;

        // If the position at the map is already filled,
        // i.e if the same element was found earlier
        // then check if that was nearer to any end
        // or this new element is nearer and update
        // the value with that key, else check from
        // which end is the element closer and put it
        // in the map
        if(mp.containsKey(arr[i]))
            mp.put(arr[i], Math.min(mp.get(arr[i]),
                                      Math.min(i + 1, N - i)));
        else
            mp.put(arr[i], Math.min(i + 1, N - i));

        // If an element is found which was filled
        // earlier in the map, which makes the sum
        // to k with the current element then the
        // time taken will be maximum of picking
        // both elements because it is visited
        // simultaneously
        if (mp.containsKey(k - arr[i])) {
            m1 = Math.max(mp.get(arr[i]), mp.get(k-arr[i]));

            // m2 is the minimal of all such distinct
            // pairs that sum to k where in each pair
            // each number was optimally chosen already
            // while filling the map
            m2 = Math.min(m1, m2);
        }
    }
    // If m2 is still Integer.MAX_VALUE, then there is no such pair
    // else return the minimum time
    return m2 != Integer.MAX_VALUE ? m2 : -1;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 7, 2, 3, 1, 9, 8 };
    int N = arr.length;
    int K = 6;

    System.out.print(minimumTime(arr, N, K));

}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python Program to implement
# the above approach

# Function to find minimum time required
# to visit array elements to get the
# sum equal to k
def minimumTime(arr, N, k):
    # Create a map
    mp = {}

    # m1 is to keep the local maxima
    m1 = 0

    # m2 is to keep the global minima
    m2 = 10 ** 9

    # Traverse the array
    for i in range(N):

        # If the element is greater than
        # or equal to k then continue
        if (arr[i] >= k):
            continue

        # If the element is exactly the
        # half of k, then also continue
        if (arr[i] == k // 2 and k - arr[i] == k // 2):
            continue

        # If the position at the map is already filled,
        # i.e if the same element was found earlier
        # then check if that was nearer to any end
        # or this new element is nearer and update
        # the value with that key, else check from
        # which end is the element closer and put it
        # in the map

        if (arr[i] not in mp):
            mp[arr[i]] = min(i + 1, N - i)
        else:
            mp[arr[i]] = min( mp[arr[i]], min(i + 1, N - i))

        # If an element is found which was filled
        # earlier in the map, which makes the sum
        # to k with the current element then the
        # time taken will be maximum of picking
        # both elements because it is visited
        # simultaneously
        if ((k - arr[i]) in mp):
            m1 = max(mp[arr[i]], mp[k - arr[i]])

            # m2 is the minimal of all such distinct
            # pairs that sum to k where in each pair
            # each number was optimally chosen already
            # while filling the map
            m2 = min(m1, m2)

    # If m2 is still INT_MAX, then there is no such pair
    # else return the minimum time
    return m2 if m2 != 10**9 else -1

# Driver Code
arr = [4, 7, 2, 3, 1, 9, 8]
N = len(arr)
K = 6

print(minimumTime(arr, N, K))

# This code is contributed by gfgking
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find minimum time required
// to visit array elements to get the
// sum equal to k
static int minimumTime(int[] arr, int N, int k)
{

    // Create a map
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // m1 is to keep the local maxima
    int m1 = 0;

    // m2 is to keep the global minima
    int m2 = Int32.MaxValue;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If the element is greater than
        // or equal to k then continue
        if (arr[i] >= k)
            continue;

        // If the element is exactly the
        // half of k, then also continue
        if (arr[i] == k / 2 && k - arr[i] == k / 2)
            continue;

        // If the position at the map is already filled,
        // i.e if the same element was found earlier
        // then check if that was nearer to any end
        // or this new element is nearer and update
        // the value with that key, else check from
        // which end is the element closer and put it
        // in the map
        if (mp.ContainsKey(arr[i]))
            mp[arr[i]] = Math.Min(
                mp[arr[i]], Math.Min(i + 1, N - i));
        else
            mp[arr[i]] = Math.Min(i + 1, N - i);

        // If an element is found which was filled
        // earlier in the map, which makes the sum
        // to k with the current element then the
        // time taken will be maximum of picking
        // both elements because it is visited
        // simultaneously
        if (mp.ContainsKey(k - arr[i]))
        {
            m1 = Math.Max(mp[arr[i]], mp[k - arr[i]]);

            // m2 is the minimal of all such distinct
            // pairs that sum to k where in each pair
            // each number was optimally chosen already
            // while filling the map
            m2 = Math.Min(m1, m2);
        }
    }

    // If m2 is still Integer.MAX_VALUE, then there is
    // no such pair else return the minimum time
    return m2 != Int32.MaxValue ? m2 : -1;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 4, 7, 2, 3, 1, 9, 8 };
    int N = arr.Length;
    int K = 6;

    Console.WriteLine(minimumTime(arr, N, K));
}
}

// This code is contributed by ukasp
```

## **java 描述语言**

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find minimum time required
        // to visit array elements to get the
        // sum equal to k
        function minimumTime(arr, N, k)
        {

            // Create a map
            let mp = new Map();

            // m1 is to keep the local maxima
            let m1 = 0;

            // m2 is to keep the global minima
            let m2 = Number.MAX_VALUE;

            // Traverse the array
            for (let i = 0; i < N; i++) {

                // If the element is greater than
                // or equal to k then continue
                if (arr[i] >= k)
                    continue;

                // If the element is exactly the
                // half of k, then also continue
                if (arr[i] == Math.floor(k / 2) && k - arr[i] == Math.floor(k / 2))
                    continue;

                // If the position at the map is already filled,
                // i.e if the same element was found earlier
                // then check if that was nearer to any end
                // or this new element is nearer and update
                // the value with that key, else check from
                // which end is the element closer and put it
                // in the map

                if (!mp.has(arr[i])) {
                    mp.set(arr[i], Math.min(i + 1, N - i))
                }
                else {
                    mp.set(arr[i], Math.min(mp.get(arr[i]), Math.min(i + 1, N - i)))
                }

                // If an element is found which was filled
                // earlier in the map, which makes the sum
                // to k with the current element then the
                // time taken will be maximum of picking
                // both elements because it is visited
                // simultaneously
                if (mp.has(k - arr[i])) {
                    m1 = Math.max(mp.get(arr[i]), mp.get(k - arr[i]));

                    // m2 is the minimal of all such distinct
                    // pairs that sum to k where in each pair
                    // each number was optimally chosen already
                    // while filling the map
                    m2 = Math.min(m1, m2);
                }
            }
            // If m2 is still INT_MAX, then there is no such pair
            // else return the minimum time
            return m2 != Number.MAX_VALUE ? m2 : -1;
        }

        // Driver Code
        let arr = [4, 7, 2, 3, 1, 9, 8];
        let N = arr.length;
        let K = 6;

        document.write(minimumTime(arr, N, K));

    // This code is contributed by Potta Lokesh
    </script>
```

****Output**

```
3
```** 

*****时间复杂度*****:**O(N)
***辅助空间*** **:** O(N)**