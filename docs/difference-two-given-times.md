# 两个给定时间之间的差值

> 原文:[https://www.geeksforgeeks.org/difference-two-given-times/](https://www.geeksforgeeks.org/difference-two-given-times/)

以字符串“HH:MM”格式给出两次。这里“H”表示小时，“M”表示分钟。您必须找出这两个字符串在相同字符串格式中的区别。但是两个给定的字符串都应该遵循这些情况。
1)时间 1 将小于或等于时间 2
2)小时将可能从 0 到 23。
3)分钟可以从 0 到 59
举例:

```
Input : s1 = "14:00";
        s2 = "16:45";
Output : result = "2:45"

Input : s1 = "1:04"
        s2 = "13:05"
Output : result = "12:01"
```

想法是先切除结肠。去掉冒号后，小时差可以用简单的数学计算出来。

## C++

```
// C++ program to find difference between two
// given times.
#include <bits/stdc++.h>
using namespace std;

// remove ':' and convert it into an integer
int removeColon(string s)
{
    if (s.size() == 4)
        s.replace(1, 1, "");

    if (s.size() == 5)
        s.replace(2, 1, "");

    return stoi(s);
}

// Main function which finds difference
string diff(string s1, string s2)
{

    // change string (eg. 2:21 --> 221, 00:23 --> 23)
    int time1 = removeColon(s1);
    int time2 = removeColon(s2);

    // difference between hours
    int hourDiff = time2 / 100 - time1 / 100 - 1;

    // difference between minutes
    int minDiff = time2 % 100 + (60 - time1 % 100);

    if (minDiff >= 60) {
        hourDiff++;
        minDiff = minDiff - 60;
    }

    // convert answer again in string with ':'

    string res = to_string(hourDiff) + ':' + to_string(minDiff);
    return res;
}

// Driver program to test above functions
int main()
{
    string s1 = "14:00";
    string s2 = "16:45";
    cout << diff(s1, s2) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program to find difference between two
# given times.

# Remove ':' and convert it into an integer
def removeColon(s):

    if (len(s) == 4):
        s = s[:1] + s[2:]

    if (len(s) == 5):
        s = s[:2] + s[3:]

    return int(s)

# Main function which finds difference
def diff(s1, s2):

    # Change string
    # (eg. 2:21 --> 221, 00:23 --> 23)
    time1 = removeColon(s1)
    time2 = removeColon(s2)

    # Difference between hours
    hourDiff = time2 // 100 - time1 // 100 - 1;

    # Difference between minutes
    minDiff = time2 % 100 + (60 - time1 % 100)

    if (minDiff >= 60):
        hourDiff += 1
        minDiff = minDiff - 60

    # Convert answer again in string with ':'
    res = str(hourDiff) + ':' + str(minDiff)

    return res

# Driver code
s1 = "14:00"
s2 = "16:45"

print(diff(s1, s2))

# This code is contributed by ApurvaRaj
```

## java 描述语言

```
<script>
// JavaScript program to find difference between two
// given times.

// remove ':' and convert it into an integer
function removeColon( s)
{
    if (s.length == 4)
        s= s.replace(":", "");

    if (s.length == 5)
        s= s.replace(":", "");

    return parseInt(s);
}

// Main function which finds difference
function diff( s1,  s2)
{

    // change string (eg. 2:21 --> 221, 00:23 --> 23)
     time1 = removeColon(s1);

     time2 = removeColon(s2);

    // difference between hours
     hourDiff = parseInt(time2 / 100 - time1 / 100 - 1);

    // difference between minutes
     minDiff = parseInt(time2 % 100 + (60 - time1 % 100));

    if (minDiff >= 60) {
        hourDiff++;
        minDiff = minDiff - 60;
    }

    // convert answer again in string with ':'
    res = (hourDiff).toString() + ':' + (minDiff).toString();
    return res;
}

// Driver program to test above functions
    s1 = "14:00";
    s2 = "16:45";
    console.log(diff(s1, s2));

// This code is contributed by ukasp.
</script>
```

输出:

```
2:45
```

本文由 **Harshit Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。