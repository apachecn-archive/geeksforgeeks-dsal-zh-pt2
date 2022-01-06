# 最多删除一个元素后，最大化包含最大和最小数组元素的子数组数

> 原文:[https://www . geesforgeks . org/maximize-subarrays-count-包含最多删除一个元素后的最大和最小数组元素/](https://www.geeksforgeeks.org/maximize-subarrays-count-containing-the-maximum-and-minimum-array-element-after-deleting-at-most-one-element/)

给定一个 **N** 大小的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】。任务是通过从数组中最多删除一个元素来最大化包含数组的最小和最大元素的子数组的数量。

**例:**

> **输入:** arr[] = {7，2，5，4，3，1}
> **输出:** 4
> **解释:**
> 从数组中删除 1，则结果数组将为{7，2，5，4，3}。所以包含最大元素 7 和最小元素 2 的子阵数量将是 4 {[7，2]，[7，2，5]，[7，2，5，4]，[7，2，5，4，3]}
> 
> **输入:** arr[] = {9，9，8，9，8，9，9，8，9，8}
> **输出:** 43

**天真方法:**最简单的方法是删除每个元素，然后计算结果数组中具有最小和最大元素的子数组的数量。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**这种方法基于这样的观察，即删除最大或最小元素以外的元素永远不会使整体结果最大化。以下是步骤:

1.  用 INT_MIN 初始化整体结果。
2.  创建一个函数，比如 **proc** ，返回包含数组中最小和最大元素的子数组的数量。
3.  要计算子阵列的数量，使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)方法找到子阵列的开始和结束索引:
    *   用数组的最后一个元素初始化最小和最大的元素，比如**低**和**高**。
    *   用数组的最后一个索引初始化两个指针 **p1** 和 **p2** ，该数组存储了**低**和**高**的位置。
    *   现在，迭代数组并检查当前元素是否小于**低**，然后更新 **p1** 。
    *   如果当前元素高于**高**，则更新 **p2** 。
    *   在每一步，更新子阵列的最大数量。
4.  现在，在以下三种情况下计算子阵列的数量:
    *   不移除任何元素

    *   移除最大的元素后
    *   去掉最小的元素后。
5.  取三种情况的最大值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
// Returns the count of subarrays
// which contains both the maximum and
// minimum elements in the given vector
long long proc(vector<int> &v)
    {

        long long int n = v.size();

        // Initialize the low and
        // high of array
        int low = v[n - 1], high = v[n - 1];
        long long int p1 = n, p2 = n;
        long long ans = 0;

        for (int i = n - 1; i >= 0; i--) {
            int x = v[i];

            // If current element is
            // less than least element
            if (x < low) {
                low = x;
                ans = 0;
            }

            // If current element is
            // more than highest element
            else if (x > high) {
                high = x;
                ans = 0;
            }

            // If current element is
            // equal to low or high
            // then update the pointers
            if (x == low)
                p1 = i;
            if (x == high)
                p2 = i;

            // Update number of subarrays
            ans += n - max(p1, p2);
        }

        // Return the result
        return ans;
    }

// Function to find the maximum
    // count of subarrays
long long subarray(vector<int>& v)
{
    long long int n=v.size();
    if(n<=1)
    return n;
    long long ans=proc(v);
    int low=v[0],pos_low=0,high=v[0],pos_high=0;
    // Iterate the array to find
    // the maximum and minimum element
    for (int i = 1; i < n; i++) {
            int x = v[i];
            if (x < low) {
                low = x;
                pos_low = i;
            }
            else if (x > high) {
                high = x;
                pos_high = i;
            }
        }
        // Vector after removing the
        // minimum element
        vector<int>u;
         // Using assignment operator to copy one
         //  vector to other
         u=v;
         u.erase(u.begin()+pos_low);
         ans=max(ans,proc(u));
         // Vector after removing the
        // maximum element
        vector<int>w;
        w=v;
        w.erase(w.begin()+pos_high);
        return max(ans,proc(w));

}

