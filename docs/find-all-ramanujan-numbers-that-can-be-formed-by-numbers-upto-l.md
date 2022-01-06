# 找出所有拉玛努詹数，这些拉玛努詹数可以由直到 L 的数字组成

> 原文:[https://www . geesforgeks . org/find-all-ramanujan-numbers-可由 numbers-up-l 形成的数字/](https://www.geeksforgeeks.org/find-all-ramanujan-numbers-that-can-be-formed-by-numbers-upto-l/)

给定一个正整数 **L** ，任务是找出任意一组四元组 **(a，b，c，d)** 可以生成的所有[拉玛努詹数](https://www.geeksforgeeks.org/taxicab-numbers/)，其中 **0 < a，b，c，d ≤ L** 。

> Ramanujan 数是可以用两种不同方式表示为两个立方体之和的数。
> 因此，拉玛努詹数(N)= a<sup>3</sup>+b<sup>3</sup>= c<sup>3</sup>+d<sup>3</sup>。

**示例:**

> **输入:** L = 20
> **输出:** 1729，4104
> **说明:**
> 数字 1729 可以表示为 12 <sup>3</sup> + 1 <sup>3</sup> 和 10 <sup>3</sup> + 9 <sup>3</sup> 。
> 数字 4104 可以表示为 16 <sup>3</sup> + 2 <sup>3</sup> 和 15 <sup>3</sup> + 9 <sup>3</sup> 。
> 
> **输入:**L = 30
> T3】输出: 1729，4104，13832，20683

**天真方法:**最简单的方法是从由满足等式**a<sup>3</sup>+b<sup>3</sup>= c<sup>3</sup>+d<sup>3</sup>**的不同元素组成的范围**【1，L】**中检查所有四元组的组合 **(a，b，c，d)** 。对于符合条件的元素，将 Ramanujan 编号存储为**<sup>3</sup>+b<sup>3</sup>**。最后，检查所有可能的组合后，打印所有存储的数字。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find Ramanujan numbers
// made up of cubes of numbers up to L
map<int,vector<int>> ramanujan_On4(int limit)
{
    map<int,vector<int>> dictionary;

    // Generate all quadruples a, b, c, d
    // of integers from the range [1, L]
    for(int a = 0; a < limit; a++)
    {
        for(int b = 0; b < limit; b++)
        {
            for(int c = 0; c < limit; c++)
            {
               for(int d = 0; d < limit; d++)
               {

                    // Condition // 2:
                    // a, b, c, d are not equal
                    if ((a != b) and (a != c) and (a != d)
                        and (b != c) and (b != d)
                            and (c != d)){

                        int x = pow(a, 3) + pow(b, 3);
                        int y = pow(c, 3) + pow(d, 3);
                        if ((x) == (y))
                        {
                            int number = pow(a, 3) + pow(b, 3);
                            dictionary[number] = {a, b, c, d};
                        }
                    }
            }
        }
    }
}

    // Return all the possible number
    return dictionary;
}

// Driver Code
int main()
{

// Given range L
int L = 30;
map<int, vector<int>> ra1_dict = ramanujan_On4(L);

// Print all the generated numbers
for(auto x:ra1_dict)
{
    cout << x.first << ": (";

   // sort(x.second.begin(),x.second.end());
    for(int i = x.second.size() - 1; i >= 0; i--)
    {
        if(i == 0)
          cout << x.second[i] << ")";
        else
         cout << x.second[i] << ", ";   
    }
    cout << endl;
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

static Map<Integer, List<Integer>> ra1_dict; 

// Function to find Ramanujan numbers
// made up of cubes of numbers up to L
static void ramanujan_On4(int limit)
{

    // Generate all quadruples a, b, c, d
    // of integers from the range [1, L]
    for(int a = 0; a < limit; a++)
    {
        for(int b = 0; b < limit; b++)
        {
            for(int c = 0; c < limit; c++)
            {
               for(int d = 0; d < limit; d++)
               {

                    // Condition // 2:
                    // a, b, c, d are not equal
                    if ((a != b) && (a != c) && (a != d) &&
                        (b != c) && (b != d) && (c != d))
                    {
                        int x = (int)Math.pow(a, 3) +
                                (int) Math.pow(b, 3);
                        int y = (int)Math.pow(c, 3) +
                                (int) Math.pow(d, 3);
                        if ((x) == (y))
                        {
                            int number = (int)Math.pow(a, 3) +
                                         (int) Math.pow(b, 3);
                            ra1_dict.put(number, new ArrayList<>(
                                Arrays.asList(a, b, c, d)));
                        }
                    }
                }
            }
        }
    }
}

// Driver code
public static void main(String[] args)
{

    // Given range L
    int L = 30;

    ra1_dict = new HashMap<>();

    ramanujan_On4(L);

    // Print all the generated numbers
    for(Map.Entry<Integer,
             List<Integer>> x: ra1_dict.entrySet())
    {
        System.out.print(x.getKey() + ": (");

        // sort(x.second.begin(),x.second.end());
        for(int i = x.getValue().size() - 1; i >= 0; i--)
        {
            if (i == 0)
                System.out.print(x.getValue().get(i) + ")");
            else
                System.out.print(x.getValue().get(i) + ", ");   
        }
        System.out.println();
    }
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach
import time

# Function to find Ramanujan numbers
# made up of cubes of numbers up to L
def ramanujan_On4(limit):
    dictionary = dict()

    # Generate all quadruples a, b, c, d
    # of integers from the range [1, L]
    for a in range(0, limit):
        for b in range(0, limit):
            for c in range(0, limit):
                for d in range(0, limit):

                    # Condition # 2:
                    # a, b, c, d are not equal
                    if ((a != b) and (a != c) and (a != d)
                        and (b != c) and (b != d)
                            and (c != d)):

                        x = a ** 3 + b ** 3
                        y = c ** 3 + d ** 3
                        if (x) == (y):
                            number = a ** 3 + b ** 3
                            dictionary[number] = a, b, c, d

    # Return all the possible number
    return dictionary

# Driver Code

# Given range L
L = 30
ra1_dict = ramanujan_On4(L)

# Print all the generated numbers
for i in sorted(ra1_dict):
    print(f'{i}: {ra1_dict[i]}', end ='\n')
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

       // Function to find Ramanujan numbers
      // made up of cubes of numbers up to L
      function ramanujan_On4(limit) {
        var dictionary = {};

        // Generate all quadruples a, b, c, d
        // of integers from the range [1, L]
        for (var a = 0; a < limit; a++) {
          for (var b = 0; b < limit; b++) {
            for (var c = 0; c < limit; c++) {
              for (var d = 0; d < limit; d++) {
                // Condition // 2:
                // a, b, c, d are not equal
                if (
                  a !== b &&
                  a !== c &&
                  a !== d &&
                  b !== c &&
                  b !== d &&
                  c !== d
                ) {
                  var x = Math.pow(a, 3) + Math.pow(b, 3);
                  var y = Math.pow(c, 3) + Math.pow(d, 3);
                  if (x == y) {
                   var number =
                   Math.pow(a, 3) + Math.pow(b, 3);

                   dictionary[number] =
                   [" " + a, " " + b, " " + c, d];
                  }
                }
              }
            }
          }
        }
        return dictionary;
      }

      // Driver code
      // Given range L
      var L = 30;

      var ra1_dict = ramanujan_On4(L);

      var temp = Object.keys(ra1_dict)
        .sort()
        .reduce((r, k) => ((r[k] = ra1_dict[k]), r), {});
      // Print all the generated numbers
      for (const [key, value] of Object.entries(temp)) {
        document.write(key + ": (" + value.reverse() + ")" +
        "<br>");
      }

</script>
```

**Output:** 

```
1729: (9, 10, 1, 12)
4104: (9, 15, 2, 16)
13832: (18, 20, 2, 24)
20683: (19, 24, 10, 27)
```

***时间复杂度:**O(L<sup>4</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[哈希](https://www.geeksforgeeks.org/data-structure-dictionary-spell-checker/)进行优化。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如**和**，来存储满足给定条件的所有可能的拉玛努詹数。
*   预计算并将范围**【1，L】**中所有数字的立方存储在辅助数组 **arr[]** 中。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，比如说 **M** ，它存储从数组**arr【】**生成的一对立方体的所有可能组合的总和。
*   现在，[生成数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)**arr【】**的所有可能的对(I，j)，如果数组中不存在对的和，则在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中标记当前对的和的出现。否则，将当前总和添加到数组**和**中，因为它是拉马努扬数字之一。
*   完成上述步骤后，打印存储在数组**和**中的数字。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach
from array import *
import time

# Function to find Ramanujan numbers
# made up of cubes of numbers up to L
def ramanujan_On2(limit):
    cubes = array('i', [])

    # Stores the sum of pairs of cubes
    dict_sum_pairs = dict()

    # Stores the Ramanujan Numbers
    dict_ramnujan_nums = dict()
    sum_pairs = 0

    # Stores the cubes from 1 to L
    for i in range(0, limit):
        cubes.append(i ** 3)

    # Generate all pairs (a, b)
    # from the range [0, L]
    for a in range(0, limit):
        for b in range(a + 1, limit):
            a3, b3 = cubes[a], cubes[b]

            # Find the sum of pairs
            sum_pairs = a3 + b3

            # Append to dictionary
            if sum_pairs in dict_sum_pairs:

                # If the current sum is in
                # the dictionary, then store
                # the current number
                c, d = dict_sum_pairs.get(sum_pairs)
                dict_ramnujan_nums[sum_pairs] = a, b, c, d

            # Otherwise append the current
            # sum pairs to the sum pairs
            # dictionary
            else:
                dict_sum_pairs[sum_pairs] = a, b

        # Return the possible Ramanujan
    # Numbers
    return dict_ramnujan_nums

# Driver Code

# Given range L
L = 30
r_dict = ramanujan_On2(L)

# Print all the numbers
for d in sorted(r_dict):
    print(f'{d}: {r_dict[d]}', end ='\n')
```

**Output:** 

```
1729: (9, 10, 1, 12)
4104: (9, 15, 2, 16)
13832: (18, 20, 2, 24)
20683: (19, 24, 10, 27)
```

***时间复杂度:**O(L<sup>2</sup>)*
***辅助空间:** O(L <sup>2</sup> )*