# 找到一个数字 X，使得(X XOR A)最小，并且 X 和 B 中的设定位数相等

> 原文:[https://www . geeksforgeeks . org/find-a-number-x-so-x-xor-a-是 x-和-b-中的最小和集合位数相等/](https://www.geeksforgeeks.org/find-a-number-x-such-that-x-xor-a-is-minimum-and-the-count-of-set-bits-in-x-and-b-are-equal/)

给定两个整数 **A** 和 **B** ，任务是找到一个整数 **X** ，使得 **(X XOR A)** 是最小可能的，并且 **X** 中的设置位计数等于 **B** 中的设置位计数。
**示例:**

> **输入:** A = 3，B = 5
> **输出:** 3
> 二进制(A) =二进制(3) = 011
> 二进制(B) =二进制(5) = 101
> 当 M = 3
> 即(3 XOR 3) = 0 且 3 中的设定位数
> 等于 5 中的设定位数时，XOR 将最小。
> **输入:** A = 7，B = 12
> **输出:** 6

**逼近:**已知一个元素与其自身的异或为 0。所以，尽量生成尽可能接近 A 的 M 的二进制表示。从 A 中的最高有效位遍历到最低有效位，如果一个位被设置在当前位置，那么它也需要被设置为所需的数量，以便最小化异或运算，但是设置的位数必须等于 B 中的设置位数。因此，当所需数量的设置位数已经达到 B 中的设置位数时，其余的位必须为 0。

也有可能 B 中的设置位的数量多于 A 中的设置位的数量，在这种情况下，开始填充未设置的位，以将位从最低有效位设置为最高有效位。

如果设置位的数量仍然不等于 B，那么将剩余数量的设置位加到最高有效位的左边，以便使 M 的设置位等于 B 的设置位

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the value x
// such that (x XOR a) is minimum
// and the number of set bits in x
// is equal to the number
// of set bits in b
int minVal(int a, int b) {

        int setBits=0,res=0;

          //To count number of set bits in b
        setBits= __builtin_popcount(b);

        //creating binary representation of a in stack s
        stack<short int> s;
        while(a>0)
        {
            s.push(a%2);
            a=a/2;
        }

        // Decrease the count of setBits
        // as in the required number set bits has to be
        // equal to the count of set bits in b
        //Creating nearest possible number in m in binary form.
        //Using vector as the number in binary for can be large.
        vector<short int> m;   

        while(!s.empty())
        {
            if(s.top()==1 && setBits>0)
            {
                m.push_back(1);
                setBits--;
            }
            else
            {
                m.push_back(0);
            }
            s.pop();
        }

        //Filling the unset bits from the least significant bit to the most significant bit
        //if the setBits are not equal to zero
        for(int i=m.size()-1;i>=0 && setBits>0;i--)
        {
            if(m[i]==0)
            {
                m[i]=1;
                setBits--;
            }
        }

        int mask;
        for(int i=m.size()-1;i>=0;i--)
        {
            mask=1<<(m.size()-i-1);

            res+=m[i]*mask;
        }
        int n=m.size();

        //if the number of setBits is still not equal to zero
        //dd the remaining number of set bits to the left of the most significant bit
        //in order to make set bits of m equal to the set bits of B.

        while(setBits>0)
        {
            res+=1<<n;
            n++;
            setBits--;
        }

        return res;
    }

// Driver code
int main()
{
    int a = 3, b = 5;

    cout << minVal(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to get no of set
    // bits in binary representation
    // of positive integer n
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

// Function to return the value x
// such that (x XOR a) is minimum
// and the number of set bits in x
// is equal to the number
// of set bits in b
static int minVal(int a, int b)
{
    // Count of set-bits in bit
    int setBits = countSetBits(b);
    int ans = 0;

    for (int i = 30; i >= 0; i--)
    {
        int mask = 1 << i;

        // If i'th bit is set also set the
        // same bit in the required number
        if ((a & mask) > 0 && setBits > 0)
        {
            ans |= (1 << i);

            // Decrease the count of setbits
            // in b as the count of set bits
            // in the required number has to be
            // equal to the count of set bits in b
            setBits--;
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int a = 3, b = 5;

    System.out.println(minVal(a, b));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the value x
# such that (x XOR a) is minimum
# and the number of set bits in x
# is equal to the number
# of set bits in b
def minVal(a, b) :

    # Count of set-bits in bit
    setBits = bin(b).count('1');
    ans = 0;

    for i in range(30, -1, -1) :
        mask = (1 << i);
        s = (a & mask);

        # If i'th bit is set also set the
        # same bit in the required number
        if (s and setBits > 0) :
            ans |= (1 << i);

            # Decrease the count of setbits
            # in b as the count of set bits
            # in the required number has to be
            # equal to the count of set bits in b
            setBits -= 1;

    return ans;

# Driver code
if __name__ == "__main__" :

    a = 3; b = 5;

    print(minVal(a, b));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to get no of set
    // bits in binary representation
    // of positive integer n
    static int countSetBits(int n)
    {
        int count = 0;
        while (n > 0)
        {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

// Function to return the value x
// such that (x XOR a) is minimum
// and the number of set bits in x
// is equal to the number
// of set bits in b
static int minVal(int a, int b)
{
    // Count of set-bits in bit
    int setBits = countSetBits(b);
    int ans = 0;

    for (int i = 30; i >= 0; i--)
    {
        int mask = 1 << i;

        // If i'th bit is set also set the
        // same bit in the required number
        if ((a & mask) > 0 && setBits > 0)
        {

            ans |= (1 << i);

            // Decrease the count of setbits
            // in b as the count of set bits
            // in the required number has to be
            // equal to the count of set bits in b
            setBits--;
        }
    }

    return ans;
}

// Driver Code
public static void Main()
{
    int a = 3, b = 5;

    Console.Write(minVal(a, b));
}
}

// This code is contributed by Mohit kumar 29
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to get no of set
// bits in binary representation
// of positive integer n
function countSetBits(n) {
    let count = 0;
    while (n > 0) {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Function to return the value x
// such that (x XOR a) is minimum
// and the number of set bits in x
// is equal to the number
// of set bits in b
function minVal(a, b)
{

    // Count of set-bits in bit
    let setBits = countSetBits(b);
    let ans = 0;

    for (let i = 30; i >= 0; i--) {
        let mask = 1 << i;

        // If i'th bit is set also set the
        // same bit in the required number
        if ((a & mask) > 0 && setBits > 0) {

            ans |= (1 << i);

            // Decrease the count of setbits
            // in b as the count of set bits
            // in the required number has to be
            // equal to the count of set bits in b
            setBits--;
        }
    }

    return ans;
}

// Driver Code
let a = 3, b = 5;

document.write(minVal(a, b));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** **O(log(N))**