# 数组的不同素因子

> 原文:[https://www . geesforgeks . org/distinct-prime-of-factors of-a-array/](https://www.geeksforgeeks.org/distinct-prime-factors-of-an-array/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找出给定数组中所有数字的不同质因数。

**示例:**

> **输入:** N = 3，arr[] = {12，15，18}
> **输出:** 2 3 5
> **解释:**
> 12 = 2 x 2 x 3
> 15 = 3 x 5
> 18 = 2 x 3 x 3
> 给定数字中不同的质因数是 2，3，5。
> 
> **输入:** N = 9，arr[] = {2，3，4，5，6，7，8，9，10 }
> T3】输出: 2 3 5 7

**天真方法:**这个问题的一个简单方法是找到数组中每个数的素因子。然后在这些质因数中找出不同的质数。
T3】时间复杂度: O(N <sup>2</sup>

**有效方法:**一种有效的方法是首先使用厄拉多塞[筛](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)找到所有达到给定极限的素数，并将其存储在数组中。对于**质数数组**中的每个质数，检查输入数组中是否有任何数可以被整除。如果它是可分的，那么把这个质数存储在答案数组中。最后，对给定输入数组中的所有数字重复此过程后，返回答案数组。

下面是上述方法的实现:

## C++14

```
#include <bits/stdc++.h>

using namespace std;

//cppimplementation of the above approach

//Function to return an array
//of prime numbers upto n
//using Sieve of Eratosthenes
vector<int> sieve(int n){
    vector<int> prime (n + 1,0);
    int p = 2;
    while(p * p<= n){
        if(prime[p]== 0){
            for (int i=2*p;i<n+1;i+=p)
                    prime[i]= 1;
              }
        p+= 1;
      }

    vector<int> allPrimes;
    for (int i =2;i<n;i++) if (prime[i]==0) allPrimes.push_back(i);
    return allPrimes;
  }

//Function to return distinct
//prime factors from the given array
vector<int> distPrime(vector<int> arr, vector<int> allPrimes){

    //Creating an empty array
    //to store distinct prime factors
    vector<int> list1;

    //Iterating through all the
    //prime numbers and check if
    //any of the prime numbers is a
    //factor of the given input array
    for (int i : allPrimes){
        for (int j :arr){
            if(j % i == 0){
                list1.push_back(i);
                break;
              }
            }
          }
    return list1;
  }

//Driver code

int main()
{
  //Finding prime numbers upto 10000
  //using Sieve of Eratosthenes
  vector<int> allPrimes = sieve(10000);

  vector<int> arr = {15, 30, 60};
  vector<int> ans = distPrime(arr, allPrimes);
  cout<<"[";
  for(int i:ans) cout<<i<<" ";
  cout<<"]";

}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to return an array
// of prime numbers upto n
// using Sieve of Eratosthenes
static ArrayList<Integer> sieve(int n){
    ArrayList<Integer> prime = new ArrayList<Integer>();
    for(int i = 0; i < n + 1; i++)
    prime.add(0);
    int p = 2;
    while(p * p <= n){
        if(prime.get(p) == 0){
            for (int i = 2 * p; i < n + 1; i += p)
                prime.set(i, 1);
            }
        p += 1;
    }

    ArrayList<Integer> allPrimes = new ArrayList<Integer>();
    for (int i = 2; i < n; i++){
    if (prime.get(i) == 0)
        allPrimes.add(i);
    }
    return allPrimes;
}

// Function to return distinct
// prime factors from the given array
static ArrayList<Integer> distPrime(ArrayList<Integer> arr,
                            ArrayList<Integer> allPrimes){

    // Creating an empty array
    // to store distinct prime factors
    ArrayList<Integer> list1 = new ArrayList<Integer>();

    // Iterating through all the
    // prime numbers and check if
    // any of the prime numbers is a
    // factor of the given input array
    for (int i = 0; i < allPrimes.size(); i++){
        for (int j = 0; j < arr.size(); j++){
            if(arr.get(j) % allPrimes.get(i) == 0){
                list1.add(allPrimes.get(i));
                break;
            }
            }
        }
    return list1;
}

// Driver code
public static void main(String args[])
{

    // Finding prime numbers upto 10000
    // using Sieve of Eratosthenes
    ArrayList<Integer> allPrimes = new ArrayList<Integer>(sieve(10000));
    ArrayList<Integer> arr = new ArrayList<Integer>();
    arr.add(15);
    arr.add(30);
    arr.add(60);
    ArrayList<Integer> ans = new ArrayList<Integer>(distPrime(arr, allPrimes));
    System.out.print("[");
    for(int i = 0; i < ans.size(); i++)
    System.out.print(ans.get(i) + " ");
    System.out.print("]");
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return an array
# of prime numbers upto n
# using Sieve of Eratosthenes
def sieve(n):
    prime =[True]*(n + 1)
    p = 2
    while(p * p<= n):
        if(prime[p] == True):
            for i in range(p * p, n + 1, p):
                prime[i] = False
        p += 1
    allPrimes = [x for x in range(2, n)if prime[x]]
    return allPrimes

# Function to return distinct
# prime factors from the given array
def distPrime(arr, allPrimes):

    # Creating an empty array
    # to store distinct prime factors
    list1 = list()

    # Iterating through all the
    # prime numbers and check if
    # any of the prime numbers is a
    # factor of the given input array
    for i in allPrimes:
        for j in arr:
            if(j % i == 0):
                list1.append(i)
                break
    return list1

# Driver code
if __name__=="__main__":

    # Finding prime numbers upto 10000
    # using Sieve of Eratosthenes
    allPrimes = sieve(10000)

    arr = [15, 30, 60]
    ans = distPrime(arr, allPrimes)
    print(ans)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to return an array
// of prime numbers upto n
// using Sieve of Eratosthenes
static List<int> sieve(int n)
{
    List<int> prime = new List<int>();
    for(int i = 0; i < n + 1; i++)
    prime.Add(0);
    int p = 2;
    while(p * p <= n)
    {
        if(prime[p] == 0)
        {
            for (int i = 2 * p; i < n + 1; i += p)
                prime[i]= 1;
            }
        p += 1;
    }

    List<int> allPrimes = new List<int>();
    for (int i = 2; i < n; i++){
    if (prime[i] == 0)
        allPrimes.Add(i);
    }
    return allPrimes;
}

// Function to return distinct
// prime factors from the given array
static List<int> distPrime(List<int> arr,
                            List<int> allPrimes){

    // Creating an empty array
    // to store distinct prime factors
       List<int> list1 = new List<int>();

    // Iterating through all the
    // prime numbers and check if
    // any of the prime numbers is a
    // factor of the given input array
    for (int i = 0; i < allPrimes.Count; i++){
        for (int j = 0; j < arr.Count; j++){
            if(arr[j] % allPrimes[i] == 0){
                list1.Add(allPrimes[i]);
                break;
            }
            }
        }
    return list1;
}

// Driver code
public static void Main(string []args)
{

    // Finding prime numbers upto 10000
    // using Sieve of Eratosthenes
    List<int> allPrimes = new List<int>(sieve(10000));
    List<int> arr = new List<int>();
    arr.Add(15);
    arr.Add(30);
    arr.Add(60);
    List<int> ans = new List<int>(distPrime(arr, allPrimes));
    Console.Write("[");
    for(int i = 0; i < ans.Count; i++)
    Console.Write(ans[i] + " ");
    Console.Write("]");
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return an array
// of prime numbers upto n
// using Sieve of Eratosthenes
function sieve(n)
{
    let prime = [];
    for(let i = 0; i < n + 1; i++)
        prime.push(0);

    let p = 2;
    while (p * p <= n)
    {
        if (prime[p] == 0)
        {
            for(let i = 2 * p; i < n + 1; i += p)
                prime[i] = 1;
        }
        p += 1;
    }

    let allPrimes = [];
    for(let i = 2; i < n; i++)
    {
        if (prime[i] == 0)
            allPrimes.push(i);
    }
    return allPrimes;
}

// Function to return distinct
// prime factors from the given array
function distPrime(arr, allPrimes)
{

    // Creating an empty array
    // to store distinct prime factors
    let list1 = [];

    // Iterating through all the
    // prime numbers and check if
    // any of the prime numbers is a
    // factor of the given input array
    for(let i = 0; i < allPrimes.length; i++)
    {
        for(let j = 0; j < arr.length; j++)
        {
            if (arr[j] % allPrimes[i] == 0)
            {
                list1.push(allPrimes[i]);
                break;
            }
        }
    }
    return list1;
}

// Driver code

// Finding prime numbers upto 10000
// using Sieve of Eratosthenes
let allPrimes = sieve(10000);
let arr = [];
arr.push(15);
arr.push(30);
arr.push(60);
let ans = distPrime(arr, allPrimes);

document.write("[");
for(let i = 0; i < ans.length; i++)
    document.write(ans[i] + " ");

document.write("]");

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
[2, 3, 5]
```