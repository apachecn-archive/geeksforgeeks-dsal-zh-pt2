# 最小化阵列分区，使得一个元素在每个分区中重复一次

> 原文:[https://www . geesforgeks . org/minimum-array-partitions-这样一个元素在每个分区中重复一次-Atmos/](https://www.geeksforgeeks.org/minimize-array-partitions-such-that-an-element-is-repeated-atmost-once-in-each-partition/)

给定一个由正整数组成的数组 **arr[]** 。任务是**最小化**如果来自**arr【】**的每个元素可以是一个组中**的一部分，并且一个数字只能重复一次，则形成的连续组。**

**示例:**

> **输入:** arr[] = {1，2，1，1，1，1，2，3}
> **输出:** { {1，2，1}，{1，1，2，3} }
> **解释:**以下是在给定条件下形成的组。
> 在 1 2 1 中，1 重复 1 次。
> 在 1 1 中，1 重复 1 次。
> 在 1 1 2 3 中，1 重复 1 次。
> 因此，总共形成了三个组，这是最小可能的。
> 
> **输入:** arr[] = {1，1 }
> T3】输出: { {1，1} }

**方法:**这个问题可以用[hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)解决。按照以下步骤解决给定的问题。

*   取一个变量，比如说 **count = 0** 用于存储形成的组的数量，一个 **2D** 向量用于存储组。
*   遍历数组**arr【】**，开始将数组元素的频率存储在**图**中，并将当前元素存储在**向量**中。
*   每当任一元素的频率变为 **2** 时，取一个标志变量，跟踪一个之前遇到过频率为 2 的数字，然后向前移动。使用标志变量断开任何组，增加计数变量，并在 **2D** 矢量中推**矢量**，清除整个临时矢量和**映射**。
*   现在打印**2D**T2 矢量作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum groups
// formed with given conditions
void findMinimumGroups(int a[], int n)
{
    map<int, int> m;

    // 2D vector to stor groups
    vector<vector<int> > v;
    int c = 0;

    vector<int> v1;

    bool to = 0;

    for (int i = 0; i < n; i++) {
        v1.push_back(a[i]);

        // Store frequency
        m[a[i]]++;

        // Counting number of groups
        if (m[a[i]] >= 2) {

            if (to or m[a[i]] == 3) {
                c++;

                // If elelemnt found again
                // push in 2d vector
                m.clear();
                v1.pop_back();
                v.push_back(v1);
                v1.clear();
                to = 0;
                i--;
            }
            else
                to = 1;
        }

        else if (i == n - 1) {
            c++;
            v.push_back(v1);
        }
    }

    for (int i = 0; i < v.size(); i++) {

        for (int j = 0; j < v[i].size(); j++) {
            cout << v[i][j] << " ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 1, 1, 1, 1, 1, 2, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findMinimumGroups(arr, N);
}
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find minimum groups
      // formed with given conditions
      function findMinimumGroups(a, n) {
          let m = new Map();

          // 2D vector to store groups
          let v = [];
          let c = 0;

          let v1 = [];

          let to = 0;

          for (let i = 0; i < n; i++) {
              v1.push(a[i]);

              // Store frequency
              if (m.has(a[i])) {
                  m.set(a[i], m.get(a[i]) + 1)
              }
              else {
                  m.set(a[i], 1)
              }

              // Counting number of groups
              if (m.get(a[i]) >= 2) {

                  if (to || m.get(a[i]) == 3) {
                      c++;

                      // If elelemnt found again
                      // push in 2d vector
                      m.clear();
                      v1.pop();
                      v.push(v1);
                      v1 = [];
                      to = 0;
                      i--;
                  }
                  else
                      to = 1;
              }

              else if (i == n - 1) {
                  c++;
                  v.push(v1);
              }
          }

          for (let i = 0; i < v.length; i++) {

              for (let j = 0; j < v[i].length; j++) {
                  document.write(v[i][j] + " ");
              }
              document.write('<br>')
          }
      }

      // Driver Code
      let arr = [1, 2, 1, 1, 1, 1, 1, 2, 3];
      let N = arr.length;

      // Function Call
      findMinimumGroups(arr, N);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
1 2 1 
1 1 
1 1 2 3 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)