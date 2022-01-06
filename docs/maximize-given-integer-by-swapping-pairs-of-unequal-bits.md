# 通过交换不相等的位对最大化给定的整数

> 原文:[https://www . geesforgeks . org/通过交换不相等位对来最大化给定整数/](https://www.geeksforgeeks.org/maximize-given-integer-by-swapping-pairs-of-unequal-bits/)

给定一个正整数**N****，任务是通过对给定整数 **N** 执行以下操作来确定**最大可能整数**:**

*   **将整数转换为其二进制表示形式。**
*   **在其二进制表示中只交换不相等的位。**

****示例:****

> ****输入** : 11
> **输出** : 14
> **解释**:**
> 
> *   **(11) <sub>10</sub> = (1011) <sub>2</sub>**
> *   **将 0 <sup>第</sup>位与 2 <sup>第</sup>位交换，得到(1110) <sub>2</sub> = (14) <sub>10</sub>**
> 
> ****输入** : 9
> **输出** : 12**

****方法:**按照给定的步骤解决问题**

*   **[统计](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/) **N** 号中的设定位数。**
*   **在任何[二进制串](https://www.geeksforgeeks.org/tag/binary-string/)中，使用上述给定的操作，所有设置的位可以向左移动，所有未设置的位可以向右移动。这是因为任意一对不等位 **(0，1)** 都可以对调，即**“0110110”**可以使用 **3** 运算转换为**“1111000”****
*   **因为，通过向左分割所有设置的位，向右分割所有未设置的位，可以最大化给定的整数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation
// of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum possible
// value that can be obtained from the
// given integer by performing given operations
int findMaxNum(int num)
{

    // Convert to equivalent
    // binary representation
    bitset<4> b(num);

    string binaryNumber = b.to_string();

    // Stores binary representation
    // of the maximized value
    string maxBinaryNumber = "";

    // Store the count of 0's and 1's
    int count0 = 0, count1 = 0;

    // Stores the total Number of Bits
    int N = 4;

    for (int i = 0; i < N; i++) {

        // If current bit is set
        if (binaryNumber[i] == '1') {

            // Increment Count1
            count1++;
        }
        else {

            // Increment Count0
            count0++;
        }
    }

    // Shift all set bits to left
    // to maximize the value
    for (int i = 0; i < count1; i++) {
        maxBinaryNumber += '1';
    }

    // Shift all unset bits to right
    // to maximize the value
    for (int i = 0; i < count0; i++) {
        maxBinaryNumber += '0';
    }

    // Return the maximized value
    return stoi(maxBinaryNumber, 0, 2);
}

// Driver code
int main()
{
    // Given "Input
    int N = 11;

    // Function call to find the
    // Maximum Possible Number
    cout << findMaxNum(N);
    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation
// of the above approach

import java.io.*;

class GFG {

    // Function to return the maximum possible
    // value that can be obtained from the
    // given integer by performing given operations
    public static int findMaxNum(int num)
    {
        // Convert to equivalent
        // binary representation
        String binaryNumber
            = Integer.toBinaryString(num);

        // Stores binary representation
        // of the maximized value
        String maxBinaryNumber = "";

        // Store the count of 0's and 1's
        int count0 = 0, count1 = 0;

        // Stores the total Number of Bits
        int N = binaryNumber.length();

        for (int i = 0; i < N; i++) {

            // If current bit is set
            if (binaryNumber.charAt(i) == '1') {

                // Increment Count1
                count1++;
            }
            else {

                // Increment Count0
                count0++;
            }
        }

        // Shift all set bits to left
        // to maximize the value
        for (int i = 0; i < count1; i++) {
            maxBinaryNumber += '1';
        }

        // Shift all unset bits to right
        // to maximize the value
        for (int i = 0; i < count0; i++) {
            maxBinaryNumber += '0';
        }

        // Return the maximized value
        return Integer.parseInt(
            maxBinaryNumber, 2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given "Input
        int N = 11;

        // Function call to find the
        // Maximum Possible Number
        System.out.println(findMaxNum(N));
    }
}
```

## **蟒蛇 3**

```
# Python3 implementation
# of the above approach

# Function to return the maximum possible
# value that can be obtained from the
# given integer by performing given operations
def findMaxNum(num):

    # Convert to equivalent
    # binary representation
    binaryNumber = bin(num)[2:]

    # Stores binary representation
    # of the maximized value
    maxBinaryNumber = ""

    # Store the count of 0's and 1's
    count0, count1 = 0, 0

    # Stores the total Number of Bits
    N = len(binaryNumber)
    for i in range(N):

        # If current bit is set
        if (binaryNumber[i] == '1'):

            # Increment Count1
            count1 += 1
        else:

            # Increment Count0
            count0 += 1

    # Shift all set bits to left
    # to maximize the value
    for i in range(count1):
        maxBinaryNumber += '1'

    # Shift all unset bits to right
    # to maximize the value
    for i in range(count0):
        maxBinaryNumber += '0'

    # Return the maximized value
    return int(maxBinaryNumber, 2)

# Driver Code
if __name__ == '__main__':

    # Given "Input
    N = 11

    # Function call to find the
    # Maximum Possible Number
    print(findMaxNum(N))

    # This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# implementation
// of the above approach
using System;
public class GFG
{

  // Function to return the maximum possible
  // value that can be obtained from the
  // given integer by performing given operations
  public static int findMaxNum(int num)
  {

    // Convert to equivalent
    // binary representation
    string binaryNumber =  Convert.ToString(num, 2);

    // Stores binary representation
    // of the maximized value
    string maxBinaryNumber = "";

    // Store the count of 0's and 1's
    int count0 = 0, count1 = 0;

    // Stores the total Number of Bits
    int N = binaryNumber.Length;
    for (int i = 0; i < N; i++)
    {

      // If current bit is set
      if (binaryNumber[i] == '1')
      {

        // Increment Count1
        count1++;
      }
      else
      {

        // Increment Count0
        count0++;
      }
    }

    // Shift all set bits to left
    // to maximize the value
    for (int i = 0; i < count1; i++)
    {
      maxBinaryNumber += '1';
    }

    // Shift all unset bits to right
    // to maximize the value
    for (int i = 0; i < count0; i++)
    {
      maxBinaryNumber += '0';
    }

    // Return the maximized value
    return Convert.ToInt32(maxBinaryNumber, 2);
  }

  // Driver Code
  static public void Main()
  {

    // Given "Input
    int N = 11;

    // Function call to find the
    // Maximum Possible Number
    Console.WriteLine(findMaxNum(N));
  }
}

// This code is contributed by Dharanendra L V
```

## **java 描述语言**

```
<script>

// javascript implementation
// of the above approach

// Function to return the maximum possible
// value that can be obtained from the
// given integer by performing given operations
function findMaxNum(num)
{
    // Convert to equivalent
    // binary representation
    var binaryNumber
        = Number(num).toString(2);;
    // Stores binary representation
    // of the maximized value
    var maxBinaryNumber = "";

    // Store the count of 0's and 1's
    var count0 = 0, count1 = 0;

    // Stores the total Number of Bits
    var N = binaryNumber.length;

    for (i = 0; i < N; i++) {

        // If current bit is set
        if (binaryNumber.charAt(i) == '1') {

            // Increment Count1
            count1++;
        }
        else {

            // Increment Count0
            count0++;
        }
    }

    // Shift all set bits to left
    // to maximize the value
    for (i = 0; i < count1; i++) {
        maxBinaryNumber += '1';
    }

    // Shift all unset bits to right
    // to maximize the value
    for (i = 0; i < count0; i++) {
        maxBinaryNumber += '0';
    }

    // Return the maximized value
    return parseInt(maxBinaryNumber,2);
}

// Driver Code

 // Given "Input
var N = 11;

// Function call to find the
// Maximum Possible Number
document.write(findMaxNum(N));

// This code contributed by Princi Singh

</script>
```

****Output:** 

```
14
```** 

*****时间复杂度:** O(log(N))*
***辅助空间:** O(1)***