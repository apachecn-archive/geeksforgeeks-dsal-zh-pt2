# 对给定三个数出现次数相等的子阵列进行计数

> 原文:[https://www . geeksforgeeks . org/count-给定三个数出现次数相等的子数组/](https://www.geeksforgeeks.org/count-subarrays-with-equal-count-of-occurrences-of-given-three-numbers/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和三个整数 **X，Y，Z** ，任务是从 **X，Y** 和 **Z** 出现次数相等的数组中找到[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的个数。

**示例:**

> **输入:** arr[] = {3，6，7，8，3，6，7}，X = 3，Y = 6，Z = 7
> **输出:** 8
> **解释说明:**有 8 个这样的子阵列，即{3，6，7}、{6，7，8，3}，{7，8，3，6}、{8}、{3，6，7，8}、{8，3，6，7，8}、{8，3，6，7，7}、{ 8，7}，{ 8，7，{3，7}
> 
> **输入:** arr[] = {23，45，76，45，76，87，23}，X = 23，Y = 45，Z = 76
> **输出:** 4
> **说明:**这样的子阵有 3 个，即{23，45，76}、{45，76，87，23}、{87}、{23，45，76，45，76，88 }

**方法:**按照以下步骤解决问题:

1.  初始化三个变量，比如 **fNum_count = 0，sNum_count = 0，tNum_count = 0** 和 **mini** 。
2.  初始化一张[地图，int >，int >](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) 。
3.  **{0，0，0}** 递增频率一次。
4.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果找到任何给定的数字，则**从所有数字中增加**对应的计数和**减少三个**中的最小值。
5.  遍历后，增加这三个变量的值集合的频率。
6.  现在初始化一个变量，说 **final_ans。**
7.  [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)，将每个频率的 **v*(v-1) / 2** 添加到 **final_ans** 中。
8.  打印 **final_ans** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

// Function to count subarrays
void countSubarrays(int arr[], int N,
                    int X, int Y, int Z)
{

    map<pair<pair<int, int>, int>, int> m;
    m[{ { 0, 0 }, 0 }]++;

    int fNum_count = 0, sNum_count = 0,
        tNum_count = 0;
    int mini;

    // Traverse the array
    for (int i = 0; i < N; ++i) {

        // Check is arr[i] is equal to X
        if (arr[i] == X) {

            // Increment fNum_count
            fNum_count++;

            mini = min(min(fNum_count,
                           sNum_count),
                       tNum_count);
            fNum_count -= mini;
            sNum_count -= mini;
            tNum_count -= mini;
        }

        // Check is arr[i] is equal to Y
        else if (arr[i] == Y) {

            // Increment the count of sNum_count
            sNum_count++;

            mini = min(min(fNum_count,
                           sNum_count),
                       tNum_count);
            fNum_count -= mini;
            sNum_count -= mini;
            tNum_count -= mini;
        }

        // Check is arr[i] is equal to Z
        else if (arr[i] == Z) {

            // Increment the count of
            // tNum_count
            tNum_count++;

            mini = min(min(fNum_count,
                           sNum_count),
                       tNum_count);
            fNum_count -= mini;
            sNum_count -= mini;
            tNum_count -= mini;
        }
        m[{ { fNum_count, sNum_count },
            tNum_count }]++;
    }

    ll final_ans = 0;
    map<pair<pair<int, int>, int>,
        int>::iterator it;

    // Iterate over the map
    for (it = m.begin(); it != m.end();
         ++it) {
        ll val = it->second;
        final_ans += (val * (val - 1)) / 2;
    }

    // Print the  answer
    cout << final_ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 3, 6, 7, 8, 3, 6, 7 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of X, Y & Z
    int X = 3, Y = 6, Z = 7;

    // Function Call
    countSubarrays(arr, N, X, Y, Z);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count subarrays
def countSubarrays(arr, N, X, Y, Z):
    m = {}
    m[(  ( 0, 0 ), 0 )] = 1
    fNum_count, sNum_count = 0, 0
    tNum_count = 0
    mini = 0

    # Traverse the array
    for i in range(N):

        # Check is arr[i] is equal to X
        if (arr[i] == X):

            # Increment fNum_count
            fNum_count += 1

            mini = min(min(fNum_count,sNum_count),tNum_count)
            fNum_count -= mini
            sNum_count -= mini
            tNum_count -= mini

        # Check is arr[i] is equal to Y
        elif (arr[i] == Y):

            # Increment the count of sNum_count
            sNum_count+=1

            mini = min(min(fNum_count,sNum_count), tNum_count)

            fNum_count -= mini
            sNum_count -= mini
            tNum_count -= mini

        # Check is arr[i] is equal to Z
        elif (arr[i] == Z):

            # Increment the count of
            # tNum_count
            tNum_count +=1

            mini = min(min(fNum_count, sNum_count), tNum_count)

            fNum_count -= mini
            sNum_count -= mini
            tNum_count -= mini

        m[(( fNum_count, sNum_count ),tNum_count )] = m.get((( fNum_count, sNum_count ),tNum_count ),0)+1

    final_ans = 0

    # Iterate over the map
    for it in m:
        val = m[it]
        final_ans += (val * (val - 1)) // 2

    # Print the  answer
    print (final_ans)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [3, 6, 7, 8, 3, 6, 7]

    # Size of the array
    N = len(arr)

    # Given value of X, Y & Z
    X, Y, Z = 3, 6, 7

    # Function Call
    countSubarrays(arr, N, X, Y, Z)

    # This code is contributed by mohit kumar 29.
```

**Output:** 

```
8
```

***时间复杂度:** O(N * LogN)*
***辅助空间:** O(N)*