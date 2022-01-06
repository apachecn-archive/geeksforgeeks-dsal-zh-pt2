# 两个数形成的最大因子

> 原文:[https://www . geesforgeks . org/maximum-factors-formed-two-numbers/](https://www.geeksforgeeks.org/maximum-factors-formed-two-numbers/)

给定一个 N 个数字的列表，找出两个数字，使得两个数字的乘积具有最大数量的[因子](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)。正式给出 n 个数字 a0，a1，a2，…..一个。我们需要找到两个数字 ai 和 aj，使得它们的相乘给出 ai * aj 的最大因子数和返回因子数
约束
1<= n<= 100
1<= ai<= 10^8

示例:

```
Input : [4, 3, 8] 
Output : 8
3*4 = 12 which has 6 factors
3*8 = 24 which has 8 factors
4*8 = 32 which has 6 factors
for ai, aj = {3, 8} we have the 
maximum number of factors 8 

```

一个简单的方法似乎是取两个最大质因数的数。这种方法可能不起作用，因为选择的两个数字可能有许多共同的因素，他们的产品可能没有最大因素。比如在[4，3，8]中，(4，8)不是答案，而是 3，8 是答案。

我们考虑每一对数字。对于每一对，我们找到因子的并集，最后返回在并集中计数最大的一对。

## C++

```
// C++ program to find the pair whose 
// product has maximum factors.
#include <bits/stdc++.h>
using namespace std;

typedef unordered_map<int,int> u_map;

// Returns a map that has counts of individual
// factors in v[]
u_map countMap(vector<int> v)
{
    u_map map;
    for (size_t i = 0; i < v.size(); i++) 
        if (map.find(v[i]) != map.end()) 
            map[v[i]]++;        
        else 
            map.insert({v[i], 1});        
    return map;
}

// Given two Numbers in the form of their 
// prime factorized maps. Returns total 
// number of factors of the product of 
// those two numbers
int totalFactors(u_map m1, u_map m2)
{
    // Find union of all factors.
    for (auto it = m2.begin(); it != m2.end(); ++it) {
        if (m1.find(it->first) != m1.end()) 
            m1[it->first] += it->second;        
        else 
            m1.insert({ it->first, it->second });        
    }

    int product = 1;
    for (auto it = m1.begin(); it != m1.end(); it++) 
        product *= (it->second + 1);

    return product;
}

// Prime factorization of a number is represented 
// as an Unordered map
u_map primeFactorize(int n)
{
    vector<int> pfac;
    int temp = 2;
    while (temp * temp <= n) {
        if (n % temp == 0) {
            pfac.push_back(temp);
            n = n / temp;
        }
        else {
            temp++;
        }
    }
    if (n > 1) 
        pfac.push_back(n);

    return countMap(pfac);
}

int maxProduct(int arr[], int n)
{
    // vector containing of prime factorizations
    // of every number in the array. Every element
    // of vector contains factors and their counts.
    vector<u_map> vum;
    for (int i = 0; i < n; i++) 
        vum.push_back(primeFactorize(arr[i]));

    // Consider every pair and find the pair with
    // maximum factors. 
    int maxp = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i == j)
                continue;
            maxp = max(maxp,
                  totalFactors(vum[i], vum[j]));
        }
    }
    return maxp;
}

// Driver code
int main()
{
    int arr[] = { 4, 3, 8 };
    cout << maxProduct(arr, 3);
    return 0;
}
```

## 计算机编程语言

```
# Python program to find the pair whose 
# product has maximum factors.
from collections import Counter

# Returns list of factors of n.
def prime_factorize(n):
    primfac = []
    d = 2
    while d * d <= n:
        while (n % d) == 0:
            primfac.append(d)  
            n //= d
        d += 1
    if n > 1:
       primfac.append(n)
    return Counter(primfac)

# Returns total factors in c1 and c2
def total_factors(c1, c2):

    c = c1 + c2
    v = c.values()

    # calc product of each element + 1
    p = 1
    for i in v:
        p *=(i + 1)
    return p

def max_product(arr):
    n = len(arr)

    # Loop through all the nc2 possibilities
    pfac = []
    for i in arr:
        pfac.append(prime_factorize(i))
    maxp = 0
    for i, v1 in enumerate(arr):
        for j, v2 in enumerate(arr):
            if i == j:
                continue
            p = total_factors(pfac[i], pfac[j])
            if(p>maxp):
                maxp = p
    return maxp

if __name__ == '__main__':
    print max_product([4, 8, 3])
```

Output:

```
8

```

一种**替代方法**是找到所有对的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) ，并找到所有 LCM 中的因子。最后返回 LCM 因子最大的对。