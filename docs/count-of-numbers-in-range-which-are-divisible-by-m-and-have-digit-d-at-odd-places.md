# 范围内可被 M 整除且奇数位有数字 D 的数字计数

> 原文:[https://www . geeksforgeeks . org/范围内可被 m 整除且奇数位有数字 d 的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-in-range-which-are-divisible-by-m-and-have-digit-d-at-odd-places/)

给定两个数字 **M，D** 和一个代表范围**【L，R】**的数组 **arr[]** ，任务是对范围**【L，R】**内的数字进行计数，该范围可被 **M** 整除，数字 **D** 出现在每个奇数位置。

**注意:**数字可能很大。所以，范围数组{L，R}以字符串的形式给出。

**示例:**

> **输入:** arr[] = {20，32}，M = 2，D = 2
> **输出:** 4
> **说明:**
> 范围内有 4 个数字在奇数(第一个)位置可被 2 和 2 整除。它们是:
> 20，24，26，28。
> 
> **输入:** arr[] = {40，60}，M = 2，D = 5
> **输出:** 5
> **说明:**
> 范围内有 5 个数字在奇数(第一个)位置可以被 2 和 5 整除。它们是:
> 50，52，54，56，58。

**天真法:**这个问题的天真法是取 **L 到 R** 之间的每一个数字，检查数字 **D** 是否出现在奇数位置，这个数字是否可以被 **M** 整除。这个解的时间复杂度将是 O(N*K)，其中 N 是范围[L，R]中的数字的计数，K 是范围[L，R]中任何数字的最大位数。

**高效途径:**思路是利用[数字-dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 的概念，找出解决问题的数字的组合个数。为了找到满足条件的数的计数，我们找到满足条件的数的计数，直到范围中的最高数 R。这包括所有 1 位、2 位、3 位数字。找到这个计数后，我们只需从上面的值中减去满足 L–1 的数字的计数，就可以得到最终的答案。

1.  假设这些数字是一个数字序列，我们试图形成一个 N 位数，它在每次迭代时都遵循一定的条件，其中 N 是给定上限 r 中的位数
2.  这个计数 C 包括 1 位数、2 位数、3 位数……最多 N 位数，其中 N 是 r 中的位数
3.  类似地，我们发现满足 L–1 条件的数的计数。让这个计数为 d。
4.  需要的答案是两个计数**C–D**之间的差值。
5.  满足给定条件的数的计数由[数字 dp](https://www.geeksforgeeks.org/digit-dp-introduction/) 的概念求出。
6.  使用[这个概念](https://www.geeksforgeeks.org/digit-dp-introduction/)形成并填充三维表格。

下面是上述方法的实现:

## C++14

```
// C++ program to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places

#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Variables to store M, N, D
ll m, n, d;

// Vector to store the digit number
// in the form of digits
vector<int> v;
ll const k = 1e9 + 7;

// Dp table to compute the answer
ll dp[2001][2001][2];

// Function to add the individual
// digits into the vector
void init(string s)
{
    memset(dp, -1, sizeof(dp));
    v.clear();

    // Iterating through the number
    // and adding the digits into
    // the vector
    for (int i = 0; i < s.size(); i++) {
        v.push_back(s[i] - '0');
    }
    n = s.size();
}

// Function to subtract 1 from a number
// represented in a form of a string
string number_minus_one(string a)
{
    string s = a.substr(1);
    string s1 = "";

    // Iterating through the number
    for (int i = 0; i < s.size() - 1; i++)
        s1 += '0';

    // If the first digit is 1, then make it 0
    // and add 9 at the end of the string.
    if (a[0] == 1 and s == s1) {
        ll l = s.size();
        a = "";
        a += '0';
        for (int i = 0; i < l; i++)
            a += '9';
    }
    else {
        for (int i = a.size() - 1; i >= 0; i--) {

            // If we need to subtract 1 from 0,
            // then make it 9 and subtract 1
            // from the previous digits
            if (a[i] == '0')
                a[i] = '9';

            // Else, simply subtract 1
            else {
                a[i] = (((a[i] - '0') - 1) + '0');
                break;
            }
        }
    }
    return a;
}

// Function to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places
ll fun(ll pos, ll sum, ll f)
{

    // Base case
    if (pos == n) {
        if (sum == 0) {

            // If we have built N-digit number
            // and the number is divisible
            // by m then we have got
            // one possible answer.
            return 1;
        }
        return 0;
    }

    // If the answer has already been computed,
    // then return the answer
    if (dp[pos][sum][f] != -1)
        return dp[pos][sum][f];
    ll lmt = 9;

    // The possible digits which we can
    // place at the pos position.
    if (!f)
        lmt = v[pos];

    ll ans = 0;

    // Iterating through all the digits
    for (ll i = 0; i <= lmt; i++) {
        if (i == d and pos % 2 == 1)
            ans += 0;
        else if (i != d and pos % 2 == 0)
            ans += 0;
        else {
            ll new_f = f;

            // If we have placed all the digits
            // up to pos-1 equal to their
            // limit and currently we are placing
            // a digit which is smaller than this
            // position's limit then we can place
            // 0 to 9 at all the next positions
            // to make the number smaller than R
            if (f == 0 and i < lmt)
                new_f = 1;

            // Calculating the number upto pos mod m.
            ll new_sum = sum;

            // Combinations of numbers as there are
            // 10 digits in the range [0, 9]
            new_sum *= 10;
            new_sum += i;
            new_sum %= m;

            // Recursively call the function
            // for the next position
            ans += fun(pos + 1, new_sum, new_f);
            ans %= k;
        }
    }

    // Returning the final answer
    return dp[pos][sum][f] = ans;
}

// Function to call the function
// for every query
void operations(string L, string R)
{
    init(R);
    ll ans = fun(0, 0, 0);
    L = number_minus_one(L);
    init(L);
    ans -= fun(0, 0, 0);
    if (ans < 0)
        ans += k;
    cout << ans << "\n";
}

// Driver code
int main()
{
    m = 2, d = 2;
    ll Q = 1;
    string arr[][2] = { { "20", "32" } };

    for (ll i = 0; i < Q; i++) {
        operations(arr[i][0], arr[i][1]);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places
import java.util.ArrayList;
import java.util.Arrays;

class Graph{

// Variables to store M, N, D
static int m, n, d;

// Vector to store the digit number
// in the form of digits
static ArrayList<Integer> v = new ArrayList<>();
static final int k = (int) 1e9 + 7;

// Dp table to compute the answer
static int[][][] dp = new int[2001][2001][2];

// Function to add the individual
// digits into the vector
static void init(StringBuilder l)
{
    for(int i = 0; i < 2001; i++)
    {
        for(int j = 0; j < 2001; j++)
        {
            for(int k = 0; k < 2; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }
    v.clear();

    // Iterating through the number
    // and adding the digits into
    // the vector
    for(int i = 0; i < l.length(); i++)
    {
        v.add(l.charAt(i) - '0');
    }
    n = l.length();

}

// Function to subtract 1 from a number
// represented in a form of a String
static String number_minus_one(StringBuilder a)
{
    String s = a.substring(1);

    String s1 = "";

    // Iterating through the number
    for(int i = 0; i < s.length() - 1; i++)
        s1 += '0';

    // If the first digit is 1, then make it 0
    // and add 9 at the end of the String.
    if (a.charAt(0) == '1' && s.compareTo(s1) == 0)
    {
        int l = s.length();
        a = new StringBuilder("");
        a.append('0');

        for(int i = 0; i < l; i++)
            a.append('9');

    }
    else
    {
        for(int i = a.length() - 1; i >= 0; i--)
        {

            // If we need to subtract 1 from 0,
            // then make it 9 and subtract 1
            // from the previous digits
            if (a.charAt(i) == '0')
                a.setCharAt(i, '9');

            // Else, simply subtract 1
            else
            {
                a.setCharAt(i, (char)(
                    ((a.charAt(i) - '0') - 1) + '0'));
                break;
            }

        }
    }

    return a.toString();
}

// Function to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places
static int fun(int pos, int sum, int f)
{

    // Base case
    if (pos == n)
    {
        if (sum == 0)
        {

            // If we have built N-digit number
            // and the number is divisible
            // by m then we have got
            // one possible answer.
            return 1;
        }
        return 0;
    }

    // If the answer has already been computed,
    // then return the answer
    if (dp[pos][sum][f] != -1)
        return dp[pos][sum][f];

    int lmt = 9;

    // The possible digits which we can
    // place at the pos position.
    if (f == 0)
        lmt = v.get(pos);

    int ans = 0;

    // Iterating through all the digits
    for(int i = 0; i <= lmt; i++)
    {
        if (i == d && pos % 2 == 1)
            ans += 0;
        else if (i != d && pos % 2 == 0)
            ans += 0;
        else
        {
            int new_f = f;

            // If we have placed all the digits
            // up to pos-1 equal to their
            // limit and currently we are placing
            // a digit which is smaller than this
            // position's limit then we can place
            // 0 to 9 at all the next positions
            // to make the number smaller than R
            if (f == 0 && i < lmt)
                new_f = 1;

            // Calculating the number upto pos mod m.
            int new_sum = sum;

            // Combinations of numbers as there are
            // 10 digits in the range [0, 9]
            new_sum *= 10;
            new_sum += i;
            new_sum %= m;

            // Recursively call the function
            // for the next position
            ans += fun(pos + 1, new_sum, new_f);
            ans %= k;
        }
    }

    // Returning the final answer
    return dp[pos][sum][f] = ans;
}

// Function to call the function
// for every query
static void operations(StringBuilder L,
                       StringBuilder R)
{
    init(R);
    int ans = fun(0, 0, 0);
    L = new StringBuilder(number_minus_one(L));
    init(L);
    ans -= fun(0, 0, 0);

    if (ans < 0)
        ans += k;

    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    m = 2;
    d = 2;
    int Q = 1;

    StringBuilder[][] arr = {
        { new StringBuilder("20"),
          new StringBuilder("32") } };

    for(int i = 0; i < Q; i++)
    {
        operations(arr[i][0], arr[i][1]);
    }
}
}

// This code is contributed by sanjeev2552
```

## C#

```
// C# program to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places
using System;
using System.Collections.Generic;
class Graph{

// Variables to store M, N, D
static int m, n, d;

// Vector to store the digit number
// in the form of digits
static List<int> v = new List<int>();
static int k = (int) 1e9 + 7;

// Dp table to compute the answer
static int[,,] dp = new int[2001, 2001, 2];

// Function to add the individual
// digits into the vector
static void init(string l)
{
    for(int i = 0; i < 2001; i++)
    {
        for(int j = 0; j < 2001; j++)
        {
            for(int k = 0; k < 2; k++)
            {
                dp[i, j, k] = -1;
            }
        }
    }
    v.Clear();

    // Iterating through the number
    // and adding the digits into
    // the vector
    for(int i = 0; i < l.Length; i++)
    {
        v.Add(l[i] - '0');
    }
    n = l.Length;

}

// Function to subtract 1 from a number
// represented in a form of a String
static string number_minus_one(string a)
{
    string s = a.Substring(1);
    string s1 = "";

    // Iterating through the number
    for(int i = 0; i < s.Length - 1; i++)
        s1 += '0';

    // If the first digit is 1, then make it 0
    // and add 9 at the end of the String.
    if (a[0] == '1' && String.Compare(s, s1) == 0)
    {
        int l = s.Length;     
        a = a.Replace(a[0], '0');       
        for(int i = 0; i < l; i++)
            a+='9';
    }
    else
    {
        for(int i = a.Length - 1; i >= 0; i--)
        {

            // If we need to subtract 1 from 0,
            // then make it 9 and subtract 1
            // from the previous digits
            if (a[i] == '0')
                a = a.Replace(a[i], '9');

            // Else, simply subtract 1
            else
            {
                a = a.Replace(a[i], (char)(((a[i] - '0') - 1) + '0'));
                break;
            }     
        }
    }
    return a.ToString();
}

// Function to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places
static int fun(int pos, int sum, int f)
{

    // Base case
    if (pos == n)
    {
        if (sum == 0)
        {

            // If we have built N-digit number
            // and the number is divisible
            // by m then we have got
            // one possible answer.
            return 1;
        }
        return 0;
    }

    // If the answer has already been computed,
    // then return the answer
    if (dp[pos, sum, f] != -1)
        return dp[pos, sum, f];      
    int lmt = 9;

    // The possible digits which we can
    // place at the pos position.
    if (f == 0)
        lmt = v[pos];
    int ans = 0;

    // Iterating through all the digits
    for(int i = 0; i <= lmt; i++)
    {
        if (i == d && pos % 2 == 1)
            ans += 0;
        else if (i != d && pos % 2 == 0)
            ans += 0;
        else
        {
            int new_f = f;

            // If we have placed all the digits
            // up to pos-1 equal to their
            // limit and currently we are placing
            // a digit which is smaller than this
            // position's limit then we can place
            // 0 to 9 at all the next positions
            // to make the number smaller than R
            if (f == 0 && i < lmt)
                new_f = 1;

            // Calculating the number upto pos mod m.
            int new_sum = sum;

            // Combinations of numbers as there are
            // 10 digits in the range [0, 9]
            new_sum *= 10;
            new_sum += i;
            new_sum %= m;

            // Recursively call the function
            // for the next position
            ans += fun(pos + 1, new_sum, new_f);
            ans %= k;
        }
    }

    // Returning the final answer
    dp[pos, sum, f] = ans;
  return dp[pos, sum, f];
}

// Function to call the function
// for every query
static void operations(string L, string R)
{
    init(R);
    int ans = fun(0, 0, 0);
    L = number_minus_one(L);
    init(L);
    ans -= fun(0, 0, 0);

    if (ans < 0)
        ans += k;

    Console.WriteLine(ans);
}

// Driver code
public static void Main(String[] args)
{
    m = 2;
    d = 2;
    int Q = 1;   
    string[,] arr = { {"20",
          "32"  }}; 
    for(int i = 0; i < Q; i++)
    {
        operations(arr[i, 0], arr[i, 1]);
    }
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// Javascript program to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places

// Variables to store M, N, D
var m, n, d;

// Vector to store the digit number
// in the form of digits
var v = [];
var k = 1000000007;

// Dp table to compute the answer
var dp =  Array(2001);

for(var i = 0; i<2001;i++)
{
    dp[i] = Array.from(Array(2001), ()=>Array(2));
}

// Function to add the individual
// digits into the vector
function init(l)
{
    for(var i = 0; i < 2001; i++)
    {
        for(var j = 0; j < 2001; j++)
        {
            for(var k = 0; k < 2; k++)
            {
                dp[i][j][k] = -1;
            }
        }
    }
    v = [];

    // Iterating through the number
    // and adding the digits into
    // the vector
    for(var i = 0; i < l.length; i++)
    {
        v.push(l[i].charCodeAt(0) - '0'.charCodeAt(0));
    }
    n = l.length;

}

// Function to subtract 1 from a number
// represented in a form of a String
function number_minus_one(a)
{
    var s = a.substring(1);
    var s1 = "";

    // Iterating through the number
    for(var i = 0; i < s.length - 1; i++)
        s1 += '0';

    // If the first digit is 1, then make it 0
    // and add 9 at the end of the String.
    if (a[0] == '1' && s === s1)
    {
        var l = s.length;     
        a = a.replace(a[0], '0');       
        for(var i = 0; i < l; i++)
            a+='9';
    }
    else
    {
        for(var i = a.length - 1; i >= 0; i--)
        {

            // If we need to subtract 1 from 0,
            // then make it 9 and subtract 1
            // from the previous digits
            if (a[i] == '0')
                a = a.replace(a[i], '9');

            // Else, simply subtract 1
            else
            {
                a = a.replace(a[i], String.fromCharCode(((a[i].charCodeAt(0) - '0'.charCodeAt(0)) - 1) + '0'.charCodeAt(0)));
                break;
            }     
        }
    }
    return a.toString();
}

// Function to find the count of numbers
// in the range [L, R] which are divisible
// by M and have digit D at the odd places
function fun(pos, sum, f)
{

    // Base case
    if (pos == n)
    {
        if (sum == 0)
        {

            // If we have built N-digit number
            // and the number is divisible
            // by m then we have got
            // one possible answer.
            return 1;
        }
        return 0;
    }

    // If the answer has already been computed,
    // then return the answer
    if (dp[pos][sum][f] != -1)
        return dp[pos][sum][f];      
    var lmt = 9;

    // The possible digits which we can
    // place at the pos position.
    if (f == 0)
        lmt = v[pos];
    var ans = 0;

    // Iterating through all the digits
    for(var i = 0; i <= lmt; i++)
    {
        if (i == d && pos % 2 == 1)
            ans += 0;
        else if (i != d && pos % 2 == 0)
            ans += 0;
        else
        {
            var new_f = f;

            // If we have placed all the digits
            // up to pos-1 equal to their
            // limit and currently we are placing
            // a digit which is smaller than this
            // position's limit then we can place
            // 0 to 9 at all the next positions
            // to make the number smaller than R
            if (f == 0 && i < lmt)
                new_f = 1;

            // Calculating the number upto pos mod m.
            var new_sum = sum;

            // Combinations of numbers as there are
            // 10 digits in the range [0, 9]
            new_sum *= 10;
            new_sum += i;
            new_sum %= m;

            // Recursively call the function
            // for the next position
            ans += fun(pos + 1, new_sum, new_f);
            ans %= k;
        }
    }

    // Returning the final answer
    dp[pos][sum][f] = ans;
  return dp[pos][sum][f];
}

// Function to call the function
// for every query
function operations(L, R)
{
    init(R);
    var ans = fun(0, 0, 0);
    L = number_minus_one(L);
    init(L);
    ans -= fun(0, 0, 0);

    if (ans < 0)
        ans += k;

    document.write(ans + "<br>");
}

// Driver code
m = 2;
d = 2;
var Q = 1;   
var arr = [["20", "32"]]; 
for(var i = 0; i < Q; i++)
{
    operations(arr[i][0], arr[i][1]);
}

</script>
```

**Output:** 

```
4
```

**时间复杂度:O(26*N)**

**辅助空间:O(2001*2001)**