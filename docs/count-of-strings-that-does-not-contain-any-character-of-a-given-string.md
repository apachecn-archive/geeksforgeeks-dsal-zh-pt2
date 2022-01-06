# 不包含给定字符串的任何字符的字符串计数

> 原文:[https://www . geesforgeks . org/不包含任何给定字符串字符的字符串计数/](https://www.geeksforgeeks.org/count-of-strings-that-does-not-contain-any-character-of-a-given-string/)

给定一个包含 **N** 字符串的数组 **arr** 和一个字符串 **str** ，任务是找出不包含字符串 **str** 任何字符的字符串数量。

**示例:**

> **输入:**arr[]= {“ABCD”、“hijk”、“xyz”、“ayt”}，str =“apple”
> **输出:** 2
> **说明:**“hijk”和“xyz”是不包含 str 任何字符的字符串
> 
> **输入:** arr[] = {“苹果”、“香蕉”、“梨”}，str = " nil "
> T3】输出: 1

**方法:**按照以下步骤解决这个问题:

1.  创建一个集合 **st** ，并将字符串的每个字符存储在这个集合中。
2.  创建一个变量**和**来存储所有需要的字符串的数量。
3.  现在，开始遍历数组，对于每个字符串，检查它的任何字符是否存在于 set st 中。如果是，则这不是必需的字符串。
4.  如果它不包含集合中的任何字符，则将答案增加 1。
5.  循环结束后返回 **ans** ，作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of strings
// that does not contain any character of string str
int allowedStrings(vector<string>& arr, string str)
{
    int ans = 0;
    unordered_set<char> st;
    for (auto x : str) {
        st.insert(x);
    }

    for (auto x : arr) {
        bool allowed = 1;
        for (auto y : x) {

            // If the character is present in st
            if (st.find(y) != st.end()) {
                allowed = 0;
                break;
            }
        }

        // If the string doesn't
        // have any character of st
        if (allowed) {
            ans += 1;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<string> arr
        = { "abcd", "hijk", "xyz", "ayt" };
    string str = "apple";
    cout << allowedStrings(arr, str);
}
```

## 蟒蛇 3

```
# Python 3 code for the above approach

# Function to count the number of strings
# that does not contain any character of string str
def allowedStrings(arr, st):
    ans = 0
    st1 = set([])
    for x in st:
        st1.add(x)

    for x in arr:
        allowed = 1
        for y in x:

            # If the character is present in st1
            if (y in st1):
                allowed = 0
                break

        # If the string doesn't
        # have any character of st
        if (allowed):
            ans += 1

    return ans

# Driver Code
if __name__ == "__main__":

    arr = ["abcd", "hijk", "xyz", "ayt"]
    st = "apple"
    print(allowedStrings(arr, st))

    # This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to count the number of strings
// that does not contain any character of string str
function allowedStrings(arr, str)
{
    let ans = 0;
    let st = new Set();
    for (x of str) {
        st.add(x);
    }

    for (x of arr) {
        let allowed = 1;
        for (y of x) {

            // If the character is present in st
            if (st.has(y)) {
                allowed = 0;
                break;
            }
        }

        // If the string doesn't
        // have any character of st
        if (allowed) {
            ans += 1;
        }
    }

    return ans;
}

// Driver Code

let arr = ["abcd", "hijk", "xyz", "ayt"];
let str = "apple";
document.write(allowedStrings(arr, str));

// This code is contributed by gfgking.
</script>
```

**Output**

```
2
```

**时间复杂度:** O(N*M)，其中 N 是数组的大小，M 是最长字符串的大小。
**辅助空间:** O(N)