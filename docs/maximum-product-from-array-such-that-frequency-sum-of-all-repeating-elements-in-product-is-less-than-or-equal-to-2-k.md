# 来自数组的最大乘积，使得乘积中所有重复元素的频率和小于或等于 2 * k

> 原文:[https://www . geesforgeks . org/从数组中获取最大乘积，使得乘积中所有重复元素的频率和小于或等于 2-k/](https://www.geeksforgeeks.org/maximum-product-from-array-such-that-frequency-sum-of-all-repeating-elements-in-product-is-less-than-or-equal-to-2-k/)

给定一个数组 **arr[]** 和一个整数 **k** ，任务是从数组中找到最大乘积，使得乘积中所有重复元素的频率和为 **≤ 2 * k** ，其中频率和为乘积中所有出现多次的元素的频率和。例如，如果我们选择一个乘积 **1 * 1 * 2 * 3 * 4 * 5 * 6 * 6 * 7 * 8 * 8** ，那么这个乘积中重复元素的频率和是 6，因为乘积中的重复元素是 1、6 和 8(1 的频率+6 的频率+8 的频率)= 2+2+2)= 6

**示例:**

> **输入:** arr[] = {5，6，7，8，2，5，6，8}，k = 2
> **输出:** 161280
> 产品可以是:
> 5 * 5 * 7 * 8 * 2 * 6 = 134400
> 5 * 8 * 8 * 7 * 6 * 2 = 161280
> 2 * 7 * 6 * 5 * 8 * 6 * 5 = 100800
> 
> **输入:** arr[] = {1，5，1，5，4，3，8}，k = 2
> **输出:** 2400

**方法:**首先取数组中所有元素的乘积(只包括元素的单次出现，因为单次出现不会影响频率和)。现在，为了最大化乘积，对数组进行排序，并从最大的元素开始获取所有剩余的元素，直到频率总和不超过 **2 * k** 。最后打印计算出来的产品。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the maximum product value
ll maxProd(int arr[], int n, int k)
{

    // To store the product
    ll product = 1;
    unordered_map<int, int> s;

    // Sort the array
    sort(arr, arr + n);

    for (int i = 0; i < n; i++) {
        if (s[arr[i]] == 0) {

            // Efficiently finding product
            // including every element once
            product = product * arr[i];
        }

        // Storing values in hash map
        s[arr[i]] = s[arr[i]] + 1;
    }

    for (int j = n - 1; j >= 0 && k > 0; j--) {
        if ((k > (s[arr[j]] - 1)) && ((s[arr[j]] - 1) > 0)) {

            // Including the greater repeating values
            // so that product can be maximized
            product *= pow(arr[j], s[arr[j]] - 1);
            k = k - s[arr[j]] + 1;
            s[arr[j]] = 0;
        }
        if (k <= (s[arr[j]] - 1) && ((s[arr[j]] - 1) > 0)) {
            product *= pow(arr[j], k);
            break;
        }
    }

    return product;
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 7, 8, 2, 5, 6, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 2;
    cout << maxProd(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function to return the maximum product value
    static long maxProd(int arr[], int n, int k)
    {

        // To store the product
        long product = 1;
        HashMap<Integer,Integer> s = new HashMap<Integer,Integer>(); 

        // Sort the array
        Arrays.sort(arr);

        for (int i = 0; i < n; i++)
        {
            if (s.containsKey(arr[i]) == false)
            {

                // Efficiently finding product
                // including every element once
                product = product * arr[i];

                s.put(arr[i], 1);

            }

            // Storing values in hash map
            else
                s.put(arr[i],s.get(arr[i]) +1);

        }

        for (int j = n - 1; j >= 0 && k > 0; j--) 
        {
            if ((k > (s.get(arr[j]) - 1)) && 
                    ((s.get(arr[j]) - 1) > 0)) 
            {

                // Including the greater repeating values
                // so that product can be maximized
                product *= Math.pow(arr[j], s.get(arr[j]) - 1);
                k = k - s.get(arr[j]) + 1;
                s.put(arr[j], 0);
            }
            if (k <= (s.get(arr[j]) - 1) && 
                    ((s.get(arr[j]) - 1) > 0)) 
            {
                product *= Math.pow(arr[j], k);
                break;
            }
        }

        return product;
    }

    // Driver code
    public static void main (String[] args) 
    {
        int arr[] = { 5, 6, 7, 8, 2, 5, 6, 8 };
        int n = arr.length;
        int k = 2;
        System.out.println(maxProd(arr, n, k));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach 

# Function to return the maximum 
# product value 
def maxProd(arr, n, k) :

    # To store the product 
    product = 1; 
    s = dict.fromkeys(arr, 0); 

    # Sort the array 
    arr.sort(); 

    for i in range(n) :
        if (s[arr[i]] == 0) :

            # Efficiently finding product 
            # including every element once 
            product = product * arr[i]; 

        # Storing values in hash map 
        s[arr[i]] = s[arr[i]] + 1; 

    j = n - 1;
    while (j >= 0 and k > 0) :

        if ((k > (s[arr[j]] - 1)) and 
           ((s[arr[j]] - 1) > 0)) :

            # Including the greater repeating values 
            # so that product can be maximized 
            product *= pow(arr[j], s[arr[j]] - 1); 
            k = k - s[arr[j]] + 1; 
            s[arr[j]] = 0; 

        if (k <= (s[arr[j]] - 1) and 
                ((s[arr[j]] - 1) > 0)) : 
            product *= pow(arr[j], k); 
            break;
        j -= 1

    return product; 

# Driver code 
if __name__ == "__main__" : 

    arr = [ 5, 6, 7, 8, 2, 5, 6, 8 ]; 
    n = len(arr) ;
    k = 2; 

    print(maxProd(arr, n, k)); 

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System; 
using System.Collections.Generic; 

class GFG
{
    // Function to return the maximum product value
    static long maxProd(int []arr, int n, int k)
    {

        // To store the product
        long product = 1;
        Dictionary<int, int> s = new Dictionary<int, int>(); 
        // Sort the array
        Array.Sort(arr);

        for (int i = 0; i < n; i++) 
        {
            if (!s.ContainsKey(arr[i]))
            {

                // Efficiently finding product
                // including every element once
                product = product * arr[i];

                s[arr[i]] = 1;
            }

            // Storing values in hash map
                else
            s[arr[i]]++;

        }

        for (int j = n - 1; j >= 0 && k > 0; j--)
        {
            if ((k > (s[arr[j]] - 1)) &&
                    ((s[arr[j]] - 1) > 0))
            {

                // Including the greater repeating values
                // so that product can be maximized
                product *= (long)Math.Pow(arr[j], s[arr[j]] - 1);
                k = k - s[arr[j]] + 1;
                s[arr[j]] = 0;
            }
            if (k <= (s[arr[j]] - 1) && ((s[arr[j]] - 1) > 0)) 
            {
                product *= (long)Math.Pow(arr[j], k);
                break;
            }
        }

        return product;
    }

    // Driver code
    public static void Main () 
    {
        int []arr = { 5, 6, 7, 8, 2, 5, 6, 8 };
        int n = arr.Length;
        int k = 2;
        Console.WriteLine(maxProd(arr, n, k));
    }
}

// This code is contributed by ihritik
```

**Output:**

```
161280

```