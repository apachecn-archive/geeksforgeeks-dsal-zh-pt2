# 将给定的二进制数从 L 转换为 R 后的素数

> 原文:[https://www . geesforgeks . org/转换给定二进制数后的素数/l 到 r 之间的基数/](https://www.geeksforgeeks.org/count-of-primes-after-converting-given-binary-number-in-base-between-l-to-r/)

给定一个二进制数 **N** ，以及一个由 **L** 和 **R** 表示的范围，任务是将所有基数中的给定二进制数转换为 L 和 R (L 和 R 包括在内)，并计算其中的素数。
**举例:**

> **输入:** N = 111，L = 3，R = 10
> **输出:** 5
> **解释:**
> 当在 3 到 10 之间的所有基数中解释 111 时，我们得到的结果数是[21，13，12，11，10，7，7，7]，其中只有 5 个数是质数。因此，输出为 5。
> **输入:** N = 11，L = 4，R = 19
> **输出:** 16
> **解释:**
> 当 11 被解释为 4 到 19 之间的所有基数时，我们得到的结果数是 3，这是一个素数。因此，输出为 16。

**方法:**将给定的二进制数逐个转换为**‘L’**和**‘R’**之间的每个基数。然后，检查结果数是否是质数。如果是，则增加计数。
以下是上述方法的实现:

## 蟒蛇 3

```
# Python3 program to count of primes
# after converting given binary
# number in base between L to R

# Function to interpret the binary number in all
# the base numbers between L and R one by one
def calc(binary, interpret_language):

    # Temporary integer as intermediate
    # value in a known language
    tmp = 0

    # Representation of digits in base 2
    base = "01"

    # For each digit in the 'binary'
    # get its index and its value
    for n, digit in enumerate(binary[::-1]):
        tmp += base.index(digit)*len(base)**n

    # Generate the 'resulting_number' by appending
    resulting_number = ''

    while tmp:
        resulting_number += interpret_language[tmp % len(interpret_language)]

        # reduce the value of tmp
        tmp //= len(interpret_language)

    return resulting_number

# Function to check if the resulting
# number is prime or not
def IS_prime (N):
    n = int(N)
    c = 1

    for i in range (2, n + 1):
        if (n % i == 0):
            c+= 1

    if (c == 2):
        return 1

    return 0

# Driver program
if __name__ == '__main__':
    binary = "111"
    L = 3
    R = 10
    bases = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 'A', 'B', 'D',
            'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M',
            'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U',
            'V', 'W', 'X', 'Y', 'Z']

    b = bases[0:R]

    # Count all the resulting numbers which are prime
    count = 0

    for i in range (R-L + 1):

        # 'list' indicates representation of digits
        # in each base number
        list = b[:(L + i)]

        # Converting in string
        interpret_language = ''.join(map(str, list))

        # Converting the binary number to the respective
        # base between L and R
        resulting_number = calc(binary, interpret_language)
        if(IS_prime(resulting_number) == 1):
            count+= 1

    print (count)
```

**Output:** 

```
5
```