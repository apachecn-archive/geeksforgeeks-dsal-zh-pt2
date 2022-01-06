# 可以用 N 卢比购买的最大升水量

> 原文:[https://www . geeksforgeeks . org/n 卢比可购买的最大升水量/](https://www.geeksforgeeks.org/maximum-litres-of-water-that-can-be-bought-with-n-rupees/)

给![N ](img/479cbec0e01453d6ddc99e257783bb88.png "Rendered by QuickLaTeX.com")卢比。一升**塑料瓶**水需要![A ](img/d1a0ee89cb1a1e0b2aaae4707c872b24.png "Rendered by QuickLaTeX.com")卢比，一升**玻璃瓶**水需要![B ](img/7e3f0162c462aaf16196732829441c73.png "Rendered by QuickLaTeX.com")卢比。但是购买后的空玻璃瓶可以兑换![C ](img/c8645c4aeec42ebc950e043b8e45b902.png "Rendered by QuickLaTeX.com")卢比。找到用![N ](img/479cbec0e01453d6ddc99e257783bb88.png "Rendered by QuickLaTeX.com")卢比可以买到的最大升水。
**举例:**

> **输入:** N = 10，A = 11，B = 9，C = 8
> **输出:** 2
> 可以买一个玻璃瓶，然后可以退货再买一个玻璃瓶
> **输入:** N = 15，A = 6，B = 4，C = 3
> **输出:** 12

**方法:**如果我们至少有![b ](img/0420d5d1d372a7e46d5d3b7e9aa62581.png "Rendered by QuickLaTeX.com")的钱，那么一个玻璃瓶的成本是**b–c**。这意味着如果**a≤(b–c)**那么我们就不需要买玻璃瓶了，只买塑料瓶，答案就是**地板(n / a)** 。否则，我们需要尽可能地购买玻璃瓶。
所以，如果我们至少有![b ](img/0420d5d1d372a7e46d5d3b7e9aa62581.png "Rendered by QuickLaTeX.com")的钱，那么我们会买**的地板((n–c)/(b–c))**的玻璃瓶，然后把剩下的钱花在塑料的上。
以下是上述方法的实施:

## C++

```
// CPP implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

void maxLitres(int budget,int plastic,int glass,int refund)
{

    // if buying glass bottles is profitable
    if (glass - refund < plastic)
       {
           // Glass bottles that can be bought
        int ans = max((budget - refund) / (glass - refund), 0);

        // Change budget according the bought bottles
        budget -= ans * (glass - refund);

        // Plastic bottles that can be bought
        ans += budget / plastic;
        cout<<ans<<endl;
       }

    // if only plastic bottles need to be bought
    else
        cout<<(budget / plastic)<<endl;
}

// Driver Code
int main()
{
    int budget = 10, plastic=11, glass=9, refund =  8;
    maxLitres(budget, plastic, glass, refund);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    static void maxLitres(int budget, int plastic,
                            int glass, int refund)
    {

        // if buying glass bottles is profitable
        if (glass - refund < plastic)
        {

            // Glass bottles that can be bought
            int ans = Math.max((budget - refund) / (glass - refund), 0);

            // Change budget according the bought bottles
            budget -= ans * (glass - refund);

            // Plastic bottles that can be bought
            ans += budget / plastic;
            System.out.println(ans);
        }

        // if only plastic bottles need to be bought
        else
        {
            System.out.println((budget / plastic));
        }

    }

    // Driver Code
    public static void main(String[] args)
    {
        int budget = 10, plastic = 11, glass = 9, refund = 8;
        maxLitres(budget, plastic, glass, refund);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

def maxLitres(budget, plastic, glass, refund):

    # if buying glass bottles is profitable
    if glass - refund < plastic:

        # Glass bottles that can be bought
        ans = max((budget - refund) // (glass - refund), 0)

        # Change budget according the bought bottles
        budget -= ans * (glass - refund)

        # Plastic bottles that can be bought
        ans += budget // plastic
        print(ans)

    # if only plastic bottles need to be bought
    else:
        print(budget // plastic)

# Driver Code
budget, plastic, glass, refund = 10, 11, 9, 8
maxLitres(budget, plastic, glass, refund)
```

## C#

```
// C# implementation of the above approach
using System;   

class GFG
{

    static void maxLitres(int budget, int plastic,
                            int glass, int refund)
    {

        // if buying glass bottles is profitable
        if (glass - refund < plastic)
        {

            // Glass bottles that can be bought
            int ans = Math.Max((budget - refund) / (glass - refund), 0);

            // Change budget according the bought bottles
            budget -= ans * (glass - refund);

            // Plastic bottles that can be bought
            ans += budget / plastic;
            Console.WriteLine(ans);
        }

        // if only plastic bottles need to be bought
        else
        {
            Console.WriteLine((budget / plastic));
        }

    }

    // Driver Code
    public static void Main(String[] args)
    {
        int budget = 10, plastic = 11, glass = 9, refund = 8;
        maxLitres(budget, plastic, glass, refund);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

function maxLitres($budget, $plastic,
                   $glass, $refund)
{

    // if buying glass bottles is profitable
    if ($glass - $refund < $plastic)
    {
        // Glass bottles that can be bought
        $ans = max((int)($budget - $refund) /
                        ($glass - $refund), 0);

        // Change budget according the bought bottles
        $budget -= $ans * ($glass - $refund);

        // Plastic bottles that can be bought
        $ans += (int)($budget / $plastic);
        echo $ans . "\n";
    }

    // if only plastic bottles need to be bought
    else
        echo (int)($budget / $plastic) . "\n";
}

// Driver Code
$budget = 10;
$plastic = 11;
$glass = 9;
$refund = 8;
maxLitres($budget, $plastic,
          $glass, $refund);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    function maxLitres(budget, plastic,
                            glass, refund)
    {

        // if buying glass bottles is profitable
        if (glass - refund < plastic)
        {

            // Glass bottles that can be bought
            let ans = Math.max((budget - refund) / (glass - refund), 0);

            // Change budget according the bought bottles
            budget -= ans * (glass - refund);

            // Plastic bottles that can be bought
            ans += Math.floor(budget / plastic);
            document.write(ans);
        }

        // if only plastic bottles need to be bought
        else
        {
            document.write(Math.floor(budget / plastic));
        }

    }

    // Driver code

    let budget = 10, plastic = 11, glass = 9, refund = 8;
    maxLitres(budget, plastic, glass, refund);

</script>
```

**Output:** 

```
2
```