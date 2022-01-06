# 对于 M 个查询，异或+ 1 等于异或(XOR) 1 的[L，R]范围内的子阵列计数

> 原文:[https://www . geesforgeks . org/范围内子数组计数-l-r-having-xor-1-等于-xor-xor-1-for-m-query/](https://www.geeksforgeeks.org/count-of-subarrays-in-range-l-r-having-xor-1-equal-to-xor-xor-1-for-m-queries/)

给定一个数组，**arr[]****N**正整数， **M** 查询由两个整数组成**【L<sub>I</sub>，R<sub>I</sub>**，其中 **1 ≤ Li ≤ Ri ≤ N** 。对于每个查询，在范围**【l<sub>I</sub>，r<sub>I</sub>**中找到子阵列的数量，其中 **(X+1)=(X⊕1)** 其中 **X** 表示子阵列的 xor。

> **输入:** arr[]= {1，2，9，8，7}，查询[] = {{1，5}，{3，4}}
> **输出:** 6 1
> **解释:**
> 查询 1: L=1，R=5:子阵列[1，3]，[1，4]，[2，2]，[2，5]，[3，5]，[4，4]
> 查询 2: L=3，R=4
> 
> **输入:** arr[] = {1，2，2，4，5}，查询[] = {{2，4}，{3，5}}
> **输出:** 6 3

**天真方法:**对于每个查询，选择给定的范围【L <sub>i</sub> ，R <sub>i</sub> ，对于每个子阵列，检查它是否满足给定的条件。
**时间复杂度:** O(N <sup>3</sup> * M)

**有效方法:**在上述问题中，可以进行以下观察:

*   为了满足给定的条件， **X** 必须是偶数，因为
    *   如果 **X** 是偶数，**(*****x*****⊕1)=(***x***+1)**
    *   如果 **X** 是奇数，**(*****x*****⊕1)=(***x***1)**
*   对于一个子阵列，如果该子阵列中奇数的计数为偶数，则其 xor 将为偶数。
*   如果奇数的计数是偶数，那么子阵列的总和将是偶数。所以，和为偶数的[子阵](https://www.geeksforgeeks.org/find-number-subarrays-even-sum/)就是这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

vector<int> countXorSubarr(
    vector<int> arr,
    vector<vector<int> > queries,
    int n, int m)
{

    // As queries are in 1-based indexing,
    // add one dummy entry in beggining
    // of arr to make it 1-indexed
    arr.insert(arr.begin(), 0);

    // sum[] will contain parity
    // of prefix sum till index i
    // count[] will contain
    // number of 0s in sum[]
    int count[n + 1], sum[n + 1];
    count[0] = sum[0] = 0;

    for (int i = 1; i <= n; i++) {

        // Take the parity of current sum
        sum[i] = (sum[i - 1] + arr[i]) % 2;
        count[i] = count[i - 1];

        // If current parity is even,
        // increase the count
        if (sum[i] % 2 == 0)
            count[i]++;
    }

    // Array to hold the answer of 'm' queries
    vector<int> ans;

    // Iterate through queries and use handshake
    // lemma to count even sum subarrays
    // ( Note that an even sum can
    // be formed by two even or two odd )
    for (vector<int> qu : queries) {
        int L = qu[0], R = qu[1];

        // Find count of even and
        // odd sums in range [L, R]
        int even = count[R] - count[L - 1];
        int odd = (R - L + 1) - even;

        // If prefix sum at L-1 is odd,
        // then we need to swap
        // our counts of odd and even
        if (sum[L - 1] == 1)
            swap(even, odd);

        // Taking no element is also
        // considered an even sum
        // so even will be increased by 1
        // (This is the condition when
        // a prefix of even sum is taken)
        even++;

        // Find number of ways to
        // select two even's or two odd's
        int subCount = (even * (even - 1)) / 2
                       + (odd * (odd - 1)) / 2;

        ans.push_back(subCount);
    }

    return ans;
}

// Driver code
int main()
{
    int n = 5;
    vector<int> arr = { 1, 2, 9, 8, 7 };
    int m = 2;
    vector<vector<int> > queries
        = { { 1, 5 }, { 3, 4 } };

    // Function call and print answer
    vector<int> ans
        = countXorSubarr(arr, queries, n, m);
    for (int x : ans)
        cout << x << " ";
    cout << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;

class GFG
{

    public static ArrayList<Integer> countXorSubarr(int[] arr, int[][] queries, int n, int m) {

        // As queries are in 1-based indexing,
        // add one dummy entry in beggining
        // of arr to make it 1-indexed
        // arr.insert(arr.begin(), 0);
        int[] temp_arr = new int[arr.length + 1];
        temp_arr[0] = 0;
        for (int i = 1; i < temp_arr.length; i++) {
            temp_arr[i] = arr[i - 1];
        }
        arr = temp_arr.clone();

        // sum[] will contain parity
        // of prefix sum till index i
        // count[] will contain
        // number of 0s in sum[]
        int[] count = new int[n + 1];
        int[] sum = new int[n + 1];
        count[0] = sum[0] = 0;

        for (int i = 1; i <= n; i++) {

            // Take the parity of current sum
            sum[i] = (sum[i - 1] + arr[i]) % 2;
            count[i] = count[i - 1];

            // If current parity is even,
            // increase the count
            if (sum[i] % 2 == 0)
                count[i]++;
        }

        // Array to hold the answer of 'm' queries
        ArrayList<Integer> ans = new ArrayList<Integer>();

        // Iterate through queries and use handshake
        // lemma to count even sum subarrays
        // ( Note that an even sum can
        // be formed by two even or two odd )
        for (int[] qu : queries) {
            int L = qu[0], R = qu[1];

            // Find count of even and
            // odd sums in range [L, R]
            int even = count[R] - count[L - 1];
            int odd = (R - L + 1) - even;

            // If prefix sum at L-1 is odd,
            // then we need to swap
            // our counts of odd and even
            if (sum[L - 1] == 1) {
                int temp = even;
                even = odd;
                odd = temp;
            }

            // Taking no element is also
            // considered an even sum
            // so even will be increased by 1
            // (This is the condition when
            // a prefix of even sum is taken)
            even++;

            // Find number of ways to
            // select two even's or two odd's
            int subCount = (even * (even - 1)) / 2 + (odd * (odd - 1)) / 2;

            ans.add(subCount);
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        int[] arr = { 1, 2, 9, 8, 7 };
        int m = 2;
        int[][] queries = { { 1, 5 }, { 3, 4 } };

        // Function call and print answer
        ArrayList<Integer> ans = countXorSubarr(arr, queries, n, m);
        for (int x : ans)
            System.out.print(x + " ");
        System.out.println("");

    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach
import math
def countXorSubarr(arr, queries, n, m):

        # As queries are in 1-based indexing,
        # add one dummy entry in beggining
        # of arr to make it 1-indexed
    arr.insert(0, 0)

    # sum[] will contain parity
    # of prefix sum till index i
    # count[] will contain
    # number of 0s in sum[]
    count = [0 for _ in range(n + 1)]
    sum = [0 for _ in range(n + 1)]

    for i in range(1, n+1):

                # Take the parity of current sum
        sum[i] = (sum[i - 1] + arr[i]) % 2
        count[i] = count[i - 1]

        # If current parity is even,
        # increase the count
        if (sum[i] % 2 == 0):
            count[i] += 1

        # Array to hold the answer of 'm' queries
    ans = []

    # Iterate through queries and use handshake
    # lemma to count even sum subarrays
    # ( Note that an even sum can
    # be formed by two even or two odd )
    for qu in queries:

        L = qu[0]
        R = qu[1]

        # Find count of even and
        # odd sums in range [L, R]
        even = count[R] - count[L - 1]
        odd = (R - L + 1) - even

        # If prefix sum at L-1 is odd,
        # then we need to swap
        # our counts of odd and even
        if (sum[L - 1] == 1):
            temp = even
            even = odd
            odd = temp

            # Taking no element is also
            # considered an even sum
            # so even will be increased by 1
            # (This is the condition when
            # a prefix of even sum is taken)
        even += 1

        # Find number of ways to
        # select two even's or two odd's
        subCount = (even * (even - 1)) // 2 + (odd * (odd - 1)) // 2
        ans.append(subCount)
    return ans

# Driver code
if __name__ == "__main__":

    n = 5
    arr = [1, 2, 9, 8, 7]
    m = 2
    queries = [[1, 5], [3, 4]]

    # Function call and print answer
    ans = countXorSubarr(arr, queries, n, m)
    for x in ans:
        print(x, end=" ")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    public static List<int> countXorSubarr(int[] arr, int[,] queries, int n, int m)
    {

        // As queries are in 1-based indexing,
        // add one dummy entry in beggining
        // of arr to make it 1-indexed
        // arr.insert(arr.begin(), 0);
        int[] temp_arr = new int[arr.Length + 1];
        temp_arr[0] = 0;
        for (int i = 1; i < temp_arr.Length; i++) {
            temp_arr[i] = arr[i - 1];
        }
        arr = temp_arr;

        // sum[] will contain parity
        // of prefix sum till index i
        // []count will contain
        // number of 0s in sum[]
        int[] count = new int[n + 1];
        int[] sum = new int[n + 1];
        count[0] = sum[0] = 0;

        for (int i = 1; i <= n; i++) {

            // Take the parity of current sum
            sum[i] = (sum[i - 1] + arr[i]) % 2;
            count[i] = count[i - 1];

            // If current parity is even,
            // increase the count
            if (sum[i] % 2 == 0)
                count[i]++;
        }

        // Array to hold the answer of 'm' queries
        List<int> ans = new List<int>();

        // Iterate through queries and use handshake
        // lemma to count even sum subarrays
        // ( Note that an even sum can
        // be formed by two even or two odd )

        for(int i = 0; i < queries.GetLength(0); i++)
        {
            int L = queries[i,0], R = queries[i,1];

            // Find count of even and
            // odd sums in range [L, R]
            int even = count[R] - count[L - 1];
            int odd = (R - L + 1) - even;

            // If prefix sum at L-1 is odd,
            // then we need to swap
            // our counts of odd and even
            if (sum[L - 1] == 1) {
                int temp = even;
                even = odd;
                odd = temp;
            }

            // Taking no element is also
            // considered an even sum
            // so even will be increased by 1
            // (This is the condition when
            // a prefix of even sum is taken)
            even++;

            // Find number of ways to
            // select two even's or two odd's
            int subCount = (even * (even - 1)) / 2 + (odd * (odd - 1)) / 2;

            ans.Add(subCount);

        }
        return ans;
    }
      public static int[] GetRow(int[,] matrix, int row)
      {
        var rowLength = matrix.GetLength(1);
        var rowVector = new int[rowLength];

        for (var i = 0; i < rowLength; i++)
          rowVector[i] = matrix[row, i];

        return rowVector;
      }

    // Driver code
    public static void Main(String []args)
    {
        int n = 5;
        int[] arr = { 1, 2, 9, 8, 7 };
        int m = 2;
        int[,] queries = { { 1, 5 }, { 3, 4 } };

        // Function call and print answer
        List<int> ans = countXorSubarr(arr, queries, n, m);
        foreach (int x in ans)
            Console.Write(x + " ");
        Console.WriteLine("");

    }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach
       function countXorSubarr(arr, queries, n, m)
       {

           // sum[] will contain parity
           // of prefix sum till index i
           // count[] will contain
           // number of 0s in sum[]
           let count = new Array(n + 1), sum = new Array(n + 1);
           count[0] = sum[0] = 0;

           for (let i = 1; i <= n; i++) {

               // Take the parity of current sum
               sum[i] = (sum[i - 1] + arr[i - 1]) % 2;
               count[i] = count[i - 1];

               // If current parity is even,
               // increase the count
               if (sum[i] % 2 == 0)
                   count[i]++;
           }

           // Array to hold the answer of 'm' queries
           let ans = [];

           // Iterate through queries and use handshake
           // lemma to count even sum subarrays
           // ( Note that an even sum can
           // be formed by two even or two odd )
           for (let qu of queries) {
               let L = qu[0], R = qu[1];

               // Find count of even and
               // odd sums in range [L, R]
               let even = count[R] - count[L - 1];
               let odd = (R - L + 1) - even;

               // If prefix sum at L-1 is odd,
               // then we need to swap
               // our counts of odd and even
               if (sum[L - 1] == 1) {
                   temp = even
                   even = odd
                   odd = temp
               }

               // Taking no element is also
               // considered an even sum
               // so even will be increased by 1
               // (This is the condition when
               // a prefix of even sum is taken)
               even++;

               // Find number of ways to
               // select two even's or two odd's
               let subCount = (even * (even - 1)) / 2
                   + (odd * (odd - 1)) / 2;

               ans.push(subCount);
           }

           return ans;
       }

       // Driver code
       let n = 5;
       let arr = [1, 2, 9, 8, 7];
       let m = 2;
       let queries
           = [[1, 5], [3, 4]];

       // Function call and print answer
       let ans
           = countXorSubarr(arr, queries, n, m);
       for (let x of ans)
           document.write(x + " ");

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
6 1 
```

**时间复杂度:**O(N+M)
T3】辅助空间: O(N+M)