# 计数数字< = N，其与它们前面的素数之差为> = K

> 原文:[https://www . geeksforgeeks . org/count-numbers-n-谁与素数计数的差-up-them-is-k/](https://www.geeksforgeeks.org/count-numbers-n-whose-difference-with-the-count-of-primes-upto-them-is-k/)

给定两个正整数 **N** 和 **K** ，任务是统计满足以下条件的所有数字:
如果数字是 **num** 、

*   在≤ N 处。
*   **ABS(num–count)≥K**其中 **count** 是到 **num** 的素数计数。

**例:**

> **输入:** N = 10，K = 3
> **输出:** 5
> 6、7、8、9、10 为有效数字。对于 6，6 和 6 (2，3，5)以内的素数之差是 3，即 6–3 = 3。7、8、9、10 的差值分别为 3、4、5、6，K≥K
> **输入:** N = 30，K = 13
> **输出:** 10

**前提:** [【二分搜索法】](https://www.geeksforgeeks.org/binary-search/)
**方法:**观察到素数的个数和计数到该数的差的函数对于特定的 **K** 是单调递增的函数。另外，如果数字 **X** 是有效数字，那么 **X + 1** 也将是有效数字。
**证明:**

> 让函数 C <sub>i</sub> 表示素数计数到数 I，现在，
> 对于数 X + 1 差为 X+1–C<sub>X+1</sub>大于
> 或等于数 X 差 X–C<sub>X</sub>，即(X+1–C<sub>X+1</sub>)≥(X–C<sub>X</sub>)。
> 因此，如果(X–C<sub>X</sub>)≥S，那么(X+1–CX+1)≥S。

因此，我们可以使用二分搜索法找到最小有效数字 **X** ，从 **X** 到 **N** 的所有数字都将是有效数字。所以，答案是**N–X+1**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000001;

// primeUpto[i] denotes count of prime
// numbers upto i
int primeUpto[MAX];

// Function to compute all prime numbers
// and update primeUpto array
void SieveOfEratosthenes()
{
    bool isPrime[MAX];
    memset(isPrime, 1, sizeof(isPrime));

    // 0 and 1 are not primes
    isPrime[0] = isPrime[1] = 0;
    for (int i = 2; i * i < MAX; i++) {

        // If i is prime
        if (isPrime[i]) {

            // Set all multiples of i as non-prime
            for (int j = i * 2; j < MAX; j += i)
                isPrime[j] = 0;
        }
    }

    // Compute primeUpto array
    for (int i = 1; i < MAX; i++) {
        primeUpto[i] = primeUpto[i - 1];
        if (isPrime[i])
            primeUpto[i]++;
    }
}

// Function to return the count
// of valid numbers
int countOfNumbers(int N, int K)
{

    // Compute primeUpto array
    SieveOfEratosthenes();
    int low = 1, high = N, ans = 0;
    while (low <= high) {
        int mid = (low + high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if (mid - primeUpto[mid] >= K) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    // ans is the minimum valid number
    return (ans ? N - ans + 1 : 0);
}

// Driver Code
int main()
{
    int N = 10, K = 3;
    cout << countOfNumbers(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class GFG{

    static final int MAX = 1000001;

    // primeUpto[i] denotes count of prime
    // numbers upto i
    static int primeUpto[] = new int [MAX];

    // Function to compute all prime numbers
    // and update primeUpto array
    static void SieveOfEratosthenes()
    {
        int isPrime[] = new int[MAX];
        for (int i=0; i < MAX ; i++ )
            isPrime[i] = 1;

        // 0 and 1 are not primes
        isPrime[0] = isPrime[1] = 0;
        for (int i = 2; i * i < MAX; i++) {

            // If i is prime
            if (isPrime[i] == 1) {

                // Set all multiples of i as non-prime
                for (int j = i * 2; j < MAX; j += i)
                    isPrime[j] = 0;
            }
        }

        // Compute primeUpto array
        for (int i = 1; i < MAX; i++) {
            primeUpto[i] = primeUpto[i - 1];
            if (isPrime[i] == 1)
                primeUpto[i]++;
        }
    }

    // Function to return the count
    // of valid numbers
    static int countOfNumbers(int N, int K)
    {

        // Compute primeUpto array
        SieveOfEratosthenes();
        int low = 1, high = N, ans = 0;
        while (low <= high) {
            int mid = (low + high) >> 1;

            // Check if the number is
            // valid, try to reduce it
            if (mid - primeUpto[mid] >= K) {
                ans = mid;
                high = mid - 1;
            }
            else
                low = mid + 1;
        }

        ans = ans != 0 ? N - ans + 1 : 0 ;
        // ans is the minimum valid number
        return ans ;
    }

    // Driver Code
     public static void main(String []args)
    {
        int N = 10, K = 3;
        System.out.println(countOfNumbers(N, K)) ;
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

MAX = 1000001
MAX_sqrt = MAX ** (0.5)

# primeUpto[i] denotes count of prime
# numbers upto i
primeUpto = [0] * (MAX)

# Function to compute all prime numbers
# and update primeUpto array
def SieveOfEratosthenes():

    isPrime = [1] * (MAX)

    # 0 and 1 are not primes
    isPrime[0], isPrime[1] = 0, 0
    for i in range(2, int(MAX_sqrt)): 

        # If i is prime
        if isPrime[i] == 1:

            # Set all multiples of i as non-prime
            for j in range(i * 2, MAX, i):
                isPrime[j] = 0

    # Compute primeUpto array
    for i in range(1, MAX):
        primeUpto[i] = primeUpto[i - 1]
        if isPrime[i] == 1:
            primeUpto[i] += 1

# Function to return the count
# of valid numbers
def countOfNumbers(N, K):

    # Compute primeUpto array
    SieveOfEratosthenes()
    low, high, ans = 1, N, 0
    while low <= high: 
        mid = (low + high) >> 1

        # Check if the number is
        # valid, try to reduce it
        if mid - primeUpto[mid] >= K: 
            ans = mid
            high = mid - 1

        else:
            low = mid + 1

    # ans is the minimum valid number
    return (N - ans + 1) if ans else 0

# Driver Code
if __name__ == "__main__":

    N, K = 10, 3 
    print(countOfNumbers(N, K))

 # This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG{

    static  int MAX = 1000001;

    // primeUpto[i] denotes count of prime
    // numbers upto i
    static int []primeUpto = new int [MAX];

    // Function to compute all prime numbers
    // and update primeUpto array
    static void SieveOfEratosthenes()
    {
        int []isPrime = new int[MAX];
        for (int i=0; i < MAX ; i++ )
            isPrime[i] = 1;

        // 0 and 1 are not primes
        isPrime[0] = isPrime[1] = 0;
        for (int i = 2; i * i < MAX; i++) {

            // If i is prime
            if (isPrime[i] == 1) {

                // Set all multiples of i as non-prime
                for (int j = i * 2; j < MAX; j += i)
                    isPrime[j] = 0;
            }
        }

        // Compute primeUpto array
        for (int i = 1; i < MAX; i++) {
            primeUpto[i] = primeUpto[i - 1];
            if (isPrime[i] == 1)
                primeUpto[i]++;
        }
    }

    // Function to return the count
    // of valid numbers
    static int countOfNumbers(int N, int K)
    {

        // Compute primeUpto array
        SieveOfEratosthenes();
        int low = 1, high = N, ans = 0;
        while (low <= high) {
            int mid = (low + high) >> 1;

            // Check if the number is
            // valid, try to reduce it
            if (mid - primeUpto[mid] >= K) {
                ans = mid;
                high = mid - 1;
            }
            else
                low = mid + 1;
        }

        ans = ans != 0 ? N - ans + 1 : 0 ;
        // ans is the minimum valid number
        return ans ;
    }

    // Driver Code
    public static void Main()
    {
        int N = 10, K = 3;
        Console.WriteLine(countOfNumbers(N, K)) ;
    }
    // This code is contributed by anuj_67..
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

$MAX = 100001;

// primeUpto[i] denotes count of
// prime numbers upto i
$primeUpto = array_fill(0, $MAX, 0);

// Function to compute all prime numbers
// and update primeUpto array
function SieveOfEratosthenes()
{
    global $MAX,$primeUpto;
    $isPrime = array_fill(0, $MAX, true);

    // 0 and 1 are not primes
    $isPrime[0] = $isPrime[1] = false;
    for ($i = 2; $i * $i < $MAX; $i++)
    {

        // If i is prime
        if ($isPrime[$i])
        {

            // Set all multiples of i as non-prime
            for ($j = $i * 2; $j < $MAX; $j += $i)
                $isPrime[$j] = false;
        }
    }

    // Compute primeUpto array
    for ($i = 1; $i < $MAX; $i++)
    {
        $primeUpto[$i] = $primeUpto[$i - 1];
        if ($isPrime[$i])
            $primeUpto[$i]++;
    }
}

// Function to return the count
// of valid numbers
function countOfNumbers($N, $K)
{

    // Compute primeUpto array
    SieveOfEratosthenes();
    global $primeUpto;
    $low = 1;
    $high = $N;
    $ans = 0;
    while ($low <= $high)
    {
        $mid = ($low + $high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if ($mid - $primeUpto[$mid] >= $K)
        {
            $ans = $mid;
            $high = $mid - 1;
        }
        else
            $low = $mid + 1;
    }

    // ans is the minimum valid number
    return ($ans ? $N - $ans + 1 : 0);
}

// Driver Code
$N = 10;
$K = 3;
echo countOfNumbers($N, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

var MAX = 1000001;

// primeUpto[i] denotes count of prime
// numbers upto i
var primeUpto = Array(MAX).fill(0);

// Function to compute all prime numbers
// and update primeUpto array
function SieveOfEratosthenes()
{
    var isPrime = Array(MAX).fill(1);

    // 0 and 1 are not primes
    isPrime[0] = isPrime[1] = 0;
    for (var i = 2; i * i < MAX; i++) {

        // If i is prime
        if (isPrime[i]) {

            // Set all multiples of i as non-prime
            for (var j = i * 2; j < MAX; j += i)
                isPrime[j] = 0;
        }
    }

    // Compute primeUpto array
    for (var i = 1; i < MAX; i++) {
        primeUpto[i] = primeUpto[i - 1];
        if (isPrime[i])
            primeUpto[i]++;
    }
}

// Function to return the count
// of valid numbers
function countOfNumbers(N, K)
{

    // Compute primeUpto array
    SieveOfEratosthenes();
    var low = 1, high = N, ans = 0;
    while (low <= high) {
        var mid = (low + high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if (mid - primeUpto[mid] >= K) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    // ans is the minimum valid number
    return (ans ? N - ans + 1 : 0);
}

// Driver Code
var N = 10, K = 3;
document.write( countOfNumbers(N, K));

</script>
```

**Output:** 

```
5
```