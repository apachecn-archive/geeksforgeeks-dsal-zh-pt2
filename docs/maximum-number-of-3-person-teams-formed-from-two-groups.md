# 两组最多组成 3 人团队

> 原文:[https://www . geeksforgeeks . org/最多 3 人小组-从两个小组组成/](https://www.geeksforgeeks.org/maximum-number-of-3-person-teams-formed-from-two-groups/)

给定两个整数 **N1** 和 **N2** 其中， **N1** 为第 1 组人数， **N2** 为第 2 组人数。任务是计算当从两个组中至少选择一个人时，可以组成的 3 人团队的最大数量。
**举例:**

> **输入:** N1 = 2，N2 = 8
> **输出:** 2
> 团队 1:来自第 2 组的 2 名成员和来自第 1 组的 1 名成员
> 更新:N1 = 1，N2 = 6
> 团队 2:来自第 2 组的 2 名成员和来自第 1 组的 1 名成员
> 更新:N1 = 0，N2 = 4
> 无法再组建团队。
> **输入:** N1 = 4，N2 = 5
> **输出:** 3

**进场:**从**成员较少**的队伍中选择一名**单人**，从**成员较多**的队伍中选择 **2 人**(尽可能)更新**计数=计数+ 1** 。最后打印**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of maximum teams possible
int maxTeams(int N1, int N2)
{

    int count = 0;

    // While it is possible to form a team
    while (N1 > 0 && N2 > 0 && N1 + N2 >= 3) {

        // Choose 2 members from group 1
        // and a single member from group 2
        if (N1 > N2) {
            N1 -= 2;
            N2 -= 1;
        }

        // Choose 2 members from group 2
        // and a single member from group 1
        else {
            N1 -= 1;
            N2 -= 2;
        }

        // Update the count
        count++;
    }

    // Return the count
    return count;
}

// Driver code
int main()
{

    int N1 = 4, N2 = 5;
    cout << maxTeams(N1, N2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Function to return the count
    // of maximum teams possible
    static int maxTeams(int N1, int N2)
    {

        int count = 0;

        // While it is possible to form a team
        while (N1 > 0 && N2 > 0 && N1 + N2 >= 3) {

            // Choose 2 members from group 1
            // and a single member from group 2
            if (N1 > N2) {
                N1 -= 2;
                N2 -= 1;
            }

            // Choose 2 members from group 2
            // and a single member from group 1
            else {
                N1 -= 1;
                N2 -= 2;
            }

            // Update the count
            count++;
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void main(String []args)
    {

        int N1 = 4, N2 = 5;
        System.out.println(maxTeams(N1, N2));

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of maximum teams possible
def maxTeams(N1, N2):

    count = 0

    # While it is possible to form a team
    while (N1 > 0 and N2 > 0 and N1 + N2 >= 3) :

        # Choose 2 members from group 1
        # and a single member from group 2
        if (N1 > N2):
            N1 -= 2
            N2 -= 1

        # Choose 2 members from group 2
        # and a single member from group 1
        else:
            N1 -= 1
            N2 -= 2

        # Update the count
        count=count+1

    # Return the count
    return count

# Driver code
N1 = 4
N2 = 5
print(maxTeams(N1, N2))

# This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach

using System;
class GFG
{
    // Function to return the count
    // of maximum teams possible
    static int maxTeams(int N1, int N2)
    {

        int count = 0;

        // While it is possible to form a team
        while (N1 > 0 && N2 > 0 && N1 + N2 >= 3) {

            // Choose 2 members from group 1
            // and a single member from group 2
            if (N1 > N2) {
                N1 -= 2;
                N2 -= 1;
            }

            // Choose 2 members from group 2
            // and a single member from group 1
            else {
                N1 -= 1;
                N2 -= 2;
            }

            // Update the count
            count++;
        }

        // Return the count
        return count;
    }

    // Driver code
    public static void Main()
    {

        int N1 = 4, N2 = 5;
        Console.WriteLine(maxTeams(N1, N2));

    }

}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of maximum teams possible
function maxTeams($N1, $N2)
{
    $count = 0 ;

    // While it is possible to form a team
    while ($N1 > 0 && $N2 > 0 &&
                $N1 + $N2 >= 3)
    {

        // Choose 2 members from group 1
        // and a single member from group 2
        if ($N1 > $N2)
        {
            $N1 -= 2;
            $N2 -= 1;
        }

        // Choose 2 members from group 2
        // and a single member from group 1
        else
        {
            $N1 -= 1;
            $N2 -= 2;
        }

        // Update the count
        $count++;
    }

    // Return the count
    return $count;
}

// Driver code
$N1 = 4 ;
$N2 = 5 ;

echo maxTeams($N1, $N2);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count
    // of maximum teams possible
    function maxTeams(N1, N2)
    {

        let count = 0;

        // While it is possible to form a team
        while (N1 > 0 && N2 > 0 && N1 + N2 >= 3) {

            // Choose 2 members from group 1
            // and a single member from group 2
            if (N1 > N2) {
                N1 -= 2;
                N2 -= 1;
            }

            // Choose 2 members from group 2
            // and a single member from group 1
            else {
                N1 -= 1;
                N2 -= 2;
            }

            // Update the count
            count++;
        }

        // Return the count
        return count;
    }

    let N1 = 4, N2 = 5;
      document.write(maxTeams(N1, N2));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
3
```