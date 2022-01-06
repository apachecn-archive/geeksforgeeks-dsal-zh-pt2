# 看两个人跳相同次数后是否相遇

> 原文:[https://www . geesforgeks . org/find-if-two-people-even-meet-after-同跳次数/](https://www.geeksforgeeks.org/find-if-two-people-ever-meet-after-same-number-of-jumps/)

两个人从两个不同的点 p1 和 p2 开始比赛。他们一次跳完 s1 和 s2 米。找出他们是否会在相同次数的跳跃后的某个点相遇。
**例:**

```
Input : p1 = 6, s1 = 3, 
        p2 = 8, s2 = 2
Output : Yes
Explanation: 6->9->12
             8->10->12
They meet after two jumps.

Input : p1 = 4, s1 = 4, 
        p2 = 8, s2 = 2
Output : Yes
Explanation: 4->8->12
             8->10->12

Input : p1 = 0, s1 = 2, 
        p2 = 5, s2 = 3
Output : No

Input : p1 = 42, s1 = 3, 
        p2 = 94, s2 = 2
Output : Yes
```

一个**简单的解决方法**就是让他们一个个跳下去。每次跳跃后，看它们是否是同一点。
一个**高效的解决方案**是基于以下事实:
由于起点总是不同的，如果满足以下条件，它们就会满足。
(1)速度不一样
(2)速度差除以初始点之间的总距离。

## C++

```
// C++ program to find any one of them
// can overtake the other
#include<bits/stdc++.h>
using namespace std;

// function to find if any one of them can
// overtake the other
bool sackRace(int p1, int s1, int p2, int s2){

    // Since starting points are always
    // different, they will meet if following
    // conditions are met.
    // (1) Speeds are not same
    // (2) Difference between speeds divide the
    //     total distance between initial points.   
    return ( (s1 > s2 && (p2 - p1) % (s1 - s2) == 0) ||
             (s2 > s1 && (p1 - p2) % (s2 - s1) == 0));
}

// driver program
int main()
{
    int p1 = 4, s1 = 4, p2 = 8, s2 = 2;
    sackRace(p1, s1, p2, s2)? cout << "Yes\n" :
                              cout << "No\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program to find any one of them
// can overtake the other
import java.util.Arrays;

public class GFG {

    // function to find if any one of
    // them can overtake the other
    static boolean sackRace(int p1, int s1,
                            int p2, int s2)
    {

        // Since starting points are
        // always different, they will
        // meet if following conditions
        // are met.
        // (1) Speeds are not same
        // (2) Difference between speeds
        // divide the total distance
        // between initial points.
        return ( (s1 > s2 && (p2 - p1) %
                    (s1 - s2) == 0) ||
                    (s2 > s1 && (p1 - p2)
                    % (s2 - s1) == 0));
    }

    public static void main(String args[])
    {
        int p1 = 4, s1 = 4, p2 = 8, s2 = 2;

        if(sackRace(p1, s1, p2, s2))
            System.out.println("Yes" );
        else
            System.out.println("No");

    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# python program to find any one of them
# can overtake the other

# function to find if any one of them can
# overtake the other
def sackRace(p1, s1, p2, s2):

    # Since starting points are always
    # different, they will meet if following
    # conditions are met.
    # (1) Speeds are not same
    # (2) Difference between speeds divide the
    #     total distance between initial points.
    return ( (s1 > s2 and (p2 - p1) % (s1 - s2) == 0)
         or (s2 > s1 and (p1 - p2) % (s2 - s1) == 0))

# driver program
p1 = 4
s1 = 4
p2 = 8
s2 = 2
if(sackRace(p1, s1, p2, s2)):
    print("Yes")
else:
    print("No")

# This code is contributed by Sam007
```

## C#

```
// C# program to find any one of them
// can overtake the other
using System;

class GFG {

    // function to find if any one of
    // them can overtake the other
    static bool sackRace(int p1, int s1,
                          int p2, int s2)
    {

        // Since starting points are
        // always different, they will
        // meet if following conditions
        // are met.
        // (1) Speeds are not same
        // (2) Difference between speeds
        // divide the total distance
        // between initial points.
        return ( (s1 > s2 && (p2 - p1) %
                       (s1 - s2) == 0) ||
                    (s2 > s1 && (p1 - p2)
                       % (s2 - s1) == 0));
    }

    // Driver code
    public static void Main()
    {
        int p1 = 4, s1 = 4, p2 = 8,
        s2 = 2;

        if(sackRace(p1, s1, p2, s2))
            Console.WriteLine("Yes" );
        else
            Console.WriteLine("No");

    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find any one of them
// can overtake the other

// function to find if any one of
// them can overtake the other
function sackRace($p1, $s1, $p2, $s2)
{

    // Since starting points are always
    // different, they will meet if following
    // conditions are met.
    // (1) Speeds are not same
    // (2) Difference between speeds divide the
    //     total distance between initial points.
    return (($s1 > $s2 && ($p2 - $p1) % ($s1 - $s2) == 0) ||
            ($s2 > $s1 && ($p1 - $p2) % ($s2 - $s1) == 0));
}

    // Driver Code
    $p1 = 4;
    $s1 = 4;
    $p2 = 8;
    $s2 = 2;
    if(sackRace($p1, $s1, $p2, $s2))
        echo "Yes\n" ;
    else
        echo "No\n";

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// JavaScript program to find any one of them
// can overtake the other

    // function to find if any one of
    // them can overtake the other
    function sackRace(p1, s1, p2, s2)
    {

        // Since starting points are
        // always different, they will
        // meet if following conditions
        // are met.
        // (1) Speeds are not same
        // (2) Difference between speeds
        // divide the total distance
        // between initial points.
        return ( (s1 > s2 && (p2 - p1) %
                    (s1 - s2) == 0) ||
                    (s2 > s1 && (p1 - p2)
                    % (s2 - s1) == 0));
    }

// Driver Code
        let p1 = 4, s1 = 4, p2 = 8, s2 = 2;

        if(sackRace(p1, s1, p2, s2))
            document.write("Yes" );
        else
            document.write("No");

// This code is contributed by susmitakundugoaldanga.
</script>
```

**输出:**

```
Yes
```

本文由**维沙尔·库马尔·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。