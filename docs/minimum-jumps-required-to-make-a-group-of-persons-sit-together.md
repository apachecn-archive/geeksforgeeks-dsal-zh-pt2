# 一群人坐在一起所需的最小跳跃次数

> 原文:[https://www . geesforgeks . org/最小跳跃-需要一群人坐在一起/](https://www.geeksforgeeks.org/minimum-jumps-required-to-make-a-group-of-persons-sit-together/)

给定一根长度为 **N** 的绳子 **S** ，由**【x】**和**组成**。给定的字符串表示一排座位，其中**‘x’**和**’**分别代表已占用和未占用的座位。任务是最小化跳跃或跳跃的总次数，以使所有乘客坐在一起，即彼此相邻，其间没有任何空位。

**注意:**由于跳数会很大，打印答案取模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** S =。。。。十.x .。x .。”
> **输出:** 5
> **说明:**以下是乘员所需的洗牌:
> **第一步:**使第 5 <sup>位</sup>位的人跳 2 位到第 7 <sup>位</sup>位。
> **第二步:**使第 13<sup>位的人跳 3 位到第 10 <sup>位</sup>位。
> 因此，需要的跳跃总数= 2 + 3 = 5。</sup>
> 
> **输入:**S =“x x x”。。。。。。。x x x x x"
> **输出:** 24
> **说明:**将乘员分别从 1 <sup>st</sup> 、2 <sup>nd</sup> 和 3 <sup>rd</sup> 位置移动到 9 <sup>th</sup> 、10 <sup>th</sup> 、11 <sup>th</sup> 位置。因此，所需的跳跃总数=(11–3)+(10–2)+(9–3)= 24。

**进场:**思路是用一个 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决这个问题。注意，在所有在场人员中，将元素移向[中间元素](https://www.geeksforgeeks.org/median/)总是最佳的。当我们将点转移到中间值时，**的跳跃次数**总是最小的。以下是步骤:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **位置**来存储在场人员的索引。
*   [求向量的中位数](https://www.geeksforgeeks.org/finding-median-of-unsorted-array-in-linear-time-using-c-stl/) **位置[]** 。所有其他人现在将被要求坐在这个人周围，因为这将给出所需的最小跳跃次数。
*   初始化一个变量**和**，存储所需的最小跳跃。
*   现在，[遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **位置[]** ，对于每个索引 **i** 找到中间元素并更新 **ans** 为:

> ans= ans+ abs(位置[I]-中间元素)

*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

long long int MOD = 1e9 + 7;

// Function to find the minimum jumps
// required to make the whole group
// sit adjacently
int minJumps(string seats)
{
    // Store the indexes
    vector<int> position;

    // Stores the count of occupants
    int count = 0;

    // Length of the string
    int len = seats.length();

    // Traverse the seats
    for (int i = 0; i < len; i++) {

        // If current place is occupied
        if (seats[i] == 'x') {

            // Push the current position
            // in the vector
            position.push_back(i - count);
            count++;
        }
    }

    // Base Case:
    if (count == len || count == 0)
        return 0;

    // The index of the median element
    int med_index = (count - 1) / 2;

    // The value of the median element
    int med_val = position[med_index];

    int ans = 0;

    // Traverse the position[]
    for (int i = 0;
         i < position.size(); i++) {

        // Update the ans
        ans = (ans % MOD
               + abs(position[i]
                     - med_val)
                     % MOD)
              % MOD;
    }

    // Return the final count
    return ans % MOD;
}

// Driver Code
int main()
{
    // Given arrange of seats
    string S = "....x..xx...x..";

    // Function Call
    cout << minJumps(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static int MOD = (int)1e9 + 7;

// Function to find the minimum
// jumps required to make the
// whole group sit adjacently
static int minJumps(String seats)
{
  // Store the indexes
  Vector<Integer> position =
                  new Vector<>();

  // Stores the count of
  // occupants
  int count = 0;

  // Length of the String
  int len = seats.length();

  // Traverse the seats
  for (int i = 0; i < len; i++)
  {
    // If current place is occupied
    if (seats.charAt(i) == 'x')
    {
      // Push the current position
      // in the vector
      position.add(i - count);
      count++;
    }
  }

  // Base Case:
  if (count == len ||
      count == 0)
    return 0;

  // The index of the median
  // element
  int med_index = (count - 1) / 2;

  // The value of the median
  // element
  int med_val = position.get(med_index);

  int ans = 0;

  // Traverse the position[]
  for (int i = 0;
           i < position.size(); i++)
  {
    // Update the ans
    ans = (ans % MOD +
           Math.abs(position.get(i) -
                    med_val) % MOD) % MOD;
  }

  // Return the final count
  return ans % MOD;
}

// Driver Code
public static void main(String[] args)
{
  // Given arrange of seats
  String S = "....x..xx...x..";

  // Function Call
  System.out.print(minJumps(S));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach
MOD = 10**9 + 7

# Function to find the minimum jumps
# required to make the whole group
# sit adjacently
def minJumps(seats):

    # Store the indexes
    position = []

    # Stores the count of occupants
    count = 0

    # Length of the string
    lenn = len(seats)

    # Traverse the seats
    for i in range(lenn):

        # If current place is occupied
        if (seats[i] == 'x'):

            # Push the current position
            # in the vector
            position.append(i - count)
            count += 1

    # Base Case:
    if (count == lenn or count == 0):
        return 0

    # The index of the median element
    med_index = (count - 1) // 2

    # The value of the median element
    med_val = position[med_index]

    ans = 0

    # Traverse the position[]
    for i in range(len(position)):

        # Update the ans
        ans = (ans % MOD +
               abs(position[i] - med_val)
               % MOD) % MOD

    # Return the final count
    return ans % MOD

# Driver Code
if __name__ == '__main__':

    # Given arrange of seats
    S = "....x..xx...x.."

    # Function Call
    print(minJumps(S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

static int MOD = (int)1e9 + 7;

// Function to find the minimum
// jumps required to make the
// whole group sit adjacently
static int minJumps(String seats)
{
  // Store the indexes
  List<int> position =
       new List<int>();

  // Stores the count of
  // occupants
  int count = 0;

  // Length of the String
  int len = seats.Length;

  // Traverse the seats
  for (int i = 0; i < len; i++)
  {
    // If current place is
    // occupied
    if (seats[i] == 'x')
    {
      // Push the current
      // position in the
      // vector
      position.Add(i - count);
      count++;
    }
  }

  // Base Case:
  if (count == len ||
      count == 0)
    return 0;

  // The index of the median
  // element
  int med_index = (count - 1) / 2;

  // The value of the median
  // element
  int med_val = position[med_index];

  int ans = 0;

  // Traverse the position[]
  for (int i = 0;
           i < position.Count; i++)
  {
    // Update the ans
    ans = (ans % MOD +
           Math.Abs(position[i] -
           med_val) % MOD) % MOD;
  }

  // Return the readonly
  // count
  return ans % MOD;
}

// Driver Code
public static void Main(String[] args)
{
  // Given arrange of seats
  String S = "....x..xx...x..";

  // Function Call
  Console.Write(minJumps(S));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach
let MOD = 1e9 + 7;

// Function to find the minimum jumps
// required to make the whole group
// sit adjacently
function minJumps(seats)
{
    // Store the indexes
    let position = [];

    // Stores the count of occupants
    let count = 0;

    // Length of the string
    let len = seats.length;

    // Traverse the seats
    for(let i = 0; i < len; i++)
    {

        // If current place is occupied
        if (seats[i] == 'x')
        {

            // Push the current position
            // in the vector
            position.push(i - count);
            count++;
        }
    }

    // Base Case:
    if (count == len || count == 0)
        return 0;

    // The index of the median element
    let med_index = parseInt((count - 1) / 2, 10);

    // The value of the median element
    let med_val = position[med_index];

    let ans = 0;

    // Traverse the position[]
    for(let i = 0; i < position.length; i++)
    {

        // Update the ans
        ans = (ans % MOD + Math.abs(position[i] -
          med_val) % MOD) % MOD;
    }

    // Return the final count
    return ans % MOD;
}

// Driver code

// Given arrange of seats
let S = "....x..xx...x..";

// Function Call
document.write(minJumps(S));

// This code is contributed by suresh07

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)