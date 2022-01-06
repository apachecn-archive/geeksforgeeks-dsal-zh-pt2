# 查找出现次数超过⌊N/3⌋时间的所有数组元素

> 原文:[https://www . geesforgeks . org/find-all-array-elements-发生-超过-% E2 % 8c % 8an-3% E2 % 8c % 8 B- times/](https://www.geeksforgeeks.org/find-all-array-elements-occurring-more-than-%e2%8c%8an-3%e2%8c%8b-times/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出出现次数超过 floor (n/3)次的所有数组元素。

**示例:**

> **输入:** arr[] = {5，3，5}
> **输出:** 5
> **说明:**
> 5 的频率为 2，大于 N/3(3/3 = 1)。
> 
> **输入:** arr[] = {7，7，7，3，4，4，5}
> **输出:** 4 7
> **说明:**
> 数组中 7 和 4 的出现频率为 3，比 N/3( 8/3 = 2)多。

#### **<u>方法一:</u>**

**方法:**基本解决方案是有两个循环，并跟踪所有不同元素的最大计数。如果最大计数大于 n/3，则打印。如果遍历数组后最大计数没有超过 n/3，那么多数元素就不存在。

## C++

```
// C++ program to find Majority
// element in an array
#include <bits/stdc++.h>
using namespace std;

// Function to find Majority element
// in an array
void findMajority(int arr[], int n) {

    int flag = 0;
    for (int i = 0; i < n; i++) {
        int count = 0;
        for (int j = i; j < n; j++) {
            if (arr[i] == arr[j]) {
                count++;
            }
        }
        if (count > (n / 3)) {
            cout << arr[i] << " ";
            flag = 1;
        }
    }
    if (!flag)
        cout << "No Majority Element" << endl;
}
int main() {

    int arr[] = { 2, 2, 3, 1, 3, 2, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    findMajority(arr, n);
    return 0;
}

// This code is contributed by Aman Chowdhury
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Majority
// element in an array

import java.io.*;

class GFG {

    // Function to find Majority element
    // in an array
      static void findMajority(int arr[], int n)
    {
        int flag=0;
        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = i; j < n; j++) {
                if (arr[i] == arr[j])
                    count++;
            }

            // if count is greater than n/3 means
              // current element is majority element
            if (count > n/3) {
                System.out.print(arr[i]+" ");
                  flag=1;
            }
        }

        // if flag is 0 means there is no
          // majority element is present
        if (flag==0)
            System.out.println("No Majority Element");

    }

    public static void main (String[] args) {
        int arr[] = { 2, 2, 3, 1, 3, 2, 1, 1 };
        int n = arr.length;

        // Function calling
        findMajority(arr, n);
    }
}

// This code is contributed by Aman Chowdhury
```

## 蟒蛇 3

```
# Python3 program to find Majority element in an array

# Function to find Majority element
# in an array
def findMajority(arr,  n):
    flag = 0
    for i in range(n):
        count = 0
        for j in range(i, n):
            if (arr[i] == arr[j]):
                count+=1

        # If count is greater than n/3 means
        # current element is majority element
        if (count > int(n / 3)):
            print(arr[i], end = " ")
            flag = 1

    # If flag is 0 means there is no
    # majority element is present
    if (flag == 0):
        print("No Majority Element")

arr = [ 2, 2, 3, 1, 3, 2, 1, 1 ]
n = len(arr)

# Function calling
findMajority(arr, n)

# This code is contributed by mukesh07.
```

## C#

```
// C# program to find Majority
// element in an array
using System;
using System.Collections.Generic;
class GFG {

    // Function to find Majority element
    // in an array
    static void findMajority(int[] arr, int n)
    {
        int flag = 0;
        for (int i = 0; i < n; i++) {
            int count = 0;
            for (int j = i; j < n; j++) {
                if (arr[i] == arr[j])
                    count++;
            }

            // if count is greater than n/3 means
              // current element is majority element
            if (count > n/3) {
                Console.Write(arr[i] + " ");
                flag = 1;
            }
        }

        // if flag is 0 means there is no
          // majority element is present
        if (flag == 0)
            Console.Write("No Majority Element");

    }

  static void Main() {
    int[] arr = { 2, 2, 3, 1, 3, 2, 1, 1 };
    int n = arr.Length;

    // Function calling
    findMajority(arr, n); 
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program to find Majority
// element in an array

// Function to find Majority element
// in an array
function findMajority(arr,  n)
{
    var flag = 0;
    for(var i = 0; i < n; i++)
    {
        var count = 0;
        for(var j = i; j < n; j++)
        {
            if (arr[i] == arr[j])
                count++;
        }

        // If count is greater than n/3 means
        // current element is majority element
        if (count > n / 3)
        {
            document.write(arr[i] + " ");
            flag = 1;
        }
    }

    // If flag is 0 means there is no
    // majority element is present
    if (flag == 0)
    {
        document.write("No Majority Element");
    }
}

// Driver code
var arr = [ 2, 2, 3, 1, 3, 2, 1, 1 ];
var n = arr.length;

// Function calling
findMajority(arr, n);

// This code is contributed by bunnyram19

</script>
```

**Output**

```
2 1 
```

**复杂度分析:**

*   **时间复杂度:** O(n*n)需要一个嵌套循环，其中两个循环从头到尾遍历数组，因此时间复杂度为 O(n^2).
*   **辅助空间:** O(1)由于任何操作都不需要额外的空间，因此空间复杂度是恒定的。

**<u>方法 2(使用 Hashmap):</u>**

*   **方法:**这种方法在时间复杂度上与摩尔投票算法有些相似，但在这种情况下，不需要摩尔投票算法的第二步。但像往常一样，这里的空间复杂度变成了 O(n)。

在 Hashmap(键值对)中，在 value 处，为每个元素(键)维护一个计数，并且每当计数大于数组长度的一半时，返回该键(多数元素)。

## C++

```
/* C++ program for finding out majority
element in an array */
#include <bits/stdc++.h>
using namespace std;

void findMajority(int arr[], int size)
{
    unordered_map<int, int> m;
    for(int i = 0; i < size; i++)
        m[arr[i]]++;
    int flag = 0;
    for(auto i : m)
    {
        if(i.second > size / 3)
        {
            flag =1;
            cout << i.first << " ";
        }
    }
    if(flag == 0)
        cout << "No Majority element" << endl;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 3, 1, 3, 2, 1, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    findMajority(arr, n);

    return 0;
}

// This code is contributed by Aman Chowdhury
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;

/* Program for finding out majority element in an array */

class MajorityElement
{
    private static void findMajority(int[] arr)
    {
        HashMap<Integer,Integer> map = new HashMap<Integer, Integer>();
        int flag=0;
        for(int i = 0; i < arr.length; i++) {
            if (map.containsKey(arr[i])) {
                    int count = map.get(arr[i]) +1;
                    if (count > arr.length /3) {
                        System.out.print(arr[i]+" ");
                          flag=1;
                    } else
                        map.put(arr[i], count);

            }
            else
                map.put(arr[i],1);
            }
              if(flag==0)
                System.out.println(" No Majority element");
    }

    /* Driver program to test the above functions */
    public static void main(String[] args)
    {
        int a[] = new int[]{2, 2, 3, 1, 3, 2, 1, 1};

        findMajority(a);
    }
}

// This code is contributed by Aman Chowdhury
```

## 蟒蛇 3

```
# Python3 program for finding out majority element in an array
def findMajority(arr, size):
    m = {}
    for i in range(size):
        if arr[i] in m:
            m[arr[i]] += 1
        else:
            m[arr[i]] = 1
    flag = 0
    for i in sorted(m):
        if m[i] > int(size / 3):
            flag =1
            print(i, end = " ")
    if flag == 0:
        print("No Majority element")

arr = [ 2, 2, 3, 1, 3, 2, 1, 1]
n = len(arr)

# Function calling
findMajority(arr, n)

# This code is contributed by rameshtravel07.
```

## C#

```
/* C# program for finding out majority
element in an array */
using System;
using System.Collections.Generic;
class GFG {

    static void findMajority(int[] arr, int size)
    {
        Dictionary<int, int> m = new Dictionary<int, int>();
        for(int i = 0; i < size; i++)
        {
            if(m.ContainsKey(arr[i]))
            {
                m[arr[i]]++;
            }
            else{
                m[arr[i]] = 1;
            }
        }
        int flag = 0;
        List<int> ans = new List<int>();
        foreach(KeyValuePair<int, int> i in m)
        {
            if(i.Value > size / 3)
            {
                flag =1;
                ans.Add(i.Key);
            }
        }
        if(ans.Count > 0)
        {
            ans.Sort();
            for(int i = 0; i < ans.Count; i++)
            {
                Console.Write(ans[i] + " ");
            }
        }
        if(flag == 0)
            Console.WriteLine("No Majority element");
    }

  static void Main() {
    int[] arr = { 2, 2, 3, 1, 3, 2, 1, 1};
    int n = arr.Length;

    // Function calling
    findMajority(arr, n);
  }
}

// This code is contributed by decode2207,
```

**Output**

```
1 2 
```

**复杂度分析:**

*   **时间复杂度:** O(n)需要对数组进行一次遍历，因此时间复杂度为线性。
*   **辅助空间:** O(n)因为散列表需要线性空间。

**<u>方法 3(摩尔投票算法):</u>**

这个想法基于摩尔投票算法。我们先找两个候选人。然后我们检查这两个候选人中是否有任何一个实际上是多数。以下是上述方法的解决方案。

## C++

```
// C++ program to find Majority
// element in an array
#include <bits/stdc++.h>
using namespace std;

// Function to find Majority element
// in an array
void findMajority(int arr[], int n){
      int count1 = 0, count2 = 0;
    int first=INT_MAX, second=INT_MAX;
    int flag=0;
    for (int i = 0; i < n; i++) {

        // if this element is previously seen,
        // increment count1.
        if (first == arr[i])
            count1++;

        // if this element is previously seen,
        // increment count2.
        else if (second == arr[i])
            count2++;

        else if (count1 == 0) {
            count1++;
            first = arr[i];
        }

        else if (count2 == 0) {
            count2++;
            second = arr[i];
        }

        // if current element is different from
        // both the previously seen variables,
        // decrement both the counts.
        else {
            count1--;
            count2--;
        }
    }

    count1 = 0;
    count2 = 0;

    // Again traverse the array and find the
    // actual counts.
    for (int i = 0; i < n; i++) {
        if (arr[i] == first)
            count1++;

        else if (arr[i] == second)
            count2++;
    }

    if (count1 > n / 3){
        cout << first << " ";
          flag=1;
    }
    if (count2 > n / 3){
        cout << second << " ";
          flag=1;
    }
      if(flag==0){
          cout << "No Majority Element" << endl;
    }
}

int main() {

    int arr[] = { 2, 2, 3, 1, 3, 2, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    findMajority(arr, n);

    return 0;
}

// This code is contributed by Aman Chowdhury
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if any element appears
// more than n/3.
class GFG {

    static void findMajority(int arr[], int n)
    {
        int count1 = 0, count2 = 0;
        int flag=0;
        // take the integers as the maximum
        // value of integer hoping the integer
        // would not be present in the array
        int first = Integer.MIN_VALUE;;
        int second = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++) {

            // if this element is previously
            // seen, increment count1.
            if (first == arr[i])
                count1++;

            // if this element is previously
            // seen, increment count2.
            else if (second == arr[i])
                count2++;

            else if (count1 == 0) {
                count1++;
                first = arr[i];
            }

            else if (count2 == 0) {
                count2++;
                second = arr[i];
            }

            // if current element is different
            // from both the previously seen
            // variables, decrement both the
            // counts.
            else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        // Again traverse the array and
        // find the actual counts.
        for (int i = 0; i < n; i++) {
            if (arr[i] == first)
                count1++;

            else if (arr[i] == second)
                count2++;
        }

        if (count1 > n / 3){
            System.out.print(first+" ");
              flag=1;
        }
        if (count2 > n / 3){
            System.out.print(second+" ");
              flag=1;
        }
          if(flag==0)
           System.out.println("No Majority Element");
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 2, 2, 3, 1, 3, 2, 1, 1 };
        int n = arr.length;
        findMajority(arr,n);

    }
}

// This code is contributed by Aman Chowdhury
```

## 蟒蛇 3

```
# Python3 program to find Majority
# element in an array

# Function to find Majority element
# in an array
def findMajority(arr, n):
    count1 = 0
    count2 = 0
    first = 2147483647
    second = 2147483647
    flag = 0
    for i in range(n):

      # if this element is previously seen,
      # increment count1.
      if first == arr[i]:
        count1 += 1

      # if this element is previously seen,
      # increment count2.
      elif second == arr[i]:
        count2 += 1
      elif count1 == 0:
        count1 += 1
        first = arr[i]
      elif count2 == 0:
        count2 += 1
        second = arr[i]

      # if current element is different from
      # both the previously seen variables,
      # decrement both the counts.
      else:
        count1 -= 1
        count2 -= 1

    count1 = 0
    count2 = 0

    # Again traverse the array and find the
    # actual counts.
    for i in range(n):
      if arr[i] == first:
        count1 += 1
      elif arr[i] == second:
        count2 += 1

    if count1 > int(n / 3):
      print(first, end = " ")
      flag = 1
    if count2 > int(n / 3):
      print(second, end = " ")
      flag = 1
    if flag == 0:
      print("No Majority Element")

arr = [ 2, 2, 3, 1, 3, 2, 1, 1 ]
n = len(arr)

# Function calling
findMajority(arr, n)

# This code is contributed by divyesh072019.
```

## C#

```
// C# program to find if any element appears
// more than n/3
using System;
class GFG {

    static void findMajority(int[] arr, int n)
    {
        int count1 = 0, count2 = 0;
        int flag = 0;
        // take the integers as the maximum
        // value of integer hoping the integer
        // would not be present in the array
        int first = Int32.MinValue;
        int second = Int32.MaxValue;

        for (int i = 0; i < n; i++)
        {

            // if this element is previously
            // seen, increment count1.
            if (first == arr[i])
                count1++;

            // if this element is previously
            // seen, increment count2.
            else if (second == arr[i])
                count2++;

            else if (count1 == 0) {
                count1++;
                first = arr[i];
            }

            else if (count2 == 0) {
                count2++;
                second = arr[i];
            }

            // if current element is different
            // from both the previously seen
            // variables, decrement both the
            // counts.
            else {
                count1--;
                count2--;
            }
        }

        count1 = 0;
        count2 = 0;

        // Again traverse the array and
        // find the actual counts.
        for (int i = 0; i < n; i++) {
            if (arr[i] == first)
                count1++;

            else if (arr[i] == second)
                count2++;
        }

        if (count1 > n / 3){
            Console.Write(first+" ");
              flag=1;
        }
        if (count2 > n / 3){
            Console.Write(second+" ");
              flag=1;
        }
          if(flag==0)
           Console.Write("No Majority Element");
    }

  static void Main() {
    int[] arr = { 2, 2, 3, 1, 3, 2, 1, 1 };
    int n = arr.Length;
    findMajority(arr,n);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

      // JavaScript program to find Majority
      // element in an array

      // Function to find Majority element
      // in an array
      function findMajority(arr, n) {
        var count1 = 0,
          count2 = 0;
        var first = 2147483647,
          second = 2147483647;
        var flag = 0;
        for (var i = 0; i < n; i++) {
          // if this element is previously seen,
          // increment count1.
          if (first === arr[i]) count1++;
          // if this element is previously seen,
          // increment count2.
          else if (second === arr[i]) count2++;
          else if (count1 === 0) {
            count1++;
            first = arr[i];
          } else if (count2 === 0) {
            count2++;
            second = arr[i];
          }

          // if current element is different from
          // both the previously seen variables,
          // decrement both the counts.
          else {
            count1--;
            count2--;
          }
        }

        count1 = 0;
        count2 = 0;

        // Again traverse the array and find the
        // actual counts.
        for (var i = 0; i < n; i++) {
          if (arr[i] === first) count1++;
          else if (arr[i] === second) count2++;
        }

        if (count1 > n / 3) {
          document.write(first + " ");
          flag = 1;
        }
        if (count2 > n / 3) {
          document.write(second + " ");
          flag = 1;
        }
        if (flag === 0) {
          document.write("No Majority Element" + "<br>");
        }
      }

      var arr = [2, 2, 3, 1, 3, 2, 1, 1];
      var n = arr.length;

      // Function calling
      findMajority(arr, n);

</script>
```

**Output**

```
2 1 
```

**复杂度分析:**

*   **时间复杂度:** O(n)算法的第一次遍历完成了对 O(n)有贡献的数组，另一个 O(n)用于检查 count1 和 count2 是否大于 floor(n/3)次。
*   **辅助空间:** O(1)由于不需要额外空间，因此空间复杂度不变

**<u>方法四:</u>**

**进场:**解决问题，思路是用[分治](https://www.geeksforgeeks.org/divide-and-conquer/)手法。按照以下步骤解决问题:

1.  初始化一个函数 **majorityElement()** ，该函数将返回数组中从任意索引**左**到**右**的多数元素的计数。
2.  将给定数组 **arr[]** 分成两半，并反复传递给函数 **majorityElement()** 。
3.  将**低电平**和**高电平**分别初始化为 **0** 和**(N–1)**。
4.  使用以下步骤计算多数元素:
    *   **如果低=高:**返回**arr[低]** 作为主要元素。
    *   找到中间指标，说**中间** (= **(低+高)/2** )。
    *   [递归调用**左右子阵列**作为**主元素(arr，低，中)**和**主元素(arr，中+ 1，高)**。](https://www.geeksforgeeks.org/recursion/)
    *   完成上述步骤后，合并两个子阵列并返回多数元素。
5.  只要找到所需的多数元素，就将其追加到结果列表中。
6.  打印列表中存储的所有主要元素。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach
class Solution:

    # Function to find all elements that
    # occurs >= N/3 times in the array
    def majorityElement(self, a):

        # If array is empty return
        # empty list
        if not a:
            return []

        # Function to find the majority
        # element by Divide and Conquer
        def divideAndConquer(lo, hi):
            if lo == hi:
                return [a[lo]]

            # Find mid
            mid = lo + (hi - lo)//2

            # Call to the left half
            left = divideAndConquer(lo, mid)

            # Call to the right half
            right = divideAndConquer(mid + 1, hi)

            # Stores the result
            result = []
            for numbers in left:
                if numbers not in right:
                    result.append(numbers)

            result.extend(right)

            # Stores all majority elements
            ans = []

            for number in result:
                count = 0

                # Count of elements that
                # occurs most
                for index in range(lo, hi + 1):
                    if a[index] == number:
                        count += 1

                # If the number is a
                # majority element
                if count > (hi - lo + 1)//3:
                    ans.append(number)

            # Return the list of element
            return ans

        # Function Call
        print(divideAndConquer(0, len(a) - 1))

# Driver Code
if __name__ == "__main__":

    # Given array a[]
    a = [7, 7, 7, 3, 4, 4, 4, 6]
    object = Solution()

    # Function Call
    object.majorityElement(a)
```

**Output**

```
[7, 4]
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(log N)*

#### 另一种方法:使用内置的 Python 函数:

*   使用 Counter()函数计算每个元素的频率。
*   遍历频率数组，打印出现次数超过 n/3 次的所有元素。

下面是实现:

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import Counter

# Function to find the number of array
# elements with frequency more than n/3 times
def printElements(arr, n):

    # Calculating n/3
    x = n//3

    # Counting frequency of every element using Counter
    mp = Counter(arr)

    # Traverse the map and print all
    # the elements with occurrence atleast n/3 times
    for it in mp:
        if mp[it] > x:
            print(it, end=" ")

# Driver code
arr = [7, 7, 7, 3, 4, 4, 4, 6]

# Size of array
n = len(arr)

# Function Call
printElements(arr, n)

# This code is contributed by vikkycirus
```

**Output**

```
7 4 
```

**时间复杂度:** O(N)

**辅助空间:** O(N)