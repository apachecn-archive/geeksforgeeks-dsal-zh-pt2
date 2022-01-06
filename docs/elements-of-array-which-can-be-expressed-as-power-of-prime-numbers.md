# 可以表示为素数幂的数组元素

> 原文:[https://www . geeksforgeeks . org/可表示为素数幂的数组元素/](https://www.geeksforgeeks.org/elements-of-array-which-can-be-expressed-as-power-of-prime-numbers/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是打印数组中所有可以表示为素数幂的元素。

**示例:**

> **输入:** arr = {2，8，81，36，100}
> **输出:** 2，8，81
> **解释:**
> 这里 2 = 2 <sup>1</sup> ，8 = 2 <sup>3</sup> 和 81 = 3 <sup>4</sup>
> 
> **输入:** arr = {4，7，144}
> **输出:** 4，7

**进场:**

*   其思想是使用厄拉多塞的[筛，并对其进行修改，将素数的所有指数存储在一个布尔数组中。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   现在[遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查布尔数组中每个元素是否标记为真。
*   如果标记为真，打印号码。

下面是上述方法的实现:

## C++

```
// C++ program to print all elements
// of Array which can be expressed
// as power of prime numbers

#include <bits/stdc++.h>
using namespace std;

// Function to mark all the
// exponent of prime numbers
void ModifiedSieveOfEratosthenes(
    int N, bool Expo_Prime[])
{
    bool primes[N];
    memset(primes, true, sizeof(primes));

    for (int i = 2; i < N; i++) {

        if (primes[i]) {

            int no = i;

            // If number is prime then marking
            // all of its exponent true
            while (no <= N) {

                Expo_Prime[no] = true;
                no *= i;
            }

            for (int j = i * i; j < N; j += i)
                primes[j] = false;
        }
    }
}

// Function to display all required elements
void Display(int arr[],
             bool Expo_Prime[],
             int n)
{

    for (int i = 0; i < n; i++)
        if (Expo_Prime[arr[i]])
            cout << arr[i] << " ";
}

// Function to print the required numbers
void FindExpoPrime(int arr[], int n)
{
    int max = 0;

    // To find the largest number
    for (int i = 0; i < n; i++) {
        if (max < arr[i])
            max = arr[i];
    }

    bool Expo_Prime[max + 1];

    memset(Expo_Prime, false,
           sizeof(Expo_Prime));

    // Function call to mark all the
    // Exponential prime nos.
    ModifiedSieveOfEratosthenes(
        max + 1, Expo_Prime);

    // Function call
    Display(arr, Expo_Prime, n);
}

// Driver code
int main()
{
    int arr[] = { 4, 6, 9, 16, 1, 3,
                  12, 36, 625, 1000 };
    int n = sizeof(arr) / sizeof(int);

    FindExpoPrime(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all elements
// of Array which can be expressed
// as power of prime numbers
import java.util.*;

class GFG{

// Function to mark all the
// exponent of prime numbers
static void ModifiedSieveOfEratosthenes(
    int N, boolean Expo_Prime[])
{
    boolean []primes = new boolean[N];
    Arrays.fill(primes, true);

    for (int i = 2; i < N; i++) {

        if (primes[i]) {

            int no = i;

            // If number is prime then marking
            // all of its exponent true
            while (no <= N) {

                Expo_Prime[no] = true;
                no *= i;
            }

            for (int j = i * i; j < N; j += i)
                primes[j] = false;
        }
    }
}

// Function to display all required elements
static void Display(int arr[],
             boolean Expo_Prime[],
             int n)
{

    for (int i = 0; i < n; i++)
        if (Expo_Prime[arr[i]])
            System.out.print(arr[i]+ " ");
}

// Function to print the required numbers
static void FindExpoPrime(int arr[], int n)
{
    int max = 0;

    // To find the largest number
    for (int i = 0; i < n; i++) {
        if (max < arr[i])
            max = arr[i];
    }

    boolean []Expo_Prime = new boolean[max + 1];

    // Function call to mark all the
    // Exponential prime nos.
    ModifiedSieveOfEratosthenes(
        max + 1, Expo_Prime);

    // Function call
    Display(arr, Expo_Prime, n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 6, 9, 16, 1, 3,
                  12, 36, 625, 1000 };
    int n = arr.length;

    FindExpoPrime(arr, n);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to print all elements
# of Array which can be expressed
# as power of prime numbers

# Function to mark all the
# exponent of prime numbers
def ModifiedSieveOfEratosthenes(N, Expo_Prime) :

    primes = [True]*N;

    for i in range(2, N) :
        if (primes[i]) :

            no = i;

            # If number is prime then marking
            # all of its exponent true
            while (no <= N) :

                Expo_Prime[no] = True;
                no *= i;

            for j in range(i * i, N, i) :
                primes[j] = False;

# Function to display all required elements
def Display(arr, Expo_Prime, n) :

    for i in range(n) :
        if (Expo_Prime[arr[i]]) :
            print(arr[i], end= " ");

# Function to print the required numbers
def FindExpoPrime(arr, n) :

    max = 0;

    # To find the largest number
    for i in range(n) :
        if (max < arr[i]) :
            max = arr[i];

    Expo_Prime = [False]*(max + 1);

    # Function call to mark all the
    # Exponential prime nos.
    ModifiedSieveOfEratosthenes(max + 1, Expo_Prime);

    # Function call
    Display(arr, Expo_Prime, n);

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 6, 9, 16, 1, 3,
                12, 36, 625, 1000 ];
    n = len(arr);

    FindExpoPrime(arr, n);

# This code is contributed by Yash_R
```

## C#

```
// C# program to print all elements
// of Array which can be expressed
// as power of prime numbers
using System;

class GFG{

// Function to mark all the
// exponent of prime numbers
static void ModifiedSieveOfEratosthenes(int N,
                            bool []Expo_Prime)
{
    bool []primes = new bool[N];
    for(int i = 0; i < N; i++)
        primes[i] = true;

    for(int i = 2; i < N; i++)
    {
       if (primes[i])
       {
           int no = i;

           // If number is prime then marking
           // all of its exponent true
           while (no <= N)
           {
               Expo_Prime[no] = true;
               no *= i;
           }
           for(int j = i * i; j < N; j += i)
              primes[j] = false;
       }
    }
}

// Function to display all required
// elements
static void Display(int []arr,
                    bool []Expo_Prime,
                    int n)
{
    for(int i = 0; i < n; i++)
       if (Expo_Prime[arr[i]])
           Console.Write(arr[i] + " ");
}

// Function to print the required numbers
static void FindExpoPrime(int []arr, int n)
{
    int max = 0;

    // To find the largest number
    for(int i = 0; i < n; i++)
    {
       if (max < arr[i])
           max = arr[i];
    }

    bool []Expo_Prime = new bool[max + 1];

    // Function call to mark all the
    // Exponential prime nos.
    ModifiedSieveOfEratosthenes(max + 1,
                                Expo_Prime);

    // Function call
    Display(arr, Expo_Prime, n);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 6, 9, 16, 1, 3,
                  12, 36, 625, 1000 };
    int n = arr.Length;

    FindExpoPrime(arr, n);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to print all elements
// of Array which can be expressed
// as power of prime numbers

// Function to mark all the
// exponent of prime numbers
function ModifiedSieveOfEratosthenes(N, Expo_Prime)
{
    let primes = new Array(N);
    primes.fill(true)

    for (let i = 2; i < N; i++) {

        if (primes[i]) {

            let no = i;

            // If number is prime then marking
            // all of its exponent true
            while (no <= N) {

                Expo_Prime[no] = true;
                no *= i;
            }

            for (let j = i * i; j < N; j += i)
                primes[j] = false;
        }
    }
}

// Function to display all required elements
function Display(arr, Expo_Prime, n)
{

    for (let i = 0; i < n; i++)
        if (Expo_Prime[arr[i]])
            document.write(arr[i] + " ");
}

// Function to print the required numbers
function FindExpoPrime(arr, n)
{
    let max = 0;

    // To find the largest number
    for (let i = 0; i < n; i++) {
        if (max < arr[i])
            max = arr[i];
    }

    let Expo_Prime = new Array(max + 1);
    Expo_Prime.fill(false)

    // Function call to mark all the
    // Exponential prime nos.
    ModifiedSieveOfEratosthenes(
        max + 1, Expo_Prime);

    // Function call
    Display(arr, Expo_Prime, n);
}

// Driver code

    let arr = [ 4, 6, 9, 16, 1, 3,
                12, 36, 625, 1000 ];
    let n = arr.length

    FindExpoPrime(arr, n);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
4 9 16 3 625
```