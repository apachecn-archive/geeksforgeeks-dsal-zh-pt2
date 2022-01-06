# 在 Array 中找到一对第二大的产品

> 原文:[https://www . geesforgeks . org/find-a-pair-in-array-with-第二大产品/](https://www.geeksforgeeks.org/find-a-pair-in-array-with-second-largest-product/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **N > 2** ，任务是从给定数组中找到第二大乘积对。

**示例:**

> **输入:** arr[] = {10，20，12，40，50}
> **输出:** 20 50
> **解释:**
> 一对数组元素= [(10，20)，(10，12)，(10，40)，(10，50)，(20，12)，(20，40)，(20，50)，(12，40)，(12，50)，(40，50)]
> 
> **输入:** arr[] = {5，2，67，45，160，78}
> **输出:** 67 160

**天真方法:**天真方法是[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并将带有对的产品插入到对的[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。将所有配对产品插入器械包后，打印器械包的第二个也是最后一个产品。以下是步骤:

1.  按照给定的数组制作一组[对](https://www.geeksforgeeks.org/sets-of-pairs-in-c/)及其产品。
2.  将所有对插入成对向量中。
3.  如果向量大小为 1，则打印该对，否则在向量的第**(总向量大小–2)个**位置打印该对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find second largest
// product of pairs
void secondLargerstPair(int arr[], int N)
{

    // If size of array is less then 3
    // then second largest product pair
    // does not exits.
    if (N < 3)
        return;

    // Declaring set of pairs which
    // contains possible pairs of array
    // and their products
    set<pair<int, pair<int, int> > > s;

    // Declaring vector of pairs
    vector<pair<int, int> > v;

    for (int i = 0; i < N; ++i) {

        for (int j = i + 1; j < N; ++j) {

            // Inserting a set
            s.insert(make_pair(arr[i] * arr[j],
                               make_pair(arr[i],
                                         arr[j])));
        }
    }

    // Traverse set of pairs
    for (auto i : s) {

        // Inserting values in vector
        // of pairs
        v.push_back(
            make_pair((i.second).first,
                      (i.second).second));
    }

    int vsize = v.size();

    // Printing the result
    cout << v[vsize - 2].first << " "
         << v[vsize - 2].second << endl;
}

// Driver Code
int main()
{
    // Given Array
    int arr[] = { 5, 2, 67, 45, 160, 78 };

    // Size of Array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    secondLargerstPair(arr, N);
    return 0;
}
```

**Output:** 

```
67 160
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**更好的解决方案:**更好的解决方案是遍历数组的所有对，同时遍历存储最大和第二大的产品对。遍历后，打印存储了第二大对的对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find second largest
// product pair in arr[0..n-1]
void maxProduct(int arr[], int N)
{
    // No pair exits
    if (N < 3) {
        return;
    }

    // Initialize max product pair
    int a = arr[0], b = arr[1];
    int c = 0, d = 0;

    // Traverse through every possible pair
    // and keep track of largest product
    for (int i = 0; i < N; i++)
        for (int j = i + 1; j < N; j++) {

            // If pair is largest
            if (arr[i] * arr[j] > a * b) {

                // Second largest
                c = a, d = b;
                a = arr[i], b = arr[j];
            }

            // If pair does not largest but
            // larger then second largest
            if (arr[i] * arr[j] < a * b
                && arr[i] * arr[j] > c * d)
                c = arr[i], d = arr[j];
        }

    // Print the pairs
    cout << c << " " << d;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 5, 2, 67, 45, 160, 78 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxProduct(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find second largest
// product pair in arr[0..n-1]
static void maxProduct(int arr[], int N)
{
    // No pair exits
    if (N < 3)
    {
        return;
    }

    // Initialize max product pair
    int a = arr[0], b = arr[1];
    int c = 0, d = 0;

    // Traverse through every possible pair
    // and keep track of largest product
    for (int i = 0; i < N; i++)
        for (int j = i + 1; j < N-1; j++)
        {

            // If pair is largest
            if (arr[i] * arr[j] > a * b)
            {

                // Second largest
                c = a;
                d = b;
                a = arr[i];
                b = arr[j];
            }

            // If pair does not largest but
            // larger then second largest
            if (arr[i] * arr[j] < a * b &&
                arr[i] * arr[j] > c * d)
                c = arr[i];
                d = arr[j];
        }

    // Print the pairs
    System.out.println(c + " " + d);
}

// Driver Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 5, 2, 67, 45, 160, 78 };
    int N = arr.length;

    // Function Call
    maxProduct(arr, N);
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find second largest
# product pair in arr[0..n-1]
def maxProduct(arr, N):

    # No pair exits
    if (N < 3):
        return;

    # Initialize max product pair
    a = arr[0]; b = arr[1];
    c = 0; d = 0;

    # Traverse through every possible pair
    # and keep track of largest product
    for i in range(0, N, 1):
        for j in range(i + 1, N - 1, 1):

            # If pair is largest
            if (arr[i] * arr[j] > a * b):

                # Second largest
                c = a;
                d = b;
                a = arr[i];
                b = arr[j];

            # If pair does not largest but
            # larger then second largest
            if (arr[i] * arr[j] < a * b and
                arr[i] * arr[j] > c * d):
                c = arr[i];

            d = arr[j];

    # Print the pairs
    print(c, " ", d);

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 5, 2, 67, 45, 160, 78];
    N = len(arr);

    # Function call
    maxProduct(arr, N);

# This code is contributed by Amit Katiyar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find second largest
// product pair in arr[0..n-1]
static void maxProduct(int []arr, int N)
{

    // No pair exits
    if (N < 3)
    {
        return;
    }

    // Initialize max product pair
    int a = arr[0], b = arr[1];
    int c = 0, d = 0;

    // Traverse through every possible pair
    // and keep track of largest product
    for(int i = 0; i < N; i++)
        for(int j = i + 1; j < N - 1; j++)
        {

            // If pair is largest
            if (arr[i] * arr[j] > a * b)
            {

                // Second largest
                c = a;
                d = b;
                a = arr[i];
                b = arr[j];
            }

            // If pair does not largest but
            // larger then second largest
            if (arr[i] * arr[j] < a * b &&
                arr[i] * arr[j] > c * d)
                c = arr[i];
                d = arr[j];
        }

    // Print the pairs
    Console.WriteLine(c + " " + d);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 5, 2, 67, 45, 160, 78 };
    int N = arr.Length;

    // Function call
    maxProduct(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find second largest
// product pair in arr[0..n-1]
function maxProduct(arr, N)
{
    // No pair exits
    if (N < 3) {
        return;
    }

    // Initialize max product pair
    let a = arr[0], b = arr[1];
    let c = 0, d = 0;

    // Traverse through every possible pair
    // and keep track of largest product
    for (let i = 0; i < N; i++)
        for (let j = i + 1; j < N; j++) {

            // If pair is largest
            if (arr[i] * arr[j] > a * b) {

                // Second largest
                c = a, d = b;
                a = arr[i], b = arr[j];
            }

            // If pair does not largest but
            // larger then second largest
            if (arr[i] * arr[j] < a * b
                && arr[i] * arr[j] > c * d)
                c = arr[i], d = arr[j];
        }

    // Print the pairs
    document.write(c + " " + d);
}

// Driver Code
    // Given array
    let arr = [ 5, 2, 67, 45, 160, 78 ];
    let N = arr.length;

    // Function Call
    maxProduct(arr, N);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
67 160
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**

1.  [排序](https://www.geeksforgeeks.org/sorting-algorithms/)数组。
2.  查找处理负数的第一个和第三个最小元素。
3.  找出处理正数的第一和第三大元素。
4.  比较最小对和最大对的乘积。
5.  归还其中最大的一个。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find second largest
// product pair in arr[0..n-1]
void maxProduct(int arr[], int N)
{
    // No pair exits
    if (N < 3) {
        return;
    }

    // Sort the array
    sort(arr, arr + N);

    // Initialize smallest element
    // of the array
    int smallest1 = arr[0];
    int smallest3 = arr[2];

    // Initialize largest element
    // of the array
    int largest1 = arr[N - 1];
    int largest3 = arr[N - 3];

    // Print second largest product pair
    if (smallest1 * smallest3
        >= largest1 * largest3) {
        cout << smallest1 << " " << smallest3;
    }
    else {
        cout << largest1 << " " << largest3;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 5, 2, 67, 45, 160, 78 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxProduct(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find second largest
// product pair in arr[0..n-1]
static void maxProduct(int arr[], int N)
{
    // No pair exits
    if (N < 3)
    {
        return;
    }

    // Sort the array
    Arrays.sort(arr);

    // Initialize smallest element
    // of the array
    int smallest1 = arr[0];
    int smallest3 = arr[2];

    // Initialize largest element
    // of the array
    int largest1 = arr[N - 1];
    int largest3 = arr[N - 3];

    // Print second largest product pair
    if (smallest1 * smallest3 >=
        largest1 * largest3)
    {
        System.out.print(smallest1 + " " +
                         smallest3);
    }
    else
    {
        System.out.print(largest1 + " " + 
                         largest3);
    }
}

// Driver Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 5, 2, 67, 45, 160, 78 };

    int N = arr.length;

    // Function Call
    maxProduct(arr, N);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find second largest
# product pair in arr[0..n-1]
def maxProduct(arr, N):

    # No pair exits
    if (N < 3):
        return;

    # Sort the array
    arr.sort();

    # Initialize smallest element
    # of the array
    smallest1 = arr[0];
    smallest3 = arr[2];

    # Initialize largest element
    # of the array
    largest1 = arr[N - 1];
    largest3 = arr[N - 3];

    # Prsecond largest product pair
    if (smallest1 *
        smallest3 >= largest1 *
                     largest3):
        print(smallest1 , " " , smallest3);
    else:
        print(largest1 , " " , largest3);

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [5, 2, 67, 45, 160, 78];

    N = len(arr);

    # Function Call
    maxProduct(arr, N);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find second largest
// product pair in arr[0..n-1]
static void maxProduct(int []arr, int N)
{
    // No pair exits
    if (N < 3)
    {
        return;
    }

    // Sort the array
    Array.Sort(arr);

    // Initialize smallest element
    // of the array
    int smallest1 = arr[0];
    int smallest3 = arr[2];

    // Initialize largest element
    // of the array
    int largest1 = arr[N - 1];
    int largest3 = arr[N - 3];

    // Print second largest product pair
    if (smallest1 * smallest3 >=
        largest1 * largest3)
    {
        Console.Write(smallest1 + " " +
                      smallest3);
    }
    else
    {
        Console.Write(largest1 + " " + 
                      largest3);
    }
}

// Driver Code
public static void Main(String[] args)
{
    // Given array
    int []arr = { 5, 2, 67, 45, 160, 78 };

    int N = arr.Length;

    // Function Call
    maxProduct(arr, N);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find second largest
// product pair in arr[0..n-1]
function maxProduct(arr, N)
{
    // No pair exits
    if (N < 3)
    {
        return;
    }

    // Sort the array
    arr.sort((a, b) => a - b)

    // Initialize smallest element
    // of the array
    let smallest1 = arr[0];
    let smallest3 = arr[2];

    // Initialize largest element
    // of the array
    let largest1 = arr[N - 1];
    let largest3 = arr[N - 3];

    // Prlet second largest product pair
    if (smallest1 * smallest3 >=
        largest1 * largest3)
    {
        document.write(smallest1 + " " +
                         smallest3);
    }
    else
    {
        document.write(largest1 + " " +
                         largest3);
    }
}

// Driver Code

       // Given array
    let arr = [ 5, 2, 67, 45, 160, 78 ];

    let N = arr.length;

    // Function Call
    maxProduct(arr, N);

</script>
```

**Output:** 

```
160 67
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*