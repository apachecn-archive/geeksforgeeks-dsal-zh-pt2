# 和二小于数组和的子序列计数

> 原文:[https://www . geeksforgeeks . org/sum 比数组 sum 少两个子序列的计数/](https://www.geeksforgeeks.org/count-of-subsequences-with-sum-two-less-than-the-array-sum/)

给定一个非负整数大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **vec[]** 。任务是计算[子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，其和等于**S–2**，其中 **S** 是数组所有元素的[和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)。

**示例:**

> **输入:** vec[] = {2，0，1，2，1}，N=5
> **输出:** 6
> **解释:** {2，0，1，1}，{2，1，1}，{2，0，2}，{2，2}，{0，1，2，1}，{1，2，1}
> 
> **输入:** vec[] = {2，0，2，3，1}，N=5
> **输出:** 4
> **解释:** {2，0，3，1}，{2，3，1}，{0，2，3，1}，{2，3，1}

**天真方法:**想法是[生成所有子序列](http://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)并检查每个子序列的和是否等于 **S-2** 。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the total number
// of subsequences with sum S-2
void countTotal(vector<int>& vec)
{

    // Calculating vector sum using
    // accumulate function
    int sum = accumulate(vec.begin(),
                         vec.end(), 0LL);

    int N = (int)vec.size();

    // Answer variable stores count
    // of subsequences with desired sum
    int answer = 0;

    // Bitmasking technique to generate
    // all possible subsequences
    for (int mask = 0; mask < (1 << N); mask++) {

        // Variable curr counts the
        // sum of the current subsequence
        int curr = 0;
        for (int i = 0; i < N; i++) {

            if ((mask & (1 << i)) != 0) {

                // Include ith element
                // of the vector
                curr += vec[i];
            }
        }

        if (curr == sum - 2)
            answer++;
    }

    // Print the answer
    cout << answer;
}

// Driver Code
int main()
{

    // Initializing a vector
    vector<int> vec = { 2, 0, 1, 2, 1 };

    countTotal(vec);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    static int accumulate(int [] vec){
        int sum1 = 0;

        for (int i = 0; i < vec.length; i++)
            sum1 += vec[i];
    return sum1;
    }

    // Function to count the total number
    // of subsequences with sum S-2
    static void countTotal(int []vec)
    {

        // Calculating vector sum using
        // accumulate function
        int sum = accumulate(vec);

        int N = vec.length;

        // Answer variable stores count
        // of subsequences with desired sum
        int answer = 0;

        // Bitmasking technique to generate
        // all possible subsequences
        for (int mask = 0; mask < (1 << N); mask++) {

            // Variable curr counts the
            // sum of the current subsequence
            int curr = 0;
            for (int i = 0; i < N; i++) {

                if ((mask & (1 << i)) != 0) {

                    // Include ith element
                    // of the vector
                    curr += vec[i];
                }
            }

            if (curr == sum - 2)
                answer++;
        }

        // Print the answer
        System.out.print(answer);
    }

    // Driver Code
    public static void main (String[] args)
    {

        // Initializing a vector
        int []vec = { 2, 0, 1, 2, 1 };

        countTotal(vec);
    }

}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python3 program for the above approach

# Function to count the total number
# of subsequences with sum S-2
def countTotal(vec) :

    # Calculating vector sum using
    # accumulate function
    Sum = sum(vec)

    N = len(vec);

    # Answer variable stores count
    # of subsequences with desired sum
    answer = 0;

    # Bitmasking technique to generate
    # all possible subsequences
    for mask in range((1 << N)) :

        # Variable curr counts the
        # sum of the current subsequence
        curr = 0;
        for i in range(N) :

            if ((mask & (1 << i)) != 0) :

                # Include ith element
                # of the vector
                curr += vec[i];

        if (curr == Sum - 2) :
            answer += 1;

    # Print the answer
    print(answer);

# Driver Code
if __name__ == "__main__" :

    # Initializing a vector
    vec = [ 2, 0, 1, 2, 1 ];

    countTotal(vec);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    static int accumulate(int[] vec)
    {
        int sum1 = 0;

        for (int i = 0; i < vec.Length; i++)
            sum1 += vec[i];
        return sum1;
    }

    // Function to count the total number
    // of subsequences with sum S-2
    static void countTotal(int[] vec)
    {

        // Calculating vector sum using
        // accumulate function
        int sum = accumulate(vec);

        int N = vec.Length;

        // Answer variable stores count
        // of subsequences with desired sum
        int answer = 0;

        // Bitmasking technique to generate
        // all possible subsequences
        for (int mask = 0; mask < (1 << N); mask++) {

            // Variable curr counts the
            // sum of the current subsequence
            int curr = 0;
            for (int i = 0; i < N; i++) {

                if ((mask & (1 << i)) != 0) {

                    // Include ith element
                    // of the vector
                    curr += vec[i];
                }
            }

            if (curr == sum - 2)
                answer++;
        }

        // Print the answer
        Console.WriteLine(answer);
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Initializing a vector
        int[] vec = { 2, 0, 1, 2, 1 };

        countTotal(vec);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the total number
// of subsequences with sum S-2
function countTotal(vec) {

  // Calculating vector sum using
  // accumulate function
  let sum = vec.reduce((acc, curr) => acc + curr, 0)

  let N = vec.length;

  // Answer variable stores count
  // of subsequences with desired sum
  let answer = 0;

  // Bitmasking technique to generate
  // all possible subsequences
  for (let mask = 0; mask < (1 << N); mask++) {

    // Variable curr counts the
    // sum of the current subsequence
    let curr = 0;
    for (let i = 0; i < N; i++) {

      if ((mask & (1 << i)) != 0) {

        // Include ith element
        // of the vector
        curr += vec[i];
      }
    }

    if (curr == sum - 2)
      answer++;
  }

  // Print the answer
  document.write(answer);
}

// Driver Code

// Initializing a vector
let vec = [2, 0, 1, 2, 1];

countTotal(vec);

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
6
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**有效方法:**想法是使用[组合学](https://www.geeksforgeeks.org/combinatorics-gq/)，除了**的 0、1、**和**的 2**之外，我们数组中的所有其他元素都将是所需子序列的一部分。让我们称它们为额外元素。然后，统计数组中 **0、1、**和**2**的出现次数。假设 **0 的**的计数是 **x** ，1 的 **1 的计数是 **y** ，2 的**的计数是 **z** 。

> *   If all 2 and extra elements are in subsequences, let's calculate the number of required subsequences. There can be exactly y–2 elements in y now. Note that there is no limit to taking 0, because it has no contribution to our subsequence sum.
> *   因此,这些子序列的总数= count 1 = 2<sup>x</sup>×<sup>y</sup>C<sub>y–2</sub>= 2<sup>x</sup>×<sup>y</sup>C<sub>2</sub>(自，<sup>n</sup>C<sub>0</sub>+<sup>n</sup>C<sub>1</sub>+.
> *   If all 1s are in our subsequences, let's calculate the number of subsequences. There can be exactly z–1 elements in z now.
> *   Therefore, the total number of such subsequences = count2 = 2 <sup>x</sup> × <sup>z</sup> c <sub>z–1</sub> = 2 <sup>x</sup> × <sub><sup>z</sup> c <sub>1 [</sub></sub>

按照以下步骤解决问题:

*   将变量**和**初始化为数组的和。
*   将变量**答案**初始化为 **0** 存储答案。
*   初始化变量**的零计数、一个**的计数和两个的**计数，以存储 **0、1** 和 **2 的计数。****
*   [使用迭代器 **x** 遍历数组](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **vec[]** ，并执行以下任务:
    *   计算 **0、1**和**2**的出现次数
*   将变量**值 1** 初始化为 **2 <sup>零计数</sup>。**
*   将变量**值 2** 初始化为**(countOfOne *(countOfOne–1))/2**。
*   将变量**值 3** 初始化为**计数 2。**
*   将**答案**的值设置为**值 1 *(值 2 +值)。**
*   执行上述步骤后，打印**答案**的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the total number
// of subsequences with sum S-2
void countTotal(vector<int>& vec)
{

    // Calculating vector sum using
    // accumulate function
    int sum = accumulate(vec.begin(),
                         vec.end(), 0LL);

    int N = (int)vec.size();

    // Answer variable stores count
    // of subsequences with desired sum
    int answer = 0;

    int countOfZero = 0,
        countOfOne = 0,
        countOfTwo = 0;
    for (auto x : vec) {
        if (x == 0)
            countOfZero++;
        else if (x == 1)
            countOfOne++;
        else if (x == 2)
            countOfTwo++;
    }

    // Select any number of
    // zeroes from 0 to count[0]
    // which is equivalent
    // to 2 ^ countOfZero
    int value1 = pow(2, countOfZero);

    // Considering all 2's
    // and extra elements
    int value2
        = (countOfOne
           * (countOfOne - 1))
          / 2;

    // Considering all 1's
    // and extra elements
    int value3 = countOfTwo;

    // Calculating final answer
    answer = value1 * (value2 + value3);

    // Print the answer
    cout << answer;
}

// Driver Code
int main()
{

    // Initializing a vector
    vector<int> vec = { 2, 0, 1, 2, 1 };

    countTotal(vec);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG {
    // Function to count the total number
    // of subsequences with sum S-2
    static void countTotal(int[] arr)
    {

        int N = arr.length;

        // Answer variable stores count
        // of subsequences with desired sum
        int answer = 0;

        int countOfZero = 0, countOfOne = 0, countOfTwo = 0;
        for (int i = 0; i < N; i++) {

            if (arr[i] == 0)
                countOfZero++;
            else if (arr[i] == 1)
                countOfOne++;
            else if (arr[i] == 2)
                countOfTwo++;
        }

        // Select any number of
        // zeroes from 0 to count[0]
        // which is equivalent
        // to 2 ^ countOfZero
        int value1 = (1 << countOfZero);

        // Considering all 2's
        // and extra elements
        int value2 = (countOfOne * (countOfOne - 1)) / 2;

        // Considering all 1's
        // and extra elements
        int value3 = countOfTwo;

        // Calculating final answer
        answer = value1 * (value2 + value3);

        // Print the answer
        System.out.println(answer);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Initializing an array
        int[] arr = { 2, 0, 1, 2, 1 };

        countTotal(arr);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the total number
# of subsequences with sum S-2
def countTotal(vec) :

    # Calculating vector sum using
    # accumulate function
    sum1 = sum(vec);

    N = len(vec);

    # Answer variable stores count
    # of subsequences with desired sum
    answer = 0;
    countOfZero = 0; countOfOne = 0; countOfTwo = 0;
    for x in vec :

        if (x == 0) :
            countOfZero += 1;

        elif (x == 1) :
            countOfOne += 1;

        elif (x == 2) :
            countOfTwo += 1;

    # Select any number of
    # zeroes from 0 to count[0]
    # which is equivalent
    # to 2 ^ countOfZero
    value1 = 2 ** countOfZero;

    # Considering all 2's
    # and extra elements
    value2 = (countOfOne * (countOfOne - 1)) // 2;

    # Considering all 1's
    # and extra elements
    value3 = countOfTwo;

    # Calculating final answer
    answer = value1 * (value2 + value3);

    # Print the answer
    print(answer);

# Driver Code
if __name__ == "__main__" :

    # Initializing a vector
    vec = [ 2, 0, 1, 2, 1 ];
    countTotal(vec);

    # This code is contributed by AnkThon
```

## C#

```
// Above approach implemented in C#
using System;

public class GFG {

    // Function to count the total number
    // of subsequences with sum S-2
    static void countTotal(int[] arr)
    {

        int N = arr.Length;

        // Answer variable stores count
        // of subsequences with desired sum
        int answer = 0;

        int countOfZero = 0, countOfOne = 0, countOfTwo = 0;
        for (int i = 0; i < N; i++) {

            if (arr[i] == 0)
                countOfZero++;

            else if (arr[i] == 1)
                countOfOne++;

            else if (arr[i] == 2)
                countOfTwo++;
        }

        // Select any number of
        // zeroes from 0 to count[0]
        // which is equivalent
        // to 2 ^ countOfZero
        int value1 = (1 << countOfZero);

        // Considering all 2's
        // and extra elements
        int value2 = (countOfOne * (countOfOne - 1)) / 2;

        // Considering all 1's
        // and extra elements
        int value3 = countOfTwo;

        // Calculating final answer
        answer = value1 * (value2 + value3);

        // Print the answer
        Console.WriteLine(answer);
    }

    // Driver Code
    public static void Main(string[] args)
    {

        // Initializing an array
        int[] arr = { 2, 0, 1, 2, 1 };

        countTotal(arr);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to count the total number
       // of subsequences with sum S-2
       function countTotal(vec)
       {

           // Calculating vector sum using
           // accumulate function
           let sum = vec.reduce(function (accumulator, currentValue) {
               return accumulator + currentValue;
           }, 0);

           let N = vec.length;

           // Answer variable stores count
           // of subsequences with desired sum
           let answer = 0;

           let countOfZero = 0,
               countOfOne = 0,
               countOfTwo = 0;
           for (let x of vec) {
               if (x == 0)
                   countOfZero++;
               else if (x == 1)
                   countOfOne++;
               else if (x == 2)
                   countOfTwo++;
           }

           // Select any number of
           // zeroes from 0 to count[0]
           // which is equivalent
           // to 2 ^ countOfZero
           let value1 = Math.pow(2, countOfZero);

           // Considering all 2's
           // and extra elements
           let value2
               = (countOfOne
                   * (countOfOne - 1))
               / 2;

           // Considering all 1's
           // and extra elements
           let value3 = countOfTwo;

           // Calculating final answer
           answer = value1 * (value2 + value3);

           // Print the answer
           document.write(answer);
       }

       // Driver Code
       // Initializing a vector
       let vec = [2, 0, 1, 2, 1];

       countTotal(vec);

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)