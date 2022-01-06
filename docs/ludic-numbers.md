# 路德数字

> 原文:[https://www.geeksforgeeks.org/ludic-numbers/](https://www.geeksforgeeks.org/ludic-numbers/)

Ludic 数是通过考虑自然数列表(从 2 开始)并在第 I 次迭代中移除第 I 个数(其中 I 从 2 开始)而获得的。在每次迭代中，第一个移除的数字是 Ludic。1 被认为是 Ludic。

> **生成 Ludic 数的过程:**
> Ludic = {1，…}
> 考虑 2、
> 2、3、4、5、6、7、8、9、10、11、12、13、14、15、16、17、18、19、20、21 …
> 
> 删除第二个数字，因为第一个数字是 2
> 3，5，7，9，11，13，15，17，19，21..
> 
> Ludic = {1，2，…}
> 
> 删除第三个数字，因为第一个数字是 3
> 5，7，11，13，17，19，22..
> 
> Ludic = {1，2，3，…}
> 
> 删除第五个数字，因为第一个数字是 5
> 5，7，11，13，17，19，22..
> 
> Ludic = {1，2，3，5，..}
> 
> 这一过程仍在继续..

过程类似于厄拉多塞的[筛。
给定一个数字 n，打印所有小于或等于 n 的 Ludic 数字](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

**示例:**

```
Input : n = 10
Output : 1, 2, 3, 5, 7

Input : n = 25
Output : 1, 2, 3, 5, 7, 11, 13, 17, 23, 25 
```

打印 Ludic 数字的想法很简单。我们创建一个大小列表，并使用上面说明的过程。在每次迭代中，我们删除每一个第 I 个数字，我们不删除当前的第一个数字，以便我们以后可以返回它。

## C++

```
// C++ code to print Lucid
// number smaller than or
// equal to n.
#include <bits/stdc++.h>
using namespace std;

// Returns a list containing
// all Ludic numbers smaller
// than or equal to n.
vector<int> getLudic(int n)
{
  // ludics list contain all
  // the ludic numbers
  vector<int> ludics;

  for (int i = 1; i <= n; i++) 
    ludics.push_back(i);

  // Here we have to start with
  // index 1 and will remove nothing
  // from the list
  for (int index = 1; index < ludics.size(); index++)
  {
    // Here first item should be included in the list
    // and the deletion is referred by this first item
    // in the loop .
    int first_ludic = ludics[index];

    // Remove_index variable is used to store
    // the next index which we want to delete
    int remove_index = index + first_ludic;

    while (remove_index < ludics.size())
    {
      // Removing the next item
      auto it = ludics.begin();
      it = it + remove_index;
      ludics.erase(it);

      // Remove_index is updated so that
      // we get the next index for deletion
      remove_index = remove_index + first_ludic - 1;
    }
  }

  return ludics;
}

// Driver code
int main()
{
  int n = 25;
  vector<int> ans = getLudic(n);
  cout << "[";

  for (int i = 0; i < ans.size() - 1; i++)
  {
    cout << ans[i] << ", ";
  }

  cout << ans[ans.size() - 1] << "]";
  return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to print Lucid number smaller than
// or equal to n.
import java.util.ArrayList;
import java.util.List;

public class Ludic {

    // Returns a list containing all Ludic numbers
    // smaller than or equal to n.
    public static List<Integer> getLudic(int n)
    {
        // ludics list contain all the ludic numbers
        List<Integer> ludics = new ArrayList<Integer>(n);
        for (int i = 1; i <= n; i++)
            ludics.add(i);

        // Here we have to start with index 1 and will remove nothing
        // from the list
        for (int index = 1; index < ludics.size(); index++) {

            // Here first item should be included in the list
            // and the deletion is referred by this first item
            // in the loop .
            int first_ludic = ludics.get(index);

            // remove_index variable is used to store
            // the next index which we want to delete
            int remove_index = index + first_ludic;
            while (remove_index < ludics.size()) {

                // removing the next item
                ludics.remove(remove_index);

                // remove_index is updated so that
                // we get the next index for deletion
                remove_index = remove_index + first_ludic - 1;
            }
        }
        return ludics;
    }

    public static void main(String[] srgs)
    {
        int n = 25;
        System.out.println(getLudic(n));
    }
}
```

## 蟒蛇 3

```
# Python3 code to print Lucid
# number smaller than or equal
# to n.

# Returns a list containing all
# Ludic numbers smaller than
# or equal to n.
def getLudic(n):

    # ludics list contain all
    # the ludic numbers
    ludics = []
    for i in range(1, n + 1):
        ludics.append(i)

    # Here we have to start with
    # index 1 and will remove
    # nothing from the list
    index = 1
    while(index != len(ludics)):

        # Here first item should be
        # included in the list and
        # the deletion is referred
        # by this first item
        # in the loop .
        first_ludic = ludics[index]

        # Remove_index variable is used
        # to store the next index which
        # we want to delete
        remove_index = index + first_ludic
        while(remove_index < len(ludics)):

            # Removing the next item
            ludics.remove(ludics[remove_index])

            # Remove_index is updated so that
            # we get the next index for deletion
            remove_index = remove_index + first_ludic - 1
        index += 1
    return ludics

# Driver code 
n = 25
print(getLudic(n))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# code to print Lucid number smaller
// than or equal to n.
using System;
using System.Collections;

class GFG{

// Returns a list containing all Ludic
// numbers smaller than or equal to n.
public static ArrayList getLudic(int n)
{

    // ludics list contain all the
    // ludic numbers
    ArrayList ludics = new ArrayList();

    for(int i = 1; i <= n; i++)
        ludics.Add(i);

    // Here we have to start with index 1
    // and will remove nothing from the list
    for(int index = 1;
            index < ludics.Count;
            index++)
    {

        // Here first item should be included
        // in the list and the deletion is
        // referred by this first item in the
        // loop .
        int first_ludic = (int)ludics[index];

        // remove_index variable is used to store
        // the next index which we want to delete
        int remove_index = index + first_ludic;

        while (remove_index < ludics.Count)
        {

            // Removing the next item
            ludics.Remove(ludics[remove_index]);

            // remove_index is updated so that
            // we get the next index for deletion
            remove_index = remove_index +
                            first_ludic - 1;
        }
    }
    return ludics;
}

// Driver code
public static void Main(string[] srgs)
{
    int n = 25;

    ArrayList tmp = getLudic(n);

    Console.Write("[");
    foreach(int x in tmp)
    {
        Console.Write(x + ", ");
    }
    Console.Write("]");
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript code to print Lucid number smaller than
// or equal to n.

// Returns a list containing all Ludic numbers
    // smaller than or equal to n.
function  getLudic(n)
{

    // ludics list contain all the ludic numbers
        let ludics = [];
        for (let i = 1; i <= n; i++)
            ludics.push(i);

        // Here we have to start with index 1 and will remove nothing
        // from the list
        for (let index = 1; index < ludics.length; index++) {

            // Here first item should be included in the list
            // and the deletion is referred by this first item
            // in the loop .
            let first_ludic = ludics[index];

            // remove_index variable is used to store
            // the next index which we want to delete
            let remove_index = index + first_ludic;
            while (remove_index < ludics.length) {

                // removing the next item
                ludics.splice(remove_index,1);

                // remove_index is updated so that
                // we get the next index for deletion
                remove_index = remove_index + first_ludic - 1;
            }
        }
        return ludics;
}

let n = 25;
document.write(getLudic(n));

// This code is contributed by unknown2108.
</script>
```

**输出:**

```
[1, 2, 3, 5, 7, 11, 13, 17, 23, 25]
```

**参考文献:**
[https://oeis.org/wiki/Ludic_numbers](https://oeis.org/wiki/Ludic_numbers)