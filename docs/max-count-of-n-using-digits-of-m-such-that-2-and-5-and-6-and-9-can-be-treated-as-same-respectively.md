# 使用 M 位数的 N 的最大计数，使得 2 和 5，以及，6 和 9 可以分别被视为相同

> 原文:[https://www . geeksforgeeks . org/max-count-of-n-use-digits-of-m-so-2-5-6-9-可分别视为相同/](https://www.geeksforgeeks.org/max-count-of-n-using-digits-of-m-such-that-2-and-5-and-6-and-9-can-be-treated-as-same-respectively/)

给定一个整数 **N** ，和[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)整数 **M** ，任务是利用[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **M** 的位数找到总计数使 **N** 。另外，数字 **2** 可以被视为数字 **5** ，数字 **6** 可以被视为数字 **9** ，反之亦然，来自[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **M** 的每个数字最多可以使用一次。

**示例:**

> **输入:** N = 6，M = "245769"
> **输出:** 2
> **说明:**数字 5 和 6 组成数字 56。数字 2 和 9 用来组成数字 56。As 2 被视为 5，而 9 被视为 6。
> 
> **输入:** N = 25，M =【55】
> T3】输出: 1

**方法:**给定的问题可以通过[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来解决。按照以下步骤解决问题:

*   创建一个空的[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)，比如说**映射**来存储给定的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **M** 的数字的频率。
*   创建一个变量，比如说 **len** 来存储[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)的长度。
*   [使用变量 **i** 和](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)[遍历给定字符串](https://www.geeksforgeeks.org/c-c-do-while-loop-with-examples/) **S** 迭代直到 I 的值小于 **len** 并执行以下步骤:
    *   如果字符 **S[i]** 等于 **'5'** ，则改为 **'2'** 。
    *   如果字符 **S[i]** 等于**‘9’**，则改为**‘6’。**
    *   如果字符出现在**我的地图**中，那么将频率更改为**我的地图。放(x，map.get(x)+1)。**
    *   否则，在地图中插入频率为 1 的字符作为 **mymap.put(x，1)** 。
    *   将频率添加到地图后，增加 **i** 并继续下一次迭代。
*   创建一个空的[散列表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)，比如**记下**来存储数字 **N.** 的数字
*   [迭代直到 **N** 的值大于 0，执行以下步骤:](https://www.geeksforgeeks.org/java-while-loop-with-examples/)
    *   创建一个变量，比如说 **rem** 来存储 **N** 的最后一位数字，使用模数运算符作为 **N%10** 。
    *   如果 **rem** 等于 **5** ，则改为 **2** 。
    *   如果 **rem** 等于 **9** ，则改为 **6** 。
    *   如果**雷姆**地图中存在**雷姆**，则将频率增加 1as **雷姆放(雷姆，雷姆拿(雷姆)+1)** 。
    *   否则，将其作为**rem . put(rem，1)** 插入到**rem**地图中。
    *   将 **N** 除以 10。
*   创建一个变量，比如说 **cnt** 来存储数字 **N** 的最大计数，这个最大计数可以使用[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **M** 的给定数字来形成。
*   [遍历地图](https://www.geeksforgeeks.org/traverse-through-a-hashmap-in-java/) **rems** ，并执行以下步骤:
    *   让地图中的每个物体都是**元素。**
    *   检查来自**元素**的**键**是否出现在字符串**的频率图**中。
    *   如果不存在，返回 0(如果字符串 M 中不存在来自 N 的数字，则不能形成数字 N)。
    *   通过将 **mymap** 中**键**的频率除以 **rems** map 中的频率作为**my map . get(key)/ele . getvalue()**来计算**计数**。
    *   更新 **cnt** 中所有迭代的最小值。
*   完成上述步骤后，打印 **cnt** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
int solve(int n, string str)
{

  // Store the frequency of digits
  // from  the given string M
  map<int,int>mymap;

  // Store length of the string M
  int len = str.size();

  // Loop to traverse the string
  for (int i = 0; i < len; i++) {
    char c = str[i];

    // Replace 5 with 2
    if (c == '5')
      c = '2';

    // Replace 9 with 6
    else if (c == '9')
      c = '6';

    // Get the int form of
    // the current character
    // in the string
    int c_int = c-'a';

    // Insert in the map
    if (mymap.find(c_int)!=mymap.end())
      mymap[c_int] += 1;
    else
      mymap[c_int] =1;
  }

  // Store all the digits of the
  // required number N
  map<int,int>rems;

  // Loop to get all the digits
  // from the number N
  while (n > 0) {

    // Get the last digit as
    // the remainder
    int rem = n % 10;

    // Replace 5 with 2
    if (rem == 5)
      rem = 2;

    // Replace 9 with 6
    if (rem == 9)
      rem = 6;

    // Insert the remainders
    // in the rems map
    if (rems.find(rem) != rems.end())
      rems[rem] += 1 ;
    else
      rems[rem] = 1;

    n = n / 10;
  }

  // Store the resultant count
  int cnt = 1e8;

  // Iterate through the rems map
  for (auto ele : rems) {

    // Get the key which is
    // a digit from the number
    // N to be formed
    int key = ele.first;

    // If not present in the
    // string M, number N that
    // cannot be formed
    if (mymap.find(key)==mymap.end())
      return 0;

    // Divide the frequency of
    // the digit from the string
    // M with the frequency of
    // the current remainder
    int temp = mymap[key]/ele.second;

    // Choose the minimum
    cnt = min(cnt, temp);
  }

  // Return the maximum count
  return cnt;
}

// Driver Code
int main()
{
  int N = 56;
  string M = "245769";
  cout<<solve(N, M)<<endl;
  return 0;
}

// This code is contributed by dwivediyash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.HashMap;
import java.util.Map;

public class GFG {

    // Function to find the count of
    // numbers that can be formed using
    // the given digits in the string
    int solve(int n, String str)
    {

        // Store the frequency of digits
        // from  the given string M
        HashMap<Integer, Integer> mymap
            = new HashMap<>();

        // Store length of the string M
        int len = str.length();

        // Loop to traverse the string
        for (int i = 0; i < len; i++) {
            char c = str.charAt(i);

            // Replace 5 with 2
            if (c == '5')
                c = '2';

            // Replace 9 with 6
            else if (c == '9')
                c = '6';

            // Get the int form of
            // the current character
            // in the string
            int c_int = Integer.parseInt(
                String.valueOf(c));

            // Insert in the map
            if (mymap.containsKey(c_int))
                mymap.put(
                    c_int, mymap.get(c_int) + 1);
            else
                mymap.put(c_int, 1);
        }

        // Store all the digits of the
        // required number N
        HashMap<Integer, Integer> rems
            = new HashMap<>();

        // Loop to get all the digits
        // from the number N
        while (n > 0) {

            // Get the last digit as
            // the remainder
            int rem = n % 10;

            // Replace 5 with 2
            if (rem == 5)
                rem = 2;
            // Replace 9 with 6
            if (rem == 9)
                rem = 6;

            // Insert the remainders
            // in the rems map
            if (rems.containsKey(rem))
                rems.put(rem, rems.get(rem) + 1);
            else
                rems.put(rem, 1);

            n = n / 10;
        }

        // Store the resultant count
        int cnt = Integer.MAX_VALUE;

        // Iterate through the rems map
        for (Map.Entry<Integer, Integer> ele : rems.entrySet()) {

            // Get the key which is
            // a digit from the number
            // N to be formed
            int key = ele.getKey();

            // If not present in the
            // string M, number N that
            // cannot be formed
            if (!mymap.containsKey(key))
                return 0;

            // Divide the frequency of
            // the digit from the string
            // M with the frequency of
            // the current remainder
            int temp = mymap.get(key)
                       / ele.getValue();

            // Choose the minimum
            cnt = Math.min(cnt, temp);
        }

        // Return the maximum count
        return cnt;
    }

    // Driver Code
    public static void main(String args[])
    {

        GFG obj = new GFG();
        int N = 56;
        String M = "245769";
        System.out.println(obj.solve(N, M));
    }
}
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the count of
// numbers that can be formed using
// the given digits in the string
function solve(n, str) {
  // Store the frequency of digits
  // from  the given string M
  let mymap = new Map();

  // Store length of the string M
  let len = str.length;

  // Loop to traverse the string
  for (let i = 0; i < len; i++) {
    let c = str.charAt(i);

    // Replace 5 with 2
    if (c == "5") c = "2";
    // Replace 9 with 6
    else if (c == "9") c = "6";

    // Get the int form of
    // the current character
    // in the string
    let c_int = parseInt(c);

    // Insert in the map
    if (mymap.has(c_int)) mymap.set(c_int, mymap.get(c_int) + 1);
    else mymap.set(c_int, 1);
  }

  // Store all the digits of the
  // required number N
  let rems = new Map();

  // Loop to get all the digits
  // from the number N
  while (n > 0) {
    // Get the last digit as
    // the remainder
    let rem = n % 10;

    // Replace 5 with 2
    if (rem == 5) rem = 2;
    // Replace 9 with 6
    if (rem == 9) rem = 6;

    // Insert the remainders
    // in the rems map
    if (rems.has(rem)) rems.set(rem, rems.get(rem) + 1);
    else rems.set(rem, 1);

    n = Math.floor(n / 10);
  }

  // Store the resultant count
  let cnt = Number.MAX_SAFE_INTEGER;

  // Iterate through the rems map
  for (let ele of rems) {
    // Get the key which is
    // a digit from the number
    // N to be formed
    let key = ele[0];

    // If not present in the
    // string M, number N that
    // cannot be formed
    if (!mymap.has(key)) return 0;

    // Divide the frequency of
    // the digit from the string
    // M with the frequency of
    // the current remainder
    let temp = mymap.get(key) / ele[1];

    // Choose the minimum
    cnt = Math.min(cnt, temp);
  }

  // Return the maximum count
  return cnt;
}

// Driver Code

let N = 56;
let M = "245769";
document.write(solve(N, M));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)