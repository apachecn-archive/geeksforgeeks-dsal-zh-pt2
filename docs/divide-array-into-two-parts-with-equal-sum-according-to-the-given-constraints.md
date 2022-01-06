# 根据给定的约束条件

将数组等和分成两部分

> 原文:[https://www . geeksforgeeks . org/根据给定的约束条件将数组分成两个相等的部分/](https://www.geeksforgeeks.org/divide-array-into-two-parts-with-equal-sum-according-to-the-given-constraints/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是选择一个整数 **x** (它可能存在于数组中，也可能不存在于数组中)，从数组中移除它的所有出现，并将剩余的数组分成两个非空的子集，这样:

1.  第一组的元素严格小于 **x** 。
2.  第二组元素严格大于 **x** 。
3.  这两个集合的元素之和相等。

    **Yes**

    **No**

    **示例:**

    > **输入:** arr[] = {1，2，2，5}
    > **输出:**是
    > 选择 x = 3，在移除其所有出现后，数组变成 arr[] = {1，2，2，5}
    > {1，2，2}和{5}是所需的子集。
    > 
    > **输入:** arr[] = {2，1 }
    > T3】输出:否

    **方法:**首先对数组进行排序，对于数组中从 1 到最大值之间的所有数字，应用二分搜索法，并检查从数组中移除所有出现的数字时，其左侧出现的元素之和(小于它)和右侧出现的元素之和(大于它)是否相等。

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation of the approach
    #include <bits/stdc++.h>
    using namespace std;

    // Function that checks if the given
    // conditions are satisfied
    void IfExists(int arr[], int n)
    {
        // To store the prefix sum
        // of the array elements
        int sum[n];

        // Sort the array
        sort(arr, arr + n);

        sum[0] = arr[0];

        // Compute the prefix sum array
        for (int i = 1; i < n; i++)
            sum[i] = sum[i - 1] + arr[i];

        // Maximum element in the array
        int max = arr[n - 1];

        // Variable to check if there exists any number
        bool flag = false;

        for (int i = 1; i <= max; i++) {

            // Stores the index of the largest
            // number present in the array
            // smaller than i
            int findex = 0;

            // Stores the index of the smallest
            // number present in the array
            // greater than i
            int lindex = 0;

            int l = 0;
            int r = n - 1;

            // Find index of smallest number
            // greater than i
            while (l <= r) {
                int m = (l + r) / 2;

                if (arr[m] < i) {
                    findex = m;
                    l = m + 1;
                }
                else
                    r = m - 1;
            }

            l = 1;
            r = n;
            flag = false;

            // Find index of smallest number
            // greater than i
            while (l <= r) {
                int m = (r + l) / 2;

                if (arr[m] > i) {
                    lindex = m;
                    r = m - 1;
                }
                else
                    l = m + 1;
            }

            // If there exists a number
            if (sum[findex] == sum[n - 1] - sum[lindex - 1]) {
                flag = true;
                break;
            }
        }

        // If no such number exists
        // print no
        if (flag)
            cout << "Yes";
        else
            cout << "No";
    }

    // Driver code
    int main()
    {
        int arr[] = { 1, 2, 2, 5 };
        int n = sizeof(arr) / sizeof(int);
        IfExists(arr, n);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of the approach 
    import java.util.*;

    class GFG
    {

    // Function that checks if the given 
    // conditions are satisfied 
    static void IfExists(int arr[], int n) 
    { 
        // To store the prefix sum 
        // of the array elements 
        int sum[] = new int[n]; 

        // Sort the array 
        Arrays.sort(arr); 

        sum[0] = arr[0]; 

        // Compute the prefix sum array 
        for (int i = 1; i < n; i++) 
            sum[i] = sum[i - 1] + arr[i]; 

        // Maximum element in the array 
        int max = arr[n - 1]; 

        // Variable to check if there exists any number 
        boolean flag = false; 

        for (int i = 1; i <= max; i++) 
        { 

            // Stores the index of the largest 
            // number present in the array 
            // smaller than i 
            int findex = 0; 

            // Stores the index of the smallest 
            // number present in the array 
            // greater than i 
            int lindex = 0; 

            int l = 0; 
            int r = n - 1; 

            // Find index of smallest number 
            // greater than i 
            while (l <= r) 
            { 
                int m = (l + r) / 2; 

                if (arr[m] < i) 
                { 
                    findex = m; 
                    l = m + 1; 
                } 
                else
                    r = m - 1; 
            } 

            l = 1; 
            r = n; 
            flag = false; 

            // Find index of smallest number 
            // greater than i 
            while (l <= r) 
            { 
                int m = (r + l) / 2; 

                if (arr[m] > i) 
                { 
                    lindex = m; 
                    r = m - 1; 
                } 
                else
                    l = m + 1; 
            } 

            // If there exists a number 
            if (sum[findex] == sum[n - 1] - sum[lindex - 1]) 
            { 
                flag = true; 
                break; 
            } 
        } 

        // If no such number exists 
        // print no 
        if (flag) 
            System.out.println("Yes"); 
        else
            System.out.println("No"); 
    } 

    // Driver code 
    public static void main(String args[])
    { 
        int arr[] = { 1, 2, 2, 5 }; 
        int n = arr.length; 
        IfExists(arr, n); 
    }
    } 

    // This code is contributed by Arnab Kundu
    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation of the approach 

    # Function that checks if the given 
    # conditions are satisfied 
    def IfExists(arr, n) :

        # To store the prefix sum 
        # of the array elements 
        sum = [0] * n; 

        # Sort the array 
        arr.sort(); 

        sum[0] = arr[0]; 

        # Compute the prefix sum array 
        for i in range(1, n) : 
            sum[i] = sum[i - 1] + arr[i]; 

        # Maximum element in the array 
        max = arr[n - 1]; 

        # Variable to check if there 
        # exists any number 
        flag = False; 

        for i in range(1, max + 1) :

            # Stores the index of the largest 
            # number present in the array 
            # smaller than i 
            findex = 0; 

            # Stores the index of the smallest 
            # number present in the array 
            # greater than i 
            lindex = 0; 

            l = 0; 
            r = n - 1; 

            # Find index of smallest number 
            # greater than i 
            while (l <= r) :
                m = (l + r) // 2; 

                if (arr[m] < i) :
                    findex = m; 
                    l = m + 1; 

                else :
                    r = m - 1; 

            l = 1; 
            r = n; 
            flag = False; 

            # Find index of smallest number 
            # greater than i 
            while (l <= r) : 
                m = (r + l) // 2; 

                if (arr[m] > i) : 
                    lindex = m; 
                    r = m - 1; 

                else :
                    l = m + 1; 

            # If there exists a number 
            if (sum[findex] == sum[n - 1] - 
                               sum[lindex - 1]) : 
                flag = True; 
                break; 

        # If no such number exists 
        # print no 
        if (flag) : 
            print("Yes"); 
        else :
            print("No"); 

    # Driver code 
    if __name__ == "__main__" : 

        arr = [ 1, 2, 2, 5 ]; 

        n = len(arr) ;
        IfExists(arr, n); 

    # This code is contributed by Ryuga
    ```

    ## C#

    ```
    // C# implementation of the approach 
    using System;

    class GFG
    {

    // Function that checks if the given 
    // conditions are satisfied 
    static void IfExists(int[] arr, int n) 
    { 
        // To store the prefix sum 
        // of the array elements 
        int[] sum = new int[n]; 

        // Sort the array 
        Array.Sort(arr); 

        sum[0] = arr[0]; 

        // Compute the prefix sum array 
        for (int i = 1; i < n; i++) 
            sum[i] = sum[i - 1] + arr[i]; 

        // Maximum element in the array 
        int max = arr[n - 1]; 

        // Variable to check if there exists any number 
        bool flag = false; 

        for (int i = 1; i <= max; i++) 
        { 

            // Stores the index of the largest 
            // number present in the array 
            // smaller than i 
            int findex = 0; 

            // Stores the index of the smallest 
            // number present in the array 
            // greater than i 
            int lindex = 0; 

            int l = 0; 
            int r = n - 1; 

            // Find index of smallest number 
            // greater than i 
            while (l <= r) 
            { 
                int m = (l + r) / 2; 

                if (arr[m] < i) 
                { 
                    findex = m; 
                    l = m + 1; 
                } 
                else
                    r = m - 1; 
            } 

            l = 1; 
            r = n; 
            flag = false; 

            // Find index of smallest number 
            // greater than i 
            while (l <= r) 
            { 
                int m = (r + l) / 2; 

                if (arr[m] > i) 
                { 
                    lindex = m; 
                    r = m - 1; 
                } 
                else
                    l = m + 1; 
            } 

            // If there exists a number 
            if (sum[findex] == sum[n - 1] - sum[lindex - 1]) 
            { 
                flag = true; 
                break; 
            } 
        } 

        // If no such number exists 
        // print no 
        if (flag) 
            Console.WriteLine("Yes"); 
        else
            Console.WriteLine("No"); 
    } 

    // Driver code 
    public static void Main()
    { 
        int[] arr = { 1, 2, 2, 5 }; 
        int n = arr.Length; 
        IfExists(arr, n); 
    }
    } 

    // This code is contributed by Code_Mech.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // PHP implementation of the approach

    // Function that checks if the given
    // conditions are satisfied
    function IfExists($arr, $n)
    {
        // To store the prefix $sum
        // of the array elements
        $sum = array_fill(0, $n, 0);

        // Sort the array
        sort($arr);

        $sum[0] = $arr[0];

        // Compute the prefix sum array
        for ($i = 1; $i < $n; $i++)
            $sum[$i] = $sum[$i - 1] + $arr[$i];

        // Maximum element in the array
        $max = $arr[$n - 1];

        // Variable to check if there exists any number
        $flag = false;

        for ($i = 1; $i <= $max; $i++) 
        {

            // Stores the index of the largest
            // number present in the array
            // smaller than i
            $findex = 0;

            // Stores the index of the smallest
            // number present in the array
            // greater than i
            $lindex = 0;

            $l = 0;
            $r = $n - 1;

            // Find index of smallest number
            // greater than i
            while ($l <= $r) 
            {
                $m = ($l + $r) / 2; 
                if ($arr[$m] < $i) 
                {
                    $findex = $m;
                    $l = $m + 1;
                }
                else
                    $r = $m - 1;
            }

            $l = 1;
            $r = $n;
            $flag = false;

            // Find index of smallest number
            // greater than i
            while ($l <= $r)
            {
                $m = ($r + $l) / 2;

                if ($arr[$m] > $i) 
                {
                    $lindex = $m;
                    $r = $m - 1;
                }
                else
                    $l = $m + 1;
            }

            // If there exists a number
            if ($sum[$findex] == $sum[$n - 1] -
                                 $sum[$lindex - 1])
            {
                $flag = true;
                break;
            }
        }

        // If no such number exists
        // print no
        if ($flag == true)
            echo "Yes";
        else
            echo "No";
    }

    // Driver code
    $arr = array(1, 2, 2, 5 );
    $n = sizeof($arr);
    IfExists($arr, $n);

    // This code is contributed by ihritik
    ?>
    ```

    **Output:**

    ```
    Yes

    ```