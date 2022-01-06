# 需要交付的最小项目数量

> 原文:[https://www . geeksforgeeks . org/最小待交付项目数/](https://www.geeksforgeeks.org/minimum-number-of-items-to-be-delivered/)

给定 N 个桶，每个桶包含 A[i]个项目。给定需要交付所有项目的 K 次旅行。一次只能从一个桶中取出物品。任务是告诉每次旅行需要交付的最小项目数，以便所有项目都可以在 K 次旅行中交付。
**条件:K > = N**
**示例** :

```
Input : 
N = 5
A[] = { 1, 3, 5, 7, 9 }
K = 10
Output : 3
By delivering 3 items at a time, 
Number of tours required for bucket 1 = 1
Number of tours required for bucket 2 = 1
Number of tours required for bucket 3 = 2
Number of tours required for bucket 4 = 3
Number of tours required for bucket 5 = 3
Total number of tours = 10

Input :
N = 10
A = 1, 4, 9, 16, 25, 36, 49, 64, 81, 100
k = 50
Output : 9
```

**接近**:需要找到每次发货的最小件数。因此，想法是从 1 迭代到桶中物品的最大值，并计算每个桶所需的旅行次数，并找到完整交付的旅行总数。第一个这样的小于或等于 K 的值给出了所需的数字。
以下是上述思路的实现:

## C++

```
//C++ program to find the minimum numbers of tours required
#include <bits/stdc++.h>

using namespace std;
int getMin(int N,int A[],int k)
{
    //Iterating through each possible 
   // value of minimum Items
   int maximum=0,tours=0;

   for(int i=0;i<N;i++)
       maximum=max(maximum,A[i]);

   for(int i=1;i<maximum+1;i++)
   {
       tours=0;
       for(int j=0;j<N;j++)
       {
           if(A[j]%i==0)//perfecctly Divisible 
           {
               tours+=A[j]/i;
           }else{
                // Not Perfectly Divisible means required
                // tours are Floor Division + 1
                tours += floor(A[j]/i) + 1;
           }
       }
       if(tours<=k)
       {
             // Return First Feasible Value found,
            // since it is also the minimum
            return i;
       }
   }

   return -1;
}
//Driver code
int main() 
{
  int a[]={1, 4, 9, 16, 25, 36, 49, 64, 81, 100};

  int n=sizeof(a)/sizeof(a[0]);

  int k=50;

  if(getMin(n,a,k)==-1)
   cout<<"Not Possible";
   else
   cout<<getMin(n,a,k);

}
//This code is contributed by Mohit kumar 29

```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum numbers of tours required
import java.util.*;
class solution
{

static int getMin(int N,int A[],int k)
{
    //Iterating through each possible 
// value of minimum Items
int maximum=0,tours=0;

for(int i=0;i<N;i++)
    maximum=Math.max(maximum,A[i]);

for(int i=1;i<maximum+1;i++)
{
    tours=0;
    for(int j=0;j<N;j++)
    {
        if(A[j]%i==0)//perfecctly Divisible 
        {
            tours+=A[j]/i;
        }else{
                // Not Perfectly Divisible means required
                // tours are Floor Division + 1
                tours += Math.floor(A[j]/i) + 1;
        }
    }
    if(tours<=k)
    {
            // Return First Feasible Value found,
            // since it is also the minimum
            return i;
    }
}

return -1;
}
//Driver code
public static void main(String args[]) 
{
int a[]={1, 4, 9, 16, 25, 36, 49, 64, 81, 100};

int n=a.length;

int k=50;

if(getMin(n,a,k)==-1)
System.out.println("Not Possible");
else
System.out.println(getMin(n,a,k));

}
}
//This code is contributed by 
// Surendra_Gangwar

```

## 蟒蛇 3

```
# Python3 program to find minimum numbers of 
# tours required

def getMin(N, A, k):

    # Iterating through each possible 
    # value of minimum Items
    for i in range(1, max(A)+1):
        tours = 0
        for j in range(0, len(A)):
            if(A[j]% i == 0):# Perfectly Divisible
                tours += A[j]/i

            else:
                # Not Perfectly Divisible means required
                # tours are Floor Division + 1
                tours += A[j]//i + 1 

        if(tours <= k):
            # Return First Feasible Value found,
            # since it is also the minimum
            return i 
    return "Not Possible"

# Driver Code
N = 10
A = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
k = 50
print(getMin(N, A, k))

```

## C#

```
// C# program to find the minimum 
// numbers of tours required
using System;

class GFG
{

static int getMin(int N, int [] A, int k)
{
    // Iterating through each possible 
    // value of minimum Items
    int maximum = 0,tours = 0;

    for(int i = 0; i < N; i++)
        maximum = Math.Max(maximum, A[i]);

    for(int i = 1; i < maximum + 1; i++)
    {
        tours = 0;
        for(int j = 0; j < N; j++)
        {
            if(A[j] % i == 0)// perfecctly Divisible 
        {
            tours += A[j] /i;
        }
        else
        {
                // Not Perfectly Divisible means required
                // tours are Floor Division + 1
                tours += (int)Math.Floor(A[j] / (i * 1.0)) + 1;
        }
    }
        if(tours <= k)
        {
            // Return First Feasible Value found,
            // since it is also the minimum
            return i;
        }
    }

    return -1;
}

// Driver code
public static void Main() 
{
    int []a = {1, 4, 9, 16, 25, 36, 49, 64, 81, 100};

    int n = 10;

    int k = 50;

    if(getMin(n, a, k) == -1)
        Console.WriteLine("Not Possible");
    else
        Console.WriteLine(getMin(n, a, k));
}
}

// This code is contributed by 
// Mohit kumar

```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum number
// of tours required

function getMin($N, $A, $k)
{

    // Iterating through each possible 
    // value of minimum Items
    $maximum = 0;
    $tours = 0;

    for($i = 0; $i < $N; $i++)
        $maximum = max($maximum, $A[$i]);

    for($i = 1; $i < $maximum + 1; $i++)
    {
        $tours = 0;
        for($j = 0; $j < $N; $j++)
        {
            if($A[$j] % $i == 0) // perfectly Divisible 
            {
                $tours += $A[$j] / $i;
            }
            else
            {
                // Not Perfectly Divisible means required
                // tours are Floor Division + 1
                $tours += floor($A[$j] / $i) + 1;
            }
        }

        if($tours <= $k)
        {
            // Return First Feasible Value found,
            // since it is also the minimum
            return $i;
        }
    }

    return -1;
}

// Driver code
$a = array(1, 4, 9, 16, 25, 36,
               49, 64, 81, 100);

$n = sizeof($a);

$k = 50;

if(getMin($n, $a, $k) == -1)
    echo "Not Possible";
else
    echo getMin($n, $a, $k);

// This code is contributed by ihritik
?>

```

## java 描述语言

```
<script>
// Javascript program to find the minimum numbers of tours required

function getMin(N,A,k)
{
    //Iterating through each possible 
// value of minimum Items
let maximum = 0, tours = 0;

for(let i = 0; i < N; i++)
    maximum=Math.max(maximum, A[i]);

for(let i = 1; i < maximum + 1; i++)
{
    tours = 0;
    for(let j = 0; j < N; j++)
    {
        if(A[j] % i == 0)//perfecctly Divisible 
        {
            tours+=Math.floor(A[j]/i);
        }else{
                // Not Perfectly Divisible means required
                // tours are Floor Division + 1
                tours += Math.floor(A[j]/i) + 1;
        }
    }
    if(tours<=k)
    {
            // Return First Feasible Value found,
            // since it is also the minimum
            return i;
    }
}

return -1;
}

//Driver code
let a = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100];
let n = a.length;
let k = 50;

if(getMin(n, a, k) == -1)
    document.write("Not Possible<br>");
else
    document.write(getMin(n, a, k));    

// This code is contributed by patel2127
</script>

```

**Output**

```
9
```