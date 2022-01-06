# 统计每个字符最多出现 k 次的子串

> 原文:[https://www . geesforgeks . org/count-substrings-character-occurrent-k-times/](https://www.geeksforgeeks.org/count-substrings-character-occurring-k-times/)

给定一个字符串，计算每个字符最多出现 k 次的子字符串数。假设字符串仅由小写英文字母组成。
**例:**

```
Input : S = ab
        k = 1
Output : 3
All the substrings a, b, ab have
individual character count less than 1\. 

Input : S = aaabb
        k = 2
Output : 12
Substrings that have individual character
count at most 2 are: a, a, a, b, b, aa, aa,
ab, bb, aab, abb, aabb.
```

一个**简单的**解决方法是先找到所有的子串，然后检查每个子串中每个字符的个数是否最多为 k。这个解决方案的时间复杂度是 O(n^3).
一个**高效的**解决方案是维护子串的起点和终点。让我们把起始点固定在一个索引 I 上，每次递增一个结束点 j。更改结束点时，更新相应字符的计数。然后检查这个子串，看每个字符的计数是否最多为 k。如果是，则将答案增加 1，否则增加起点并重置终点。起点增加是因为在终点的最后一次更新中，字符数超过了 k，而且只会进一步增加。所以给定固定起点的后续子串不会是每个字符数最多 k 的子串
**实现:**

## C++

```
// CPP program to count number of substrings
// in which each character has count less
// than or equal to k.
#include <bits/stdc++.h>

using namespace std;

int findSubstrings(string s, int k)
{
    // variable to store count of substrings.
    int ans = 0;

    // array to store count of each character.
    int cnt[26];

    int i, j, n = s.length();
    for (i = 0; i < n; i++) {

        // Initialize all characters count to zero.
        memset(cnt, 0, sizeof(cnt));

        for (j = i; j < n; j++) {
            // increment character count
            cnt[s[j] - 'a']++;

            // check only the count of current character
            // because only the count of this
            // character is changed. The ending point is
            // incremented to current position only if
            // all other characters have count at most
            // k and hence their count is not checked.
            // If count is less than k, then increase ans
            // by 1.
            if (cnt[s[j] - 'a'] <= k)
                ans++;

            // if count is less than k, then break as
            // subsequent substrings for this starting
            // point will also have count greater than
            // k and hence are reduntant to check.
            else
                break;
        }
    }

    // return the final count of substrings.
    return ans;
}

// Driver code
int main()
{
    string S = "aaabb";
    int k = 2;
    cout << findSubstrings(S, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java program to count number of substrings
// in which each character has count less
// than or equal to k.
class GFG {

    static int findSubstrings(String s, int k) {
        // variable to store count of substrings.
        int ans = 0;

        // array to store count of each character.
        int cnt[] = new int[26];

        int i, j, n = s.length();
        for (i = 0; i < n; i++) {

            // Initialize all characters count to zero.
            Arrays.fill(cnt, 0);

            for (j = i; j < n; j++) {
                // increment character count
                cnt[s.charAt(j) - 'a']++;

                // check only the count of current character
                // because only the count of this
                // character is changed. The ending point is
                // incremented to current position only if
                // all other characters have count at most
                // k and hence their count is not checked.
                // If count is less than k, then increase ans
                // by 1.
                if (cnt[s.charAt(j) - 'a'] <= k) {
                    ans++;
                } // if count is less than k, then break as
                // subsequent substrings for this starting
                // point will also have count greater than
                // k and hence are reduntant to check.
                else {
                    break;
                }
            }
        }

        // return the final count of substrings.
        return ans;
    }

// Driver code
    static public void main(String[] args) {
        String S = "aaabb";
        int k = 2;
        System.out.println(findSubstrings(S, k));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count number of substrings
# in which each character has count less
# than or equal to k.

def findSubstrings(s, k):

    # variable to store count of substrings.
    ans = 0
    n = len(s)
    for i in range(n):

        # array to store count of each character.
        cnt = [0] * 26

        for j in range(i, n):

            # increment character count
            cnt[ord(s[j]) - ord('a')] += 1

            # check only the count of current character
            # because only the count of this
            # character is changed. The ending point is
            # incremented to current position only if
            # all other characters have count at most
            # k and hence their count is not checked.
            # If count is less than k, then increase
            # ans by 1.

            if (cnt[ord(s[j]) - ord('a')] <= k):
                ans += 1

            # if count is less than k, then break as
            # subsequent substrings for this starting
            # point will also have count greater than
            # k and hence are reduntant to check.
            else:
                break

    # return the final count of substrings.
    return ans

# Driver code
if __name__ == "__main__":

    S = "aaabb"
    k = 2
    print(findSubstrings(S, k))

# This code is contributed by ita_c
```

## C#

```
// C# program to count number of substrings
// in which each character has count less
// than or equal to k.
using System;

class GFG
{

public static int findSubstrings(string s, int k)
{
    // variable to store count of substrings.
    int ans = 0;

    // array to store count of each character.
    int []cnt = new int[26];

    int i, j, n = s.Length;
    for (i = 0; i < n; i++)
    {

        // Initialize all characters count to zero.
        Array.Clear(cnt, 0, cnt.Length);

        for (j = i; j < n; j++)
        {

            // increment character count
            cnt[s[j] - 'a']++;

            // check only the count of current character
            // because only the count of this
            // character is changed. The ending point is
            // incremented to current position only if
            // all other characters have count at most
            // k and hence their count is not checked.
            // If count is less than k, then increase ans
            // by 1.
            if (cnt[s[j] - 'a'] <= k)
                ans++;

            // if count is less than k, then break as
            // subsequent substrings for this starting
            // point will also have count greater than
            // k and hence are reduntant to check.
            else
                break;
        }
    }

    // return the final count of substrings.
    return ans;
}

// Driver code
public static int Main()
{
    string S = "aaabb";
    int k = 2;
    Console.WriteLine(findSubstrings(S, k));
    return 0;
}
}

// This code is contributed by SoM15242.
```

## java 描述语言

```
<script>

// Javascript program to count number of substrings
// in which each character has count less
// than or equal to k.

function findSubstrings(s, k)
{
    // variable to store count of substrings.
    var ans = 0;

    // array to store count of each character.
    var cnt = Array(26);

    var i, j, n = s.length;
    for (i = 0; i < n; i++) {
        cnt = Array(26).fill(0);
        for (j = i; j < n; j++) {

            // increment character count
            cnt[(s[j].charCodeAt(0) - 'a'.charCodeAt(0))]++;

            // check only the count of current character
            // because only the count of this
            // character is changed. The ending point is
            // incremented to current position only if
            // all other characters have count at most
            // k and hence their count is not checked.
            // If count is less than k, then increase ans
            // by 1.
            if (cnt[(s[j].charCodeAt(0) - 'a'.charCodeAt(0))] <= k)
                ans++;

            // if count is less than k, then break as
            // subsequent substrings for this starting
            // point will also have count greater than
            // k and hence are reduntant to check.
            else
                break;
        }
    }

    // return the final count of substrings.
    return ans;
}

// Driver code
var S = "aaabb";
var k = 2;
document.write( findSubstrings(S, k));

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
 12
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(1)
另一个**高效的**解决方案是使用滑动窗口技术。其中我们将保持左右两个指针。我们将左指针和右指针初始化为 0，移动右指针，直到每个字母表的计数小于 k，当计数大于 k 时，我们开始递增左指针并递减相应字母表的计数，一旦条件满足，我们将答案加上(右-左+ 1)。
**实施:**

## C++

```
// CPP program to count number of substrings
// in which each character has count less
// than or equal to k.
#include<bits/stdc++.h>

using namespace std;

//function to find number of substring
//in which each character has count less
// than or equal to k.

int find_sub(string s,int k){
    int len=s.length();
    int lp=0,rp=0;             // initialize left and right pointer to 0
    int ans=0;
    int hash_char[26]={0};     // an array to keep track of count of each alphabet
    for(;rp<len;rp++){
        hash_char[s[rp]-'a']++;
        while(hash_char[s[rp]-'a']>k){
            hash_char[s[lp]-'a']--;   // decrement the count
            lp++;         //increment left pointer
        }
        ans+=rp-lp+1;
    }
    return ans;
}

// Driver code
int main(){
    string s="aaabb";
    int k=2;
    cout<<find_sub(s,k)<<endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of substrings
// in which each character has count less
// than or equal to k.
class GFG
{

    //function to find number of substring
    //in which each character has count less
    // than or equal to k.
    static int find_sub(String s, int k)
    {
        int len = s.length();

        // initialize left and right pointer to 0
        int lp = 0, rp = 0;
        int ans = 0;

        // an array to keep track of count of each alphabet
        int[] hash_char = new int[26];
        for (; rp < len; rp++)
        {
            hash_char[s.charAt(rp) - 'a']++;
            while (hash_char[s.charAt(rp) - 'a'] > k)
            {
                // decrement the count
                hash_char[s.charAt(lp) - 'a']--;

                //increment left pointer
                lp++;
            }
            ans += rp - lp + 1;
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        String S = "aaabb";
        int k = 2;
        System.out.println(find_sub(S, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## 计算机编程语言

```
# Python3 program to count number of substrings
# in which each character has count less
# than or equal to k.

# function to find number of substring
# in which each character has count less
# than or equal to k.

def find_sub(s, k):

    Len = len(s)

    # initialize left and right pointer to 0
    lp, rp = 0, 0

    ans = 0

    # an array to keep track of count of each alphabet
    hash_char = [0 for i in range(256)]   
    for rp in range(Len):

        hash_char[ord(s[rp])] += 1

        while(hash_char[ord(s[rp])] > k):
            hash_char[ord(s[lp])] -= 1 # decrement the count
            lp += 1         #increment left pointer

        ans += rp - lp + 1

    return ans

# Driver code
s = "aaabb"
k = 2;
print(find_sub(s, k))

# This code is contributed by mohit kumar
```

## C#

```
// C# program to count number of substrings
// in which each character has count less
// than or equal to k.
using System;

class GFG
{
    //function to find number of substring
    //in which each character has count less
    // than or equal to k.
    static int find_sub(string s, int k)
    {
        int len = s.Length;

        // initialize left and right pointer to 0
        int lp = 0,rp = 0;            
        int ans = 0;

        // an array to keep track of count of each alphabet
        int []hash_char = new int[26];    
        for(;rp < len; rp++)
        {
            hash_char[s[rp] - 'a']++;
            while(hash_char[s[rp] - 'a'] > k)
            {
                // decrement the count
                hash_char[s[lp] - 'a']--;

                 //increment left pointer
                lp++;       
            }
            ans += rp - lp + 1;
        }  
        return ans;
     }

    // Driver code
    static public void Main()
    {
        String S = "aaabb";
        int k = 2;
        Console.WriteLine(find_sub(S, k));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to count number of substrings
// in which each character has count less
// than or equal to k.

    //function to find number of substring
    //in which each character has count less
    // than or equal to k.
    function find_sub(s,k)
    {
        let len = s.length;

        // initialize left and right pointer to 0
        let lp = 0, rp = 0;
        let ans = 0;

        // an array to keep track of count of each alphabet
        let hash_char = new Array(26);
        for(let i = 0; i < hash_char.length; i++)
        {
            hash_char[i] = 0;
        }
        for (; rp < len; rp++)
        {
            hash_char[s[rp].charCodeAt(0) - 'a'.charCodeAt(0)]++;
            while (hash_char[s[rp].charCodeAt(0) - 'a'.charCodeAt(0)] > k)
            {

                // decrement the count
                hash_char[s[lp].charCodeAt(0) - 'a'.charCodeAt(0)]--;

                //increment left pointer
                lp++;
            }
            ans += rp - lp + 1;
        }
        return ans;
    }

    // Driver code
    let S = "aaabb";
    let k = 2;
    document.write(find_sub(S, k));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
 12
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)