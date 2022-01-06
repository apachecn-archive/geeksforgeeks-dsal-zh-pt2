# 给定人员可以组成的最大团队数量

> 原文:[https://www . geeksforgeeks . org/给定人员可组成的最大团队数量/](https://www.geeksforgeeks.org/maximum-number-of-teams-that-can-be-formed-with-given-persons/)

给定两个整数 **N** 和 **M** ，分别表示**1 型**和**2 型**的人数。任务是找到这两种人可以组成的最大团队数量。一个团队可以包含 **2 名第 1 类人员和 1 名第 2 类人员**或 **1 名第 1 类人员和 2 名第 2 类人员**。
**示例:**

> **输入:** N = 2，M = 6
> T3】输出: 2
> (Type1，Type2，Type2)和(Type1，Type2，Type2)是两种可能的队伍。
> **输入:** N = 4，M = 5
> **输出:** 3

**方法:**贪婪的方法是从成员较多的组中选择 2 个人，从成员较少的组中选择 1 个人，并相应地更新每个组中的人数。终止条件是不能再组建团队。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if it possible
// to form a team with the given n and m
bool canFormTeam(int n, int m)
{

    // 1 person of Type1 and 2 persons of Type2
    // can be chosen
    if (n >= 1 && m >= 2)
        return true;

    // 1 person of Type2 and 2 persons of Type1
    // can be chosen
    if (m >= 1 && n >= 2)
        return true;

    // Cannot from a team
    return false;
}

// Function to return the maximum number of teams
// that can be formed
int maxTeams(int n, int m)
{
    // To store the required count of teams formed
    int count = 0;

    while (canFormTeam(n, m)) {
        if (n > m) {

            // Choose 2 persons of Type1
            n -= 2;

            // And 1 person of Type2
            m -= 1;
        }
        else {

            // Choose 2 persons of Type2
            m -= 2;

            // And 1 person of Type1
            n -= 1;
        }

        // Another team has been formed
        count++;
    }

    return count;
}

// Driver code
int main()
{
    int n = 4, m = 5;
    cout << maxTeams(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true
    // if it possible to form a
    // team with the given n and m
    static boolean canFormTeam(int n, int m)
    {

        // 1 person of Type1 and 2 persons
        // of Type2 can be chosen
        if (n >= 1 && m >= 2)
            return true;

        // 1 person of Type2 and 2 persons
        // of Type1 can be chosen
        if (m >= 1 && n >= 2)
            return true;

        // Cannot from a team
        return false;
    }

    // Function to return the maximum
    // number of teams that can be formed
    static int maxTeams(int n, int m)
    {
        // To store the required count
        // of teams formed
        int count = 0;

        while (canFormTeam(n, m))
        {
            if (n > m)
            {

                // Choose 2 persons of Type1
                n -= 2;

                // And 1 person of Type2
                m -= 1;
            }
            else
            {

                // Choose 2 persons of Type2
                m -= 2;

                // And 1 person of Type1
                n -= 1;
            }

            // Another team has been formed
            count++;
        }
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 4, m = 5;
        System.out.println(maxTeams(n, m));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function that returns true if it possible
# to form a team with the given n and m
def canFormTeam(n, m):

    # 1 person of Type1 and 2 persons of Type2
    # can be chosen
    if (n >= 1 and m >= 2):
        return True

    # 1 person of Type2 and 2 persons of Type1
    # can be chosen
    if (m >= 1 and n >= 2):
        return True

    # Cannot from a team
    return False

# Function to return the maximum number of teams
# that can be formed
def maxTeams(n, m):
    # To store the required count of teams formed
    count = 0

    while (canFormTeam(n, m)):
        if (n > m):
            # Choose 2 persons of Type1
            n -= 2

            # And 1 person of Type2
            m -= 1

        else:
            # Choose 2 persons of Type2
            m -= 2

            # And 1 person of Type1
            n -= 1

        # Another team has been formed
        count += 1

    return count

# Driver code
if __name__ == '__main__':
    n = 4
    m = 5
    print(maxTeams(n, m))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if it possible
// to form a team with the given n and m
static bool canFormTeam(int n, int m)
{

    // 1 person of Type1 and 2 persons
    //  of Type2 can be chosen
    if (n >= 1 && m >= 2)
        return true;

    // 1 person of Type2 and 2 persons
    // of Type1 can be chosen
    if (m >= 1 && n >= 2)
        return true;

    // Cannot from a team
    return false;
}

// Function to return the maximum
// number of teams that can be formed
static int maxTeams(int n, int m)
{
    // To store the required count
    // of teams formed
    int count = 0;

    while (canFormTeam(n, m))
    {
        if (n > m)
        {

            // Choose 2 persons of Type1
            n -= 2;

            // And 1 person of Type2
            m -= 1;
        }
        else
        {

            // Choose 2 persons of Type2
            m -= 2;

            // And 1 person of Type1
            n -= 1;
        }

        // Another team has been formed
        count++;
    }
    return count;
}

// Driver code
public static void Main()
{
    int n = 4, m = 5;
    Console.WriteLine(maxTeams(n, m));
}
}

// This code is contributed by
// tufan_gupta2000
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if it possible
// to form a team with the given n and m
function canFormTeam($n, $m)
{

    // 1 person of Type1 and 2 persons
    // of Type2 can be chosen
    if ($n >= 1 && $m >= 2)
        return true;

    // 1 person of Type2 and 2 persons
    // of Type1 can be chosen
    if ($m >= 1 && $n >= 2)
        return true;

    // Cannot from a team
    return false;
}

// Function to return the maximum number
// of teams that can be formed
function maxTeams($n, $m)
{

    // To store the required count
    // of teams formed
    $count = 0;

    while (canFormTeam($n, $m))
    {
        if ($n > $m)
        {

            // Choose 2 persons of Type1
            $n -= 2;

            // And 1 person of Type2
            $m -= 1;
        }
        else
        {

            // Choose 2 persons of Type2
            $m -= 2;

            // And 1 person of Type1
            $n -= 1;
        }

        // Another team has been formed
        $count++;
    }

    return $count;
}

// Driver code
$n = 4;
$m = 5;
echo maxTeams($n, $m);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach    
// Function that returns true

    // if it possible to form a
    // team with the given n and m
    function canFormTeam(n, m)
    {

        // 1 person of Type1 and 2 persons
        // of Type2 can be chosen
        if (n >= 1 && m >= 2)
            return true;

        // 1 person of Type2 and 2 persons
        // of Type1 can be chosen
        if (m >= 1 && n >= 2)
            return true;

        // Cannot from a team
        return false;
    }

    // Function to return the maximum
    // number of teams that can be formed
    function maxTeams(n , m)
    {

        // To store the required count
        // of teams formed
        var count = 0;

        while (canFormTeam(n, m))
        {
            if (n > m)
            {

                // Choose 2 persons of Type1
                n -= 2;

                // And 1 person of Type2
                m -= 1;
            }
            else
            {

                // Choose 2 persons of Type2
                m -= 2;

                // And 1 person of Type1
                n -= 1;
            }

            // Another team has been formed
            count++;
        }
        return count;
    }

    // Driver code
    var n = 4, m = 5;
    document.write(maxTeams(n, m));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
3
```