// Driver Code
int main()
{

    // Given array
    vector<int>v;
    v.push_back(7);
    v.push_back(2);
    v.push_back(5);
    v.push_back(4);
    v.push_back(3);
    v.push_back(1);

  // Function Call
  cout<<subarray(v)<<endl;

    return 0;
}
// This code is contributed by dwivediyash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to find the maximum
    // count of subarrays
    static long subarray(List<Integer> v)
    {
        int n = v.size();
        if (n <= 1)
            return n;

        long ans = proc(v);
        int low = v.get(0), pos_low = 0;
        int high = v.get(0), pos_high = 0;

        // Iterate the array to find
        // the maximum and minimum element
        for (int i = 1; i < n; i++) {
            int x = v.get(i);
            if (x < low) {
                low = x;
                pos_low = i;
            }
            else if (x > high) {
                high = x;
                pos_high = i;
            }
        }

        // List after removing the
        // minimum element
        List<Integer> u
            = new ArrayList<>(
                Collections.nCopies(n, 0));
        Collections.copy(u, v);
        u.remove(pos_low);
        ans = Math.max(ans, proc(u));

        // List after removing the
        // maximum element
        List<Integer> w
            = new ArrayList<>(
                Collections.nCopies(n, 0));
        Collections.copy(w, v);
        w.remove(pos_high);

        return Math.max(ans, proc(w));
    }

    // Returns the count of subarrays
    // which contains both the maximum and
    // minimum elements in the given list
    static long proc(List<Integer> v)
    {

        int n = v.size();

        // Initialize the low and
        // high of array
        int low = v.get(n - 1), high = v.get(n - 1);
        int p1 = n, p2 = n;
        long ans = 0;

        for (int i = n - 1; i >= 0; i--) {
            int x = v.get(i);

            // If current element is
            // less than least element
            if (x < low) {
                low = x;
                ans = 0;
            }

            // If current element is
            // more than highest element
            else if (x > high) {
                high = x;
                ans = 0;
            }

            // If current element is
            // equal to low or high
            // then update the pointers
            if (x == low)
                p1 = i;
            if (x == high)
                p2 = i;

            // Update number of subarrays
            ans += n - Math.max(p1, p2);
        }

        // Return the result
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        List<Integer> arr = Arrays.asList(7, 2, 5, 4, 3, 1);

        // Function Call
        System.out.println(subarray(arr));
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Returns the count of subarrays
# which contains both the maximum and
# minimum elements in the given vector
def proc(v):
  n = len(v);

  # Initialize the low and
  # high of array
  low = v[n - 1]
  high = v[n - 1]
  p1 = n
  p2 = n;
  ans = 0;

  for i in range(n - 1, -1, -1):
    x = v[i];

    # If current element is
    # less than least element
    if (x < low):
      low = x;
      ans = 0;

    # If current element is
    # more than highest element
    elif (x > high):
      high = x;
      ans = 0;

    # If current element is
    # equal to low or high
    # then update the pointers
    if (x == low): p1 = i;
    if (x == high): p2 = i;

    # Update number of subarrays
    ans += n - max(p1, p2);

  # Return the result
  return ans;

# Function to find the maximum
# count of subarrays
def subarray(v):
  n = len(v);

  if (n <= 1):
    return n;

  ans = proc(v);
  low = v[0]
  pos_low = 0
  high = v[0]
  pos_high = 0

  # Iterate the array to find
  # the maximum and minimum element
  for i in range(1, n):
    x = v[i];
    if (x < low):
      low = x;
      pos_low = i;
    elif (x > high):
      high = x;
      pos_high = i;

  # Vector after removing the
  # minimum element
  u = v[:];

  # Using assignment operator to copy one
  #  vector to other
  del u[pos_low];

  ans = max(ans, proc(u));

  # Vector after removing the
  # maximum element
  w = v[:];

  del w[pos_high];
  return max(ans, proc(w));

# Driver Code

# Given array
v = [];
v.append(7);
v.append(2);
v.append(5);
v.append(4);
v.append(3);
v.append(1);

# Function Call
print(subarray(v));

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Returns the count of subarrays
// which contains both the maximum and
// minimum elements in the given vector
function proc(v)
{
  let n = v.length;

  // Initialize the low and
  // high of array
  let low = v[n - 1],
    high = v[n - 1];
  let p1 = n,
    p2 = n;
  let ans = 0;

  for (let i = n - 1; i >= 0; i--) {
    let x = v[i];

    // If current element is
    // less than least element
    if (x < low) {
      low = x;
      ans = 0;
    }

    // If current element is
    // more than highest element
    else if (x > high) {
      high = x;
      ans = 0;
    }

    // If current element is
    // equal to low or high
    // then update the pointers
    if (x == low) p1 = i;
    if (x == high) p2 = i;

    // Update number of subarrays
    ans += n - Math.max(p1, p2);
  }

  // Return the result
  return ans;
}

// Function to find the maximum
// count of subarrays
function subarray(v) {
  let n = v.length;

  if (n <= 1) {
    return n;
  }

  let ans = proc(v);
  let low = v[0],
    pos_low = 0,
    high = v[0],
    pos_high = 0;

  // Iterate the array to find
  // the maximum and minimum element
  for (let i = 1; i < n; i++) {
    let x = v[i];
    if (x < low) {
      low = x;
      pos_low = i;
    } else if (x > high) {
      high = x;
      pos_high = i;
    }
  }

  // Vector after removing the
  // minimum element
  let u = [...v];

  // Using assignment operator to copy one
  //  vector to other
  u.splice(pos_low, 1);

  ans = Math.max(ans, proc(u));

  // Vector after removing the
  // maximum element
  let w = [...v];

  w.splice(pos_high, 1);

  return Math.max(ans, proc(w));
}

// Driver Code

// Given array
let v = [];
v.push(7);
v.push(2);
v.push(5);
v.push(4);
v.push(3);
v.push(1);

// Function Call
document.write(subarray(v));

// This code is contributed by gfgking

</script>
```

**Output** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间** : O(N)