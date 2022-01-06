# 执行一次交换后可以获得的不同字符串的计数

> 原文:[https://www . geeksforgeeks . org/执行完全一次交换后可以获得的不同字符串计数/](https://www.geeksforgeeks.org/count-of-distinct-strings-that-can-be-obtained-after-performing-exactly-one-swap/)

给定一个包含小写英文字母字符的字符串。任务是计算恰好执行一次交换后可以获得的不同字符串的数量。

> **输入:** s =【极客】
> **输出:** 6
> **解释:**以下是正好做一次互换形成的字符串
> 字符串=【“egek”“eegk”“极客”“geke”“gkee”“keeg”】
> 因此，有 6 个截然不同的可能字符串。
> 
> **输入:**s**T3】=【ab】
> T5】输出:** 1

**方法:**这个问题可以用[hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)解决。按照以下步骤解决给定的问题。

*   [检查字符串中唯一元素的数量 **s**](https://www.geeksforgeeks.org/count-the-number-of-unique-characters-in-a-string-in-python/) 。
*   在地图中存储所有唯一字符的频率。
*   声明一个变量，比如说 **ans = 0** ，来存储不同可能字符串的数量。
*   迭代字符串，除了当前元素之外，增加**和**个元素，当前元素将用于构建新字符串。
*   再次迭代字符串，检查某些字符的频率是否大于 2。如果是这样，那么将答案增加 1，因为它们将只形成一个额外的唯一字符串。
*   返回 **ans** 作为最终答案。

下面是上述方法的实现

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of distinct
// string formed after one swap
long long countStrings(string S)
{
    long long N = S.size();

    // mp[] to store the frequency
    // of each character
    int mp[26] = { 0 };

    // For storing frequencies
    for (auto i : S) {
        mp[i - 'a']++;
    }
    long long ans = 0;
    for (auto i : S) {
        ans += N - mp[i - 'a'];
    }
    ans /= 2;

    for (int i = 0; i < 26; i++) {
        if (mp[i] >= 2) {
            ans++;
            break;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    string S = "geek";

    // Function Call
    long long ans = countStrings(S);
    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;
public class GFG
{

// Function to count number of distinct
// string formed after one swap
static long countStrings(String S)
{
    long N = S.length();

    // mp[] to store the frequency
    // of each character
    int mp[] = new int[26];
    for(int i = 0; i < 26; i++) {
        mp[i] = 0;
    }

    // For storing frequencies
    for (int i = 0; i < S.length(); i++) {
        mp[S.charAt(i) - 'a']++;
    }
    long ans = 0;
    for (int i = 0; i < S.length(); i++) {
        ans += N - mp[S.charAt(i) - 'a'];
    }
    ans /= 2;

    for (int i = 0; i < 26; i++) {
        if (mp[i] >= 2) {
            ans++;
            break;
        }
    }
    return ans;
}

// Driver code
public static void main(String args[])
{
    String S = "geek";

    // Function Call
    long ans = countStrings(S);
    System.out.println(ans);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to count number of distinct
// string formed after one swap
function countStrings(S)
{
    let N = S.length;

    // mp[] to store the frequency
    // of each character
    let mp = new Map();

    // For storing frequencies
    for(let i = 0; i < S.length; i++)
    {
        if (!mp.has(S[i].charCodeAt(0) - 'a'.charCodeAt(0)))
        {
            mp.set(S[i].charCodeAt(0) - 'a'.charCodeAt(0), 1);
        }
        else
        {
            mp.set(S[i].charCodeAt(0) -
                    'a'.charCodeAt(0),
                   mp.get(S[i].charCodeAt(0) -
                           'a'.charCodeAt(0)) + 1)
        }
    }
    let ans = 0;
    for(let i = 0; i < S.length; i++)
    {
        ans += N - mp.get(S[i].charCodeAt(0) -
                           'a'.charCodeAt(0));
    }
    ans = Math.floor(ans / 2)

    for(let i = 0; i < 26; i++)
    {
        if (mp.get(i) >= 2)
        {
            ans++;
            break;
        }
    }
    return ans;
}

// Driver Code
let S = "geek";

// Function Call
let ans = countStrings(S);
document.write(ans + '<br>')

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
6
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)