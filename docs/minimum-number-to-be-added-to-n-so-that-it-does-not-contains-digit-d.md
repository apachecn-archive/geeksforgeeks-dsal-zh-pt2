# 要加到 N 上的最小数字，使其不包含数字 D

> 原文:[https://www . geeksforgeeks . org/最小 n 加数不含数字 d/](https://www.geeksforgeeks.org/minimum-number-to-be-added-to-n-so-that-it-does-not-contains-digit-d/)

给定一个正整数 **N** 和一个数字 **D** ，任务是找到最小的**非负数**需要**加**到给定的数字，这样相加后，结果数**不应该包含**数字 **D** 。

**示例:**

> **输入:** N = 25，D = 2
> **输出:** 5
> **说明:**数字 30 是 25 之后的最小数字，不包含数字 2。因此，必须将所需的数字加到 25 才能去掉数字 2，即 30–25 = 5
> 
> **输入:** N = 100，D = 0
> **输出:** 11
> **说明:**数字 111 是100 之后的最小数字，没有数字 0。所以需要的数字必须加到 100 才能去掉，数字 0 是 111–100 = 11

****方法:**这个问题可以通过从右向左迭代给定数字的位数，找到不包含数字 d 的最近位数来解决。**

**遵循以下步骤:**

*   **迭代给定的数字，检查数字中是否有给定的数字。**
*   **如果**当前数字与给定数字匹配**，则**检查以下条件**:

    *   如果当前数字在 **1 至 9** 的范围内，则**将当前数字**增加 1** ，并使其右边的**所有数字为 0** 。**
    *   否则，如果当前数字为 **0** ，则**将当前数字**增加 1** 并使其右边的**所有数字为 1****** 
*   **使用上述条件形成的数字与原始数字之间的**差是所需的最小数字。****

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate smallest positive
// number to be added to remove
// the given digit
int smallestNumber(int n, int d)
{
    // Copy the number to another variable
    int temp = n;

    int ans = 0, count = 0;

    // Iterate over digits of the given
    // number from right to left
    while (temp > 0) {

        // Extract the last digit of the
        // number and check if it is
        // equal to the given digit (d)
        int remainder = temp % 10;
        temp = temp / 10;
        count++;

        if (remainder == d) {
            // If the digit which
            // need to be replaced
            // is equal to 0 then
            // increment the current
            // digit and make the all digits
            // to its right 1
            if (d == 0) {

                string num = string(count, '1');

                temp = temp * pow(10, count) + stoi(num);
            }

            // Else, increment the current digit
            // by 1 and make the all digits
            // to its right 0
            else {

                temp = temp * pow(10, count)
                       + (remainder + 1)
                             * pow(10, count - 1);
            }
            // After the removal of given
            // digit the number will be temp
            // So, the required smallest
            // number is (temp - n)
            ans = temp - n;

            // Set count as 0
            count = 0;
        }
    }

    // Return the result
    return ans;
}

// Driver code
int main()
{
    int N = 100;
    int D = 0;

    // print the smallest number required
    // to be added to remove
    // the digit 'D' in number 'N'
    cout << smallestNumber(N, D) << "\n";

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
class GFG{

// Function to calculate smallest positive
// number to be added to remove
// the given digit
public static int smallestNumber(int n, int d)
{

    // Copy the number to another variable
    int temp = n;

    int ans = 0, count = 0;

    // Iterate over digits of the given
    // number from right to left
    while (temp > 0)
    {

        // Extract the last digit of the
        // number and check if it is
        // equal to the given digit (d)
        int remainder = temp % 10;
        temp = temp / 10;
        count++;

        if (remainder == d)
        {

            // If the digit which need to be
            // replaced is equal to 0 then
            // increment the current digit
            // and make the all digits to
            // its right 1
            if (d == 0)
            {
                String num = "";
                for(int i = 0; i < count; i++)
                {
                    num = num + "1";
                }
                temp = (int)(temp * Math.pow(10, count) +
                       Integer.parseInt(num));
            }

            // Else, increment the current digit
            // by 1 and make the all digits
            // to its right 0
            else
            {
                temp = (int) (temp * Math.pow(10, count) +
                   (remainder + 1) * Math.pow(10, count - 1));
            }

            // After the removal of given
            // digit the number will be temp
            // So, the required smallest
            // number is (temp - n)
            ans = temp - n;

            // Set count as 0
            count = 0;
        }
    }

    // Return the result
    return ans;
}

// Driver code
public static void main(String args[])
{
    int N = 100;
    int D = 0;

    // Print the smallest number required
    // to be added to remove the digit 'D'
    // in number 'N'
    System.out.println(smallestNumber(N, D));
}
}

// This code is contributed by _saurabh_jaiswal
```

## **蟒蛇 3**

```
# Python 3 implementation of the above approach

# Function to calculate smallest positive
# number to be added to remove
# the given digit
def smallestNumber(n, d):

    # Copy the number to another variable
    temp = n

    ans = 0
    count = 0

    # Iterate over digits of the given
    # number from right to left
    while (temp > 0):

        # Extract the last digit of the
        # number and check if it is
        # equal to the given digit (d)
        remainder = temp % 10
        temp = temp // 10
        count += 1

        if (remainder == d):
            # If the digit which
            # need to be replaced
            # is equal to 0 then
            # increment the current
            # digit and make the all digits
            # to its right 1
            if (d == 0):

                num = '1'*count
                temp = temp * pow(10, count) + int(num)

            # Else, increment the current digit
            # by 1 and make the all digits
            # to its right 0
            else:

                temp = (temp * pow(10, count) + (remainder + 1)
                             * pow(10, count - 1))

            # After the removal of given
            # digit the number will be temp
            # So, the required smallest
            # number is (temp - n)
            ans = temp - n

            # Set count as 0
            count = 0

    # Return the result
    return ans

# Driver code
if __name__ == "__main__":

    N = 100
    D = 0

    # print the smallest number required
    # to be added to remove
    # the digit 'D' in number 'N'
    print(smallestNumber(N, D))

    # This code is contributed by ukasp.
```

## **C#**

```
// C# implementation for the above approach
using System;

class GFG {

  // Function to calculate smallest positive
  // number to be added to remove
  // the given digit
  public static int smallestNumber(int n, int d)
  {

    // Copy the number to another variable
    int temp = n;

    int ans = 0, count = 0;

    // Iterate over digits of the given
    // number from right to left
    while (temp > 0)
    {

      // Extract the last digit of the
      // number and check if it is
      // equal to the given digit (d)
      int remainder = temp % 10;
      temp = temp / 10;
      count++;

      if (remainder == d)
      {

        // If the digit which need to be
        // replaced is equal to 0 then
        // increment the current digit
        // and make the all digits to
        // its right 1
        if (d == 0)
        {
          string num = "";
          for(int i = 0; i < count; i++)
          {
            num = num + "1";
          }
          temp = (int)(temp * Math.Pow(10, count) +
                       Int32.Parse(num));
        }

        // Else, increment the current digit
        // by 1 and make the all digits
        // to its right 0
        else
        {
          temp = (int) (temp * Math.Pow(10, count) +
                        (remainder + 1) * Math.Pow(10, count - 1));
        }

        // After the removal of given
        // digit the number will be temp
        // So, the required smallest
        // number is (temp - n)
        ans = temp - n;

        // Set count as 0
        count = 0;
      }
    }

    // Return the result
    return ans;
  }

  // Driver code
  public static void Main(String[] args)
  {

    int N = 100;
    int D = 0;

    // Print the smallest number required
    // to be added to remove the digit 'D'
    // in number 'N'
    Console.Write(smallestNumber(N, D));
  }
}

// This code is contributed by sanjoy_62.
```

## **java 描述语言**

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to calculate smallest positive
       // number to be added to remove
       // the given digit
       function smallestNumber(n, d)
       {

           // Copy the number to another variable
           let temp = n;

           let ans = 0, count = 0;

           // Iterate over digits of the given
           // number from right to left
           while (temp > 0) {

               // Extract the last digit of the
               // number and check if it is
               // equal to the given digit (d)
               let remainder = temp % 10;
               temp = Math.floor(temp / 10);
               count++;

               if (remainder == d)
               {

                   // If the digit which
                   // need to be replaced
                   // is equal to 0 then
                   // increment the current
                   // digit and make the all digits
                   // to its right 1
                   if (d == 0) {

                       let num = ''
                       for (let i = 0; i < count; i++) {
                           num = num + '1';
                       }
                       temp = temp * Math.pow(10, count) + parseInt(num);
                   }

                   // Else, increment the current digit
                   // by 1 and make the all digits
                   // to its right 0
                   else {

                       temp = temp * Math.pow(10, count)
                           + (remainder + 1)
                           * Math.pow(10, count - 1);
                   }

                   // After the removal of given
                   // digit the number will be temp
                   // So, the required smallest
                   // number is (temp - n)
                   ans = temp - n;

                   // Set count as 0
                   count = 0;
               }
           }

           // Return the result
           return ans;
       }

       // Driver code
       let N = 100;
       let D = 0;

       // print the smallest number required
       // to be added to remove
       // the digit 'D' in number 'N'
       document.write(smallestNumber(N, D) + "<br>");

   // This code is contributed by Potta Lokesh
   </script>
```

****Output**

```
11
```** 

****时间复杂度:**o((log(n))^2)
T3】辅助空间: O(log(N))**