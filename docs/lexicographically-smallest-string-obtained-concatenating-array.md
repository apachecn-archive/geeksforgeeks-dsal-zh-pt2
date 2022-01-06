# 串联数组后获得的字典最小字符串

> 原文:[https://www . geeksforgeeks . org/词典学-最小-字符串-获得-串联-数组/](https://www.geeksforgeeks.org/lexicographically-smallest-string-obtained-concatenating-array/)

给定 n 个字符串，按照产生字典上最小可能字符串的顺序连接它们。
**例:**

```
Input :  a[] = ["c", "cb", "cba"]
Output : cbacbc
Possible strings are ccbcba, ccbacb, 
cbccba, cbcbac, cbacbc and cbaccb. 
Among all these strings, cbacbc is 
the lexicographically smallest.

Input :  a[] = ["aa", "ab", "aaa"]
Output : aaaaaab
```

人们可能会认为，按照字典顺序对给定的字符串进行排序，然后将它们串联起来，就能产生正确的输出。这种方法为像["a "、" ab "、" abc"]这样的输入产生正确的输出。然而，在["c "、" cb "、" cba"]上应用此方法会产生错误的输入，因此此方法是不正确的。
正确的做法是使用规则的排序算法。当比较两个字符串 a 和 b 以决定它们是否必须交换时，不要检查 a 在字典上是否小于 b。相反，请检查在 a 的末尾追加 b 是否会产生字典上较小的字符串，或者在 b 的末尾追加 a 是否会。这种方法之所以有效，是因为我们希望串联的字符串在字典序上很小，而不是单个字符串按照字典序排列。

## C++

```
// CPP code to find the lexicographically
// smallest string
#include <bits/stdc++.h>
using namespace std;

// Compares two strings by checking if
// which of the two concatenations causes
// lexicographically smaller string.
bool compare(string a, string b)
{
    return (a+b < b+a);
}

string lexSmallest(string a[], int n)
{
    // Sort strings using above compare()
    sort(a, a+n, compare);

    // Concatenating sorted strings
    string answer = "";
    for (int i = 0; i < n; i++)
        answer += a[i];

    return answer;
}

// Driver code
int main()
{
    string a[] = { "c", "cb", "cba" };
    int n = sizeof(a)/sizeof(a[0]);
    cout << lexSmallest(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the lexicographically
// smallest string

class GFG {

// function to sort the
// array of string
static void sort(String a[], int n)
{

    //sort the array
    for(int i = 0;i < n;i++)
    {
        for(int j = i + 1;j < n;j++)
        {

            // comparing which of the
            // two concatenation causes
            // lexicographically smaller
            // string
            if((a[i] + a[j]).compareTo(a[j] + a[i]) > 0)
            {
                String s = a[i];
                a[i] = a[j];
                a[j] = s;
            }
        }
    }
}

static String lexsmallest(String a[], int n)
{

    // Sort strings
    sort(a,n);

    // Concatenating sorted strings
    String answer = "";
    for (int i = 0; i < n; i++)
        answer += a[i];

    return answer;
}

// Driver code
public static void main(String args[])
{
    String a[] = {"c", "cb", "cba"};
    int n = 3;
    System.out.println("lexicographically smallest string = "
                                      + lexsmallest(a, n));

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 code to find the lexicographically
# smallest string
def lexSmallest(a, n):
  # Sort strings using above compare()
  for i in range(0,n):
    for j in range(i+1,n):
      if(a[i]+a[j]>a[j]+a[i]):
        s=a[i]
        a[i]=a[j]
        a[j]=s

  # Concatenating sorted strings
  answer = ""
  for i in range( n):
    answer += a[i]
  return answer

# Driver code
if __name__ == "__main__":

    a = [ "c", "cb", "cba" ]
    n = len(a)
    print(lexSmallest(a, n))

# This code is contributed by vibhu karnwal

```

## C#

```
// C# code to find
// the lexicographically
// smallest string
using System;

class GFG {

// function to sort the
// array of string
static void sort(String []a, int n)
{

    //sort the array
    for(int i = 0;i < n;i++)
    {
        for(int j = i + 1;j < n;j++)
        {

            // comparing which of the
            // two concatenation causes
            // lexicographically smaller
            // string
            if((a[i] + a[j]).CompareTo(a[j] +
                                  a[i]) > 0)
            {
                String s = a[i];
                a[i] = a[j];
                a[j] = s;
            }
        }
    }
}

static String lexsmallest(String []a, int n)
{

    // Sort strings
    sort(a,n);

    // Concatenating sorted
    // strings
    String answer = "";
    for (int i = 0; i < n; i++)
        answer += a[i];

    return answer;
}

// Driver code
public static void Main()
{
    String []a = {"c", "cb", "cba"};
    int n = 3;
    Console.Write("lexicographically smallest string = "
                                 + lexsmallest(a, n));

}
}

// This code is contributed by nitin mittal
```

## java 描述语言

```
<script>
// Javascript code to find the lexicographically
// smallest string

// function to sort the
// array of string
function sort(a,n)
{

    // sort the array
    for(let i = 0;i < n;i++)
    {
        for(let j = i + 1;j < n;j++)
        {

            // comparing which of the
            // two concatenation causes
            // lexicographically smaller
            // string
            if((a[i] + a[j])>(a[j] + a[i]) )
            {
                let s = a[i];
                a[i] = a[j];
                a[j] = s;
            }
        }
    }
}

function lexsmallest(a,n)
{
    // Sort strings
    sort(a,n);

    // Concatenating sorted strings
    let answer = "";
    for (let i = 0; i < n; i++)
        answer += a[i];

    return answer;
}

// Driver code
let a=["c", "cb", "cba"];
let n = 3;
document.write("lexicographically smallest string = "
                                      + lexsmallest(a, n));

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
cbacbc
```

**时间复杂度:**上面的代码在 O(M * N * logN)中运行，其中 N 是字符串的个数，M 是字符串的最大长度。