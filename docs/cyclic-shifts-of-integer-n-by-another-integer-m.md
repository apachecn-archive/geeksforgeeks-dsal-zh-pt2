# 整数 N 乘以另一个整数 m 的循环移位

> 原文:[https://www . geesforgeks . org/整数 n 乘另一整数 m 的循环移位/](https://www.geeksforgeeks.org/cyclic-shifts-of-integer-n-by-another-integer-m/)

给定一个表示为 X = 16 位二进制表示的**整数 N** 。我们还得到了一个数字‘M’和一个字符 c，该字符是 L 或 r。任务是确定一个数字 M，该数字 M 是在将 N 的二进制表示循环移位 M 个位置后生成的，如果 c = L，则向左移位；如果 c = R，则向右移位。
**示例:**

> **输入:** N = 7881，m = 5，c = L
> **输出:** 55587
> **解释:**
> 二进制中的 N 为 0001 1110 1100 1001，左移 5 位，变成 1101 1001 0010 0011，在十进制中为 55587。
> **输入:** N = 7881，m = 3，c = R
> **输出:** 9177
> **说明:**
> 二进制中的 N 为 0001 1110 1100 1001 并向右移位 3 位，则变为 0010 0011 1101 1001，在十进制中为 9177。

**方法:**
为了解决上面提到的问题，我们观察到，如果字符是 R，我们必须将数字右移 m，否则，如果字符是 L，我们将左移 m，其中，左移相当于将一个数字乘以 2，右移相当于将一个数字除以 2。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Cyclic shifts of integer N by another integer m
void Count(int N, int m, char turn)
{
  // str represents bitwise representation of N
  string str = bitset<16>(N).to_string();

  m%=(int)str.size();

  // rotate the string by a specific count
  if(turn=='R')
    str = str.substr((int)str.size()-m) + str.substr(0,(int)str.size());
  else 
    str = str.substr(m) + str.substr(0,m);

  // printing the number represented by the bitset
  // in str
  cout << bitset<16> (str).to_ulong() << '\n';
}

int main()
{
  int N = 7881 ;
  int m = 5;
  char turn = 'L';
  Count(N,m,turn);
}
```

## 蟒蛇 3

```
# Python implementation to make
# Cyclic shifts of integer N by another integer m

def Count(N, count, turn):
    # Convert N into hexadecimal number and
    # remove the initial zeros in it
    N = hex(int(N)).split('x')[-1]

    # Convert hexadecimal term binary
    # string of length = 16 with padded 0s
    S = ( bin(int(N, 16))[2:] ).zfill(16)

    # rotate the string by a specific count
    if(turn == 'R'):
        S = (S[16 - int(count) : ] + S[0 : 16 - int(count)])

    else:
        S = (S[int(count) : ] + S[0 : int(count)])

    # Convert the rotated binary string
    # in decimal form, here 2 means in binary form.
    print(int(S, 2))

# driver code
N = 7881
count = 5
turn = 'L'

Count(N, count, turn)
```

**Output:** 

```
55587
```

**时间复杂度:** O(n)

**辅助空间:** O(1)