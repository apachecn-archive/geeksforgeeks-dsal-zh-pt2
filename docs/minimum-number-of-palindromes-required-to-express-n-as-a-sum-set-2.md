# 将 N 表示为和所需的最小回文数|集合 2

> 原文:[https://www . geesforgeks . org/最小回文数-需要将 n 表示为总和集-2/](https://www.geeksforgeeks.org/minimum-number-of-palindromes-required-to-express-n-as-a-sum-set-2/)

给定一个数 N，我们必须找到将 N 表示为它们的和所需的最小回文数。
**例**:

> **输入** : N = 11
> **输出** : 1
> **解释** : 11 本身就是回文。
> **输入** : N = 65
> **输出** : 3
> **解释** : 65 可以表示为三个回文的和(55，9，1)。

在[之前的帖子](https://www.geeksforgeeks.org/minimum-number-of-palindromes-required-to-express-n-as-a-sum-set-1/)中，我们讨论了一种动态规划方法来解决这个时间和空间复杂度为 O(N <sup>3/2</sup> 的问题。
Cilleruelo、Luca 和 Baxter 在 2016 年的一篇研究论文中证明，每个数字都可以表示为任意基数 b > = 5 中最多三个回文的和(这个下限后来被改进为 3)。关于这个定理的证明，请参考[原纸](https://arxiv.org/pdf/1602.06208)。如果数字 N 本身不是回文，不能表示为两个回文之和，我们可以安全地假设答案为 3，从而利用这个定理。
以下是上述方法的实施:

## C++

```
// C++ program to find the minimum number of
// palindromes required to express N as a sum

#include <bits/stdc++.h>
using namespace std;

// A utility for creating palindrome
int createPalindrome(int input, bool isOdd)
{
    int n = input;
    int palin = input;

    // checks if number of digits is odd or even
    // if odd then neglect the last digit of input in
    // finding reverse as in case of odd number of
    // digits middle element occur once
    if (isOdd)
        n /= 10;

    // Creates palindrome by just appending reverse
    // of number to itself
    while (n > 0) {
        palin = palin * 10 + (n % 10);
        n /= 10;
    }

    return palin;
}

// Function to generate palindromes
vector<int> generatePalindromes(int N)
{
    vector<int> palindromes;
    int number;

    // Run two times for odd and even
    // length palindromes
    for (int j = 0; j < 2; j++) {

        // Creates palindrome numbers with first half as i.
        // Value of j decides whether we need an odd length
        // or even length palindrome.
        int i = 1;
        while ((number = createPalindrome(i++, j)) <= N)
            palindromes.push_back(number);
    }

    return palindromes;
}

// Function to find the minimum
// number of palindromes required
// to express N as a sum
int minimumNoOfPalindromes(int N)
{
    // Checking if the number is a palindrome
    string a, b = a = to_string(N);
    reverse(b.begin(), b.end());
    if (a == b)
        return 1;

    // Checking if the number is a
    // sum of two palindromes

    // Getting the list of all palindromes upto N
    vector<int> palindromes = generatePalindromes(N);

    // Sorting the list of palindromes
    sort(palindromes.begin(), palindromes.end());

    int l = 0, r = palindromes.size() - 1;
    while (l < r) {
        if (palindromes[l] + palindromes[r] == N)
            return 2;
        else if (palindromes[l] + palindromes[r] < N)
            ++l;
        else
            --r;
    }

    // The answer is three if the
    // control reaches till this point
    return 3;
}

// Driver code
int main()
{
    int N = 65;

    cout << minimumNoOfPalindromes(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number of
// palindromes required to express N as a sum
import java.util.*;

class GFG
{

    // A utility for creating palindrome
    static int createPalindrome(int input, int isOdd)
    {
        int n = input;
        int palin = input;

        // checks if number of digits is odd or even
        // if odd then neglect the last digit of input in
        // finding reverse as in case of odd number of
        // digits middle element occur once
        if (isOdd % 2 == 1)
        {
            n /= 10;
        }

        // Creates palindrome by just appending reverse
        // of number to itself
        while (n > 0)
        {
            palin = palin * 10 + (n % 10);
            n /= 10;
        }

        return palin;
    }

    // Function to generate palindromes
    static Vector<Integer> generatePalindromes(int N)
    {
        Vector<Integer> palindromes = new Vector<>();
        int number;

        // Run two times for odd and even
        // length palindromes
        for (int j = 0; j < 2; j++)
        {

            // Creates palindrome numbers with first half as i.
            // Value of j decides whether we need an odd length
            // or even length palindrome.
            int i = 1;
            while ((number = createPalindrome(i++, j)) <= N)
            {
                palindromes.add(number);
            }
        }

        return palindromes;
    }

    static String reverse(String input)
    {
        char[] temparray = input.toCharArray();
        int left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.valueOf(temparray);
    }

    // Function to find the minimum
    // number of palindromes required
    // to express N as a sum
    static int minimumNoOfPalindromes(int N)
    {
        // Checking if the number is a palindrome
        String a = String.valueOf(N);
        String b = String.valueOf(N);
        b = reverse(b);
        if (a.equals(b))
        {
            return 1;
        }

        // Checking if the number is a
        // sum of two palindromes
        // Getting the list of all palindromes upto N
        Vector<Integer> palindromes = generatePalindromes(N);

        // Sorting the list of palindromes
        Collections.sort(palindromes);

        int l = 0, r = palindromes.size() - 1;
        while (l < r)
        {
            if (palindromes.get(l) + palindromes.get(r) == N)
            {
                return 2;
            }
            else if (palindromes.get(l) + palindromes.get(r) < N)
            {
                ++l;
            }
            else
            {
                --r;
            }
        }

    // The answer is three if the
        // control reaches till this point
        return 3;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 65;
        System.out.println(minimumNoOfPalindromes(N));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find the minimum number of
# palindromes required to express N as a sum

# A utility for creating palindrome
def createPalindrome(_input, isOdd):

    n = palin = _input

    # checks if number of digits is odd or even
    # if odd then neglect the last digit of _input in
    # finding reverse as in case of odd number of
    # digits middle element occur once
    if isOdd:
        n //= 10

    # Creates palindrome by just appending reverse
    # of number to itself
    while n > 0: 
        palin = palin * 10 + (n % 10)
        n //= 10

    return palin

# Function to generate palindromes
def generatePalindromes(N):

    palindromes = []

    # Run two times for odd and even
    # length palindromes
    for j in range(0, 2): 

        # Creates palindrome numbers with first half as i.
        # Value of j decides whether we need an odd length
        # or even length palindrome.
        i = 1
        number = createPalindrome(i, j)
        while number <= N:
            palindromes.append(number)
            i += 1
            number = createPalindrome(i, j)

    return palindromes

# Function to find the minimum
# number of palindromes required
# to express N as a sum
def minimumNoOfPalindromes(N):

    # Checking if the number is a palindrome
    b = a = str(N)
    b = b[::-1]
    if a == b:
        return 1

    # Checking if the number is a
    # sum of two palindromes

    # Getting the list of all palindromes upto N
    palindromes = generatePalindromes(N)

    # Sorting the list of palindromes
    palindromes.sort()

    l, r = 0, len(palindromes) - 1
    while l < r:

        if palindromes[l] + palindromes[r] == N:
            return 2
        elif palindromes[l] + palindromes[r] < N:
            l += 1
        else:
            r -= 1

    # The answer is three if the
    # control reaches till this point
    return 3

# Driver code
if __name__ == "__main__":

    N = 65
    print(minimumNoOfPalindromes(N))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the
// minimum number of palindromes
// required to express N as a sum
using System;
using System.Collections.Generic;
class GFG{

// A utility for creating palindrome
static int createPalindrome(int input,
                            int isOdd)
{
  int n = input;
  int palin = input;

  // checks if number of digits
  // is odd or even if odd then
  // neglect the last digit of
  // input in finding reverse
  // as in case of odd number of
  // digits middle element occur once
  if (isOdd % 2 == 1)
  {
    n /= 10;
  }

  // Creates palindrome by
  // just appending reverse
  // of number to itself
  while (n > 0)
  {
    palin = palin * 10 + (n % 10);
    n /= 10;
  }

  return palin;
}

// Function to generate palindromes
static List<int> generatePalindromes(int N)
{
  List<int> palindromes = new List<int>();
  int number;

  // Run two times for
  // odd and even length
  // palindromes
  for (int j = 0; j < 2; j++)
  {
    // Creates palindrome numbers
    // with first half as i. Value
    // of j decides whether we need
    // an odd length or even length
    // palindrome.
    int i = 1;
    while ((number = createPalindrome(i++,
                                      j)) <= N)
    {
      palindromes.Add(number);
    }
  }

  return palindromes;
}

static String reverse(String input)
{
  char[] temparray = input.ToCharArray();
  int left, right = 0;
  right = temparray.Length - 1;

  for (left = 0;
       left < right; left++, right--)
  {
    // Swap values of left and right
    char temp = temparray[left];
    temparray[left] = temparray[right];
    temparray[right] = temp;
  }

  return String.Join("", temparray);
}

// Function to find the minimum
// number of palindromes required
// to express N as a sum
static int minimumNoOfPalindromes(int N)
{
  // Checking if the number
  // is a palindrome
  String a = String.Join("", N);
  String b = String.Join("", N);
  b = reverse(b);

  if (a.Equals(b))
  {
    return 1;
  }

  // Checking if the number is
  // a sum of two palindromes
  // Getting the list of all
  // palindromes upto N
  List<int> palindromes =
            generatePalindromes(N);

  // Sorting the list
  // of palindromes
  palindromes.Sort();

  int l = 0,
      r = palindromes.Count - 1;

  while (l < r)
  {
    if (palindromes[l] +
        palindromes[r] == N)
    {
      return 2;
    }
    else if (palindromes[l] +
             palindromes[r] < N)
    {
      ++l;
    }
    else
    {
      --r;
    }
  }

  // The answer is three if the
  // control reaches till this point
  return 3;
}

// Driver code
public static void Main(String[] args)
{
  int N = 65;
  Console.WriteLine(minimumNoOfPalindromes(N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find the
// minimum number of palindromes
// required to express N as a sum

// A utility for creating palindrome
function createPalindrome(input, isOdd)
{
  var n = input;
  var palin = input;

  // checks if number of digits
  // is odd or even if odd then
  // neglect the last digit of
  // input in finding reverse
  // as in case of odd number of
  // digits middle element occur once
  if (isOdd % 2 == 1)
  {
    n = parseInt(n/10);
  }

  // Creates palindrome by
  // just appending reverse
  // of number to itself
  while (n > 0)
  {
    palin = palin * 10 + (n % 10);
    n = parseInt(n/10);
  }

  return palin;
}

// Function to generate palindromes
function generatePalindromes(N)
{
  var palindromes = [];
  var number;

  // Run two times for
  // odd and even length
  // palindromes
  for (var j = 0; j < 2; j++)
  {
    // Creates palindrome numbers
    // with first half as i. Value
    // of j decides whether we need
    // an odd length or even length
    // palindrome.
    var i = 1;
    while ((number = createPalindrome(i++,
                                      j)) <= N)
    {
      palindromes.push(number);
    }
  }

  return palindromes;
}

function reverse(input)
{
  var temparray = input.split('');
  var left, right = 0;
  right = temparray.length - 1;

  for (left = 0;
       left < right; left++, right--)
  {
    // Swap values of left and right
    var temp = temparray[left];
    temparray[left] = temparray[right];
    temparray[right] = temp;
  }

  return temparray.join('');
}

// Function to find the minimum
// number of palindromes required
// to express N as a sum
function minimumNoOfPalindromes(N)
{
  // Checking if the number
  // is a palindrome
  var a = N.toString();
  var b = N.toString();
  b = reverse(b);

  if (a == b)
  {
    return 1;
  }

  // Checking if the number is
  // a sum of two palindromes
  // Getting the list of all
  // palindromes upto N
  var palindromes =
            generatePalindromes(N);

  // Sorting the list
  // of palindromes
  palindromes.sort();

  var l = 0,
      r = palindromes.length - 1;

  while (l < r)
  {
    if (palindromes[l] +
        palindromes[r] == N)
    {
      return 2;
    }
    else if (palindromes[l] +
             palindromes[r] < N)
    {
      ++l;
    }
    else
    {
      --r;
    }
  }

  // The answer is three if the
  // control reaches till this point
  return 3;
}

// Driver code
var N = 65;
document.write(minimumNoOfPalindromes(N));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(√(N)log N。