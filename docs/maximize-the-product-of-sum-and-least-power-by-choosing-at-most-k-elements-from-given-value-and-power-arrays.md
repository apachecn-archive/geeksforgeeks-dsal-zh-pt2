# 从给定值和幂数组中选择最多 K 个元素，最大化和与最小幂的乘积

> 原文:[https://www . geesforgeks . org/通过从给定值和幂数组中选择最多 k 个元素来最大化和最小幂的乘积/](https://www.geeksforgeeks.org/maximize-the-product-of-sum-and-least-power-by-choosing-at-most-k-elements-from-given-value-and-power-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和 **powr[]** 大小为 **N** 和一个整数 **K** 。每个元素**arr【I】**都有各自的力量**pour【I】**。任务是通过从数组中最多选择 K 个**元素来最大化**给定函数的值。该功能定义为:****

> ****f(n)=(arr[I]t0[1]t1]]+arr[I]T2[2]T3]]+arr[I]T4[3]t5]+……-什么 arr[I<sub>n</sub>)* min(pow[I<sub>1</sub>、pow[I<sub>2</sub>、pow[I<sub>3</sub>、……-什么 pow[I〖t14〗n〗t15〗在哪里，arr[I〖t16〗1〗，arr[I〖t18〗2〗t19〗，arr[I〖t20〗3〖t21〗，}-什么 arr[我〖t22〗n〖t23〗〗〗〗〗〗，是选择的要素。****

******示例:******

> ******输入:** arr[] = {11，10，7，6，9}，powr[] = {3，2，4，1，1}，K = 2，N = 5
> **输出:** 54
> **解释:**在索引{0，2}处选择元素所以，f(N) = (11 + 7) * min(3，4) = 18 * 3 = 54，这是最多选择 2 个元素可以达到的最大可能值。****
> 
>  ******输入:** arr[] = {5，12，11，9}，powr[] = {2，1，10，1}，K = 3，N = 4
> **输出:** 110****

******进场:**思路是以元素为最小功率考虑每一个**，为此，[按照功率的降序](https://www.geeksforgeeks.org/sort-c-stl/)对元素进行排序，那么第一个元素会被认为功率最高。任何时候都尽量保持一个最多 **K** 大小的元素列表。该列表最多包含**最大的**个 **K** 元素，不包括当前的**和**元素。如果已经有一个尺寸列表 **K** ，则移除具有最小长度的元素，这样，尺寸变为**K–1**，然后将当前元素包括到列表中，尺寸变为 **K** ，并更新最大尺寸的 **res** 。最后，返回 **res** ，这就是答案。******

*   **[初始化大小为 **N** 的一对向量](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **v[]** ，以存储元素及其能量。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:

    *   将值**幂【I】**和**arr【I】**指定为数组 **v[]的第一个和第二个值。**** 
*   **[按升序排列**v[]**](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)。**
*   **将变量 **res** 和 **sum** 初始化为 **0** 来存储结果和总和。**
*   **[初始化一组对 **s[]**](https://www.geeksforgeeks.org/sets-of-pairs-in-c/) **。****
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N-1，0】**，并执行以下任务:

    *   插入一对 **{v[i]。二、我}** 入集 **s[]。**
    *   加上**v【I】的值。第二个**到变量**的和。**
    *   如果 **s.size()** 大于 **K** ，则执行以下任务:
        *   将变量**初始化为集合 **s[]的第一个元素。****
        *   从变量**和中减去数值 **it.first** 。**
        *   从设置 **s[]中移除变量**。****
    *   **首先将 **res** 的值设置为 **res** 或 **sum*v[i]的最大值。****** 
*   ****执行上述步骤后，打印 **res** 的值作为答案。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the value of the
// function by choosing at most K elements
// from the given array
int maximumValue(int arr[], int powr[],
                 int K, int N)
{

    // Vector to store the power of elements
    // along with the elements in pair
    vector<pair<int, int> > v(N);

    // In a pair, the first position contains
    // the power and the second position
    // contains the element
    for (int i = 0; i < N; i++) {
        v[i].first = powr[i];
        v[i].second = arr[i];
    }

    // Sort the vector according to the
    // power of the elements
    sort(v.begin(), v.end());

    // Variable to store the answer
    int res = 0;

    // Variable to store the sum of
    // elements
    int sum = 0;

    // Create a set of pairs
    set<pair<int, int> > s;

    // Traverse the vector in reverse order
    for (int i = N - 1; i >= 0; i--) {

        // Insert the element along with the
        // index in pair
        s.insert(make_pair(v[i].second, i));
        sum += v[i].second;

        // If size of set exceeds K, then
        // delete the first pair in the set
        // and update the sum by excluding
        // the elements value from it
        if (s.size() > K) {
            auto it = s.begin();
            sum -= it->first;
            s.erase(it);
        }

        // Store the maximum of all sum
        // multiplied by the element's
        // power
        res = max(res, sum * v[i].first);
    }

    // Return res
    return res;
}

// Driver Code
int main()
{
    int arr[] = { 11, 10, 7, 6, 9 };
    int powr[] = { 3, 2, 4, 1, 1 };
    int K = 2;

    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumValue(arr, powr, K, N);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.HashSet;

class GFG {

  static class Pair {
    int first;
    int second;

    Pair(int first, int second) {
      this.first = first;
      this.second = second;
    }
  }

  // Function to maximize the value of the
  // function by choosing at most K elements
  // from the given array
  public static int maximumValue(int arr[], int powr[], int K, int N) {

    // Vector to store the power of elements
    // along with the elements in pair
    ArrayList<Pair> v = new ArrayList<Pair>();

    // In a pair, the first position contains
    // the power and the second position
    // contains the element
    for (int i = 0; i < N; i++) {
      v.add(new Pair(0, 0));
      v.get(i).first = powr[i];
      v.get(i).second = arr[i];
    }

    // Sort the vector according to the
    // power of the elements
    Collections.sort(v, new Comparator<Pair>() {
      @Override
      public int compare(final Pair lhs, Pair rhs) {
        return lhs.first > rhs.first ? 1 : -1;
      };
    });

    // Variable to store the answer
    int res = 0;

    // Variable to store the sum of
    // elements
    int sum = 0;

    // Create a set of pairs
    HashSet<Pair> s = new HashSet<Pair>();

    // Traverse the vector in reverse order
    for (int i = N - 1; i >= 0; i--) {

      // Insert the element along with the
      // index in pair
      s.add(new Pair(v.get(i).second, i));
      sum += v.get(i).second;

      // If size of set exceeds K, then
      // delete the first pair in the set
      // and update the sum by excluding
      // the elements value from it
      if (s.size() > K) {
        Pair it = s.iterator().next();
        sum -= it.first;
        s.remove(it);
      }

      // Store the maximum of all sum
      // multiplied by the element's
      // power
      res = Math.max(res, sum * v.get(i).first);
    }

    // Return res
    return res;
  }

  // Driver Code
  public static void main(String args[]) {
    int arr[] = { 11, 10, 7, 6, 9 };
    int powr[] = { 3, 2, 4, 1, 1 };
    int K = 2;

    int N = arr.length;
    System.out.println(maximumValue(arr, powr, K, N));

  }
}

// This code is contributed by gfgking.**
```

## ****蟒蛇 3****

```
**# Python 3 program for the above approach

# Function to maximize the value of the
# function by choosing at most K elements
# from the given array
def maximumValue(arr, powr, K, N):

    # Vector to store the power of elements
    # along with the elements in pair
    v = [[0 for x in range(2)] for y in range(N)]

    # In a pair, the first position contains
    # the power and the second position
    # contains the element
    for i in range(N):
        v[i][0] = powr[i]
        v[i][1] = arr[i]

    # Sort the vector according to the
    # power of the elements
    v.sort()

    # Variable to store the answer
    res = 0

    # Variable to store the sum of
    # elements
    sum = 0

    # Create a set of pairs
    s = set([])

    # Traverse the vector in reverse order
    for i in range(N - 1, -1, -1):

        # Insert the element along with the
        # index in pair
        s.add((v[i][1], i))
        sum += v[i][1]

        # If size of set exceeds K, then
        # delete the first pair in the set
        # and update the sum by excluding
        # the elements value from it
        if (len(s) > K):

            sum -= list(s)[0][0]
            list(s).remove(list(s)[0])

        # Store the maximum of all sum
        # multiplied by the element's
        # power
        res = max(res, sum * v[i][0])

    # Return res
    return res

# Driver Code
if __name__ == "__main__":

    arr = [11, 10, 7, 6, 9]
    powr = [3, 2, 4, 1, 1]
    K = 2

    N = len(arr)
    print(maximumValue(arr, powr, K, N))

     # This code is contributed by ukasp.**
```

## ****java 描述语言****

```
**<script>
// Javascript program for the above approach

// Function to maximize the value of the
// function by choosing at most K elements
// from the given array
function maximumValue(arr, powr, K, N) {

  // Vector to store the power of elements
  // along with the elements in pair
  let v = new Array(N).fill(0).map(() => []);

  // In a pair, the first position contains
  // the power and the second position
  // contains the element
  for (let i = 0; i < N; i++) {
    v[i][0] = powr[i];
    v[i][1] = arr[i];
  }

  // Sort the vector according to the
  // power of the elements
  v.sort();

  // Variable to store the answer
  let res = 0;

  // Variable to store the sum of
  // elements
  let sum = 0;

  // Create a set of pairs
  let s = new Set();

  // Traverse the vector in reverse order
  for (let i = N - 1; i >= 0; i--) {

    // Insert the element along with the
    // index in pair
    s.add([v[i][1], i]);
    sum += v[i][1];

    // If size of set exceeds K, then
    // delete the first pair in the set
    // and update the sum by excluding
    // the elements value from it
    if (s.size > K) {
      let it = [...s][0];
      sum -= it[0];
      s.delete(it);
    }

    // Store the maximum of all sum
    // multiplied by the element's
    // power
    res = Math.max(res, sum * v[i][0]);
  }

  // Return res
  return res;
}

// Driver Code

let arr = [11, 10, 7, 6, 9];
let powr = [3, 2, 4, 1, 1];
let K = 2;

let N = arr.length;
document.write(maximumValue(arr, powr, K, N))

// This code is contributed by saurabh_jaiswal.
</script>**
```

******Output**

```
54
```**** 

*******时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*****