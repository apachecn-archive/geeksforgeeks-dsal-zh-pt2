# 用最小的变化做一个词典上最小的回文

> 原文:[https://www . geeksforgeeks . org/make-a-按字典序最小化-回文最小化-更改/](https://www.geeksforgeeks.org/make-a-lexicographically-smallest-palindrome-with-minimal-changes/)

给定一个字符串，打印字典中最小的字符串。您可以对字符串中的字符进行最小的更改，也可以对字符串进行置换。

示例:

```
Input : S = "aabc"
Output : "abba"

Input : S = "äabcd"
Output : "abcba"

```

**解释 1:** 把最后一个指标“c”改成“b”，就变成了“aabb”。然后重新排列弦，就变成了“阿爸”。这是字典上最小的字符串。
**解释二:**将“d”改为“b”=>“aabcb”=>“abcba”。

**方法:**
cnt[a]是字符 a 出现的次数，考虑 cnt[a]的奇数，那么一个回文不能包含一个以上带有 cnt[a]的字符 a。用奇数计数 cnt[]表示字符，如下 a <sub>1</sub> ，a <sub>2</sub> …。a <sub>k</sub> (按字母顺序排列)。将符号 a <sub>k</sub> 替换为符号 a <sub>1</sub> ，将符号 a <sub>k-1</sub> 替换为符号 a <sub>2</sub> 等等，直到上述顺序的中间。现在，只有一个奇怪的符号。放在答案中间。答案的前半部分将由符号 a 的![cnt[a]/2](img/b488567ad5385ee1eac51460209a19d0.png "Rendered by QuickLaTeX.com")出现组成。后半部分将以相反的顺序包含相同的符号。
**例:**

```
  take string S =  "aabcd"
  cnt[a] = 2, cnt[b] = 1, cnt = 1, cnt[d] = 1.
 Odd characters => b, c, d
  replace ak('d') with a1('b') we get => b, c, b.
  cnt[b] = 2, cnt = 1.Place odd character in middle 
   and 'a' and 'b' in first half and also in second half,
   we get "abcba".

```

## C++

```
// CPP code for changing a string
// into lexicographically smallest
// pallindromic string
#include <bits/stdc++.h>
using namespace std;

// Function to create a palindrome
int Palindrome(string s, int n)
{
    unordered_map<char, int> cnt;
    string R = "";

    // Count the occurrences of
    // every character in the string
    for (int i = 0; i < n; i++) {
        char a = s[i];
        cnt[a]++;
    }

    // Create a string of characters
    // with odd occurrences
    for (char i = 'a'; i <= 'z'; i++) {
        if (cnt[i] % 2 != 0)
            R += i;
    }

    int l = R.length();
    int j = 0;

    // Change the created string upto
    // middle element and update
    // count to make sure that only
    // one odd character exists.
    for (int i = l - 1; i >= l / 2; i--) {

        // decrease the count of
        // character updated
        cnt[R[i]]--;
        R[i] = R[j];
        cnt[R[j]]++;
        j++;
    }

    // Create three strings to make
    // first half second half and
    // middle one.
    string first, middle, second;

    for (char i = 'a'; i <= 'z'; i++) {
        if (cnt[i] != 0) {

            // characters with even occurrences
            if (cnt[i] % 2 == 0) {
                int j = 0;

                // fill the first half.
                while (j < cnt[i] / 2) {
                    first += i;
                    j++;
                }
            }

            // character with odd occurrence
            else {
                int j = 0;

                // fill the first half with
                // half of occurrence except one
                while (j < (cnt[i] - 1) / 2) {
                    first += i;
                    j++;
                }

                // For middle element
                middle += i;
            }
        }
    }

    // create the second half by
    // reversing the first half.
    second = first;
    reverse(second.begin(), second.end());
    string resultant = first + middle + second;
    cout << resultant << endl;
}

// Driver code
int main()
{
    string S = "geeksforgeeks";
    int n = S.length();
    Palindrome(S, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python code for changing a string
# into lexicographically smallest
# pallindromic string

# Function to create a palindrome
def palindrome(s: str, n: int) -> int:
    cnt = dict()
    R = []

    # Count the occurrences of
    # every character in the string
    for i in range(n):
        a = s[i]
        if a in cnt:
            cnt[a] += 1
        else:
            cnt[a] = 1

    # Create a string of characters
    # with odd occurrences
    i = 'a'
    while i <= 'z':
        if i in cnt and cnt[i] % 2 != 0:
            R += i
        i = chr(ord(i) + 1)

    l = len(R)
    j = 0

    # Change the created string upto
    # middle element and update
    # count to make sure that only
    # one odd character exists.
    for i in range(l - 1, (l // 2) - 1, -1):

        # decrease the count of
        # character updated
        if R[i] in cnt:
            cnt[R[i]] -= 1
        else:
            cnt[R[i]] = -1

        R[i] = R[j]

        if R[j] in cnt:
            cnt[R[j]] += 1
        else:
            cnt[R[j]] = 1
        j += 1

    # Create three strings to make
    # first half second half and
    # middle one.
    first, middle, second = "", "", ""

    i = 'a'
    while i <= 'z':
        if i in cnt:

            # characters with even occurrences
            if cnt[i] % 2 == 0:
                j = 0

                # fill the first half.
                while j < cnt[i] // 2:
                    first += i
                    j += 1

            # character with odd occurrence
            else:
                j = 0

                # fill the first half with
                # half of occurrence except one
                while j < (cnt[i] - 1) // 2:
                    first += i
                    j += 1

                # For middle element
                middle += i
        i = chr(ord(i) + 1)

    # create the second half by
    # reversing the first half.
    second = first
    second = ''.join(reversed(second))
    resultant = first + middle + second
    print(resultant)

# Driver Code
if __name__ == "__main__":

    S = "geeksforgeeks"
    n = len(S)
    palindrome(S, n)

# This code is contributed by
# sanjeev2552
```

**Output:**

```
 eefgksoskgfee

```