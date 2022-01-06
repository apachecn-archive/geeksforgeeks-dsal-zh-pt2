# 通过避免一组给定字符串来获得给定数值字符串的最小循环旋转次数

> 原文:[https://www . geeksforgeeks . org/通过避免给定字符串集来获得给定数字字符串的最小循环旋转数/](https://www.geeksforgeeks.org/minimum-circular-rotations-to-obtain-a-given-numeric-string-by-avoiding-a-set-of-given-strings/)

给定长度为 **N** 的数字字符串**目标**和一组长度为的数字字符串**阻塞**，每个长度为 **N** ，任务是通过避免在任何步骤出现在**阻塞**中的任何字符串，找到将仅由 **0** 组成的初始字符串转换为**目标**所需的最小圆周旋转次数。如果不可能，打印-1。
**注:**单次旋转包括以 **1** 单位增加或减少特定指数的值。由于旋转是圆形的，0 可以转换为 9，9 可以转换为 0。
**例:**

> **输入:**target =“7531”，blocked = {“1543”、“7434”、“7300”、“7321”、“2427”}
> **输出:** 12
> **解释:**“0000”->“9000”->“8000”->“7000”->“7100”->“7200”->

**进场:**为了解决这个问题，我们采用以下 [BFS](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/) 进场:

*   创建一个长度为 **N** 的字符串**开始**，仅由 0 组成。将其推入队列。创建队列是为了通过增加或减少一个字符来存储下一个可能的有效组合。
*   创建一个无序集**避免**，并在其中添加所有**阻塞的**字符串。
*   如果**避开**出现**启动**或**目标**，则无法达到要求的目标。
*   从队列中弹出**开始**，遍历**开始**的所有字符。以保持不变的单位增减每个字符，并检查字符串是否出现在**中，避免出现**。如果不是，新组合不等于目标，将其推到队列中插入**避免**以防止以后重复相同的组合。
*   一旦遍历了 **start** 的整个长度，对下一级重复上述步骤，这是从 start 获得的有效字符串，并且当前存在于队列中。
*   继续重复以上步骤，直到达到目标或没有其他组合，队列变空。
*   在任何时刻，如果形成的字符串等于目标，返回**计数**的值，该值记录 BFS 遍历的层数。count 的值是所需的最小循环次数。
*   如果无法获得进一步的状态，队列为空，则打印*“不可能”*。

以下是上述逻辑的实现:

## C++

```
// C++ Program to count the minimum
// number of circular rotations required
// to obtain a given numeric strings
// avoiding a set of blocked strings

#include <bits/stdc++.h>
using namespace std;

int minCircularRotations(
    string target,
    vector<string>& blocked,
    int N)
{
    string start = "";
    for (int i = 0; i < N; i++) {
        start += '0';
    }

    unordered_set<string> avoid;

    for (int i = 0; i < blocked.size(); i++)
        avoid.insert(blocked[i]);

    // If the starting string needs
    // to be avoided
    if (avoid.find(start) != avoid.end())
        return -1;

    // If the final string needs
    // to be avoided
    if (avoid.find(target) != avoid.end())
        return -1;

    queue<string> qu;
    qu.push(start);

    // Variable to store count of rotations
    int count = 0;

    // BFS Approach
    while (!qu.empty()) {

        count++;

        // Store the current size
        // of the queue
        int size = qu.size();

        for (int j = 0; j < size; j++) {

            string st = qu.front();
            qu.pop();

            // Traverse the string
            for (int i = 0; i < N; i++) {

                char ch = st[i];

                // Increase the
                // current character
                st[i]++;

                // Circular rotation
                if (st[i] > '9')
                    st[i] = '0';

                // If target is reached
                if (st == target)
                    return count;

                // If the string formed
                // is not one to be avoided
                if (avoid.find(st)
                    == avoid.end())
                    qu.push(st);

                // Add it to the list of
                // strings to be avoided
                // to prevent visiting
                // already visited states
                avoid.insert(st);

                // Decrease the current
                // value by 1 and repeat
                // the similar checkings
                st[i] = ch - 1;

                if (st[i] < '0')
                    st[i] = '9';
                if (st == target)
                    return count;
                if (avoid.find(st)
                    == avoid.end())
                    qu.push(st);
                avoid.insert(st);

                // Restore the original
                // character
                st[i] = ch;
            }
        }
    }

    return -1;
}

// Driver code
int main()
{
    int N = 4;
    string target = "7531";
    vector<string> blocked
        = { "1543",
            "7434",
            "7300",
            "7321",
            "2427" };

    cout << minCircularRotations(
                target,
                blocked, N)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count the minimum
// number of circular rotations required
// to obtain a given numeric Strings
// avoiding a set of blocked Strings
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Queue;

class GFG
{
  static int minCircularRotations(String target,
                                  ArrayList<String> blocked,
                                  int N)
  {
    String start = "";
    for (int i = 0; i < N; i++)
    {
      start += '0';
    }

    HashSet<String> avoid = new HashSet<>();
    for (int i = 0; i < blocked.size(); i++)
      avoid.add(blocked.get(i));

    // If the starting String needs // to be avoided
    if (avoid.contains(start))
      return -1;

    // If the final String needs // to be avoided
    if (avoid.contains(target))
      return -1;
    Queue<String> qu = new LinkedList<>();
    qu.add(start);

    // Variable to store count of rotations
    int count = 0;

    // BFS Approach
    while (!qu.isEmpty())
    {
      count++;

      // Store the current size // of the queue
      int size = qu.size();
      for (int j = 0; j < size; j++)
      {
        StringBuilder st = new StringBuilder(qu.poll());

        // Traverse the String
        for (int i = 0; i < N; i++)
        {
          char ch = st.charAt(i);

          // Increase the // current character
          st.setCharAt(i, (char) (st.charAt(i) + 1));

          // Circular rotation
          if (st.charAt(i) > '9')
            st.setCharAt(i, '0');

          // If target is reached
          if (st.toString().equals(target))
            return count;

          // If the String formed
          // is not one to be avoided
          if (!avoid.contains(st.toString()))
            qu.add(st.toString());

          // Add it to the list of
          // Strings to be avoided
          // to prevent visiting
          // already visited states
          avoid.add(st.toString());

          // Decrease the current
          // value by 1 and repeat
          // the similar checkings
          st.setCharAt(i, (char) (ch - 1));
          if (st.charAt(i) < '0')
            st.setCharAt(i, '9');
          if (st.toString().equals(target))
            return count;
          if (!avoid.contains(st.toString()))
            qu.add(st.toString());
          avoid.add(st.toString());

          // Restore the original
          // character
          st.setCharAt(i, ch);
        }
      }
    }
    return -1;
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 4;
    String target = "7531";
    ArrayList<String> blocked =
      new ArrayList<>(Arrays.asList("1543",
                                    "7434",
                                    "7300",
                                    "7321",
                                    "2427"));
    System.out.println(minCircularRotations(target, blocked, N));
  }
}

// This code is contributed by sanjeev2552
```

**Output:** 

```
12
```