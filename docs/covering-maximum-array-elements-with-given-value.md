# 用给定值覆盖最大数组元素

> 原文:[https://www . geesforgeks . org/covering-最大值数组元素-带给定值/](https://www.geeksforgeeks.org/covering-maximum-array-elements-with-given-value/)

给定糖果总数“X”、学生人数“N”和数组“arr”，数组“arr”保存必须给学生的糖果的确切数量的值，以使学生快乐，其中 arr[i]是使学生“I”快乐的糖果的确切数量。任务是以最大限度让学生开心的方式分发糖果。
**例:**

```
Input : X = 70, arr = {20, 30, 10}
Output: 2
One optimal way of distribution is (20, 40, 10)
So, the number of happy students are 2.

Input: X = 10, arr = {20, 30, 10}
Output: 1
One optimal way of distribution is (0, 0, 10)
Only 1 student can be made happy in this case
```

**方法:**我们可以通过开始给那些喜欢吃较少糖果的学生糖果来最大化快乐学生的数量。
所以我们根据糖果对学生名单进行升序排序。然后，我们将简单地遍历数组并取学生，直到总和小于或等于糖果总数。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
# include<bits/stdc++.h>
using namespace std;

// Function to find value for
// covering maximum array elements
int maxArrayCover(vector<int> a, int n, int x){

    // sort the students in
    // ascending based on
    // the candies
    sort(a.begin(), a.end());

    // To store the number
    // of happy students
    int cc = 0;

    // To store the running sum
    int s = 0;
    for (int i = 0; i < n; i++){
        s += a[i];

        // If the current student
        // can't be made happy
        if(s > x){
           break;
        }

        // increment the count
        // if we can make the
        // ith student happy
        cc += 1;
    }

    // If the sum = x
    // then answer is n
    if(accumulate(a.begin(), a.end(), 0) == x){
        return n;
    }
    else{
        // If the count is
        // equal to n then
        // the answer is n-1
        if(cc == n){
            return n-1;
        }
        else{
            return cc;
        }
    }
}

// Driver function
int main(){

    int n = 3;
    int x = 70;
    vector<int> a = {10, 20, 30};

    printf("%d\n",maxArrayCover(a, n, x));

    return 0;
}
// This code is contributed
// by Harshit Saini
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

class GFG{

    // Function to find value for
    // covering maximum array elements
    public static int maxArrayCover(int[] a, int n, int x){

        // sort the students in
        // ascending based on
        // the candies
        Arrays.sort(a);

        // To store the number
        // of happy students
        int cc = 0;

        // To store the running sum
        int s = 0;
        for (int i = 0; i < n; i++){
            s += a[i];

            // If the current student
            // can't be made happy
            if(s > x){
               break;
            }

            // increment the count
            // if we can make the
            // ith student happy
            cc += 1;
        }

        // If the sum = x
        // then answer is n
        if(Arrays.stream(a).sum() == x){
            return n;
        }
        else{
            // If the count is
            // equal to n then
            // the answer is n-1
            if(cc == n){
                return n-1;
            }
            else{
                return cc;
            }
        }
    }

    // Driver function
    public static void main(String []args){

        int n   = 3;
        int x   = 70;
        int[] a = new int[]{10, 20, 30};

        System.out.println(maxArrayCover(a, n, x));

        System.exit(0);
    }
}

// This code is contributed
// by Harshit Saini
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to find value for
# covering maximum array elements
def maxArrayCover(a, n, x):

    # sort the students in
    # ascending based on
    # the candies
    a.sort()

    # To store the number
    # of happy students
    cc = 0

    # To store the running sum
    s = 0
    for i in range(n):
         s+= a[i]

         # If the current student
         # can't be made happy
         if(s > x):
             break

         # increment the count
         # if we can make the
         # ith student happy
         cc += 1

    # If the sum = x
    # then answer is n
    if(sum(a) == x):
         return n
    else:
         # If the count is
         # equal to n then
         # the answer is n-1
         if(cc == n):
            return n-1
         else:
            return cc

# Driver function
if __name__ == '__main__':

    n, x = 3, 70
    a    = [10, 20, 30]   

    print(maxArrayCover(a, n, x))
```

## C#

```
// C# implementation of the approach

using System;
using System.Linq;

class GFG{

    // Function to find value for
    // covering maximum array elements
    static int maxArrayCover(int[] a, int n, int x){

        // sort the students in
        // ascending based on
        // the candies
        Array.Sort(a);

        // To store the number
        // of happy students
        int cc = 0;

        // To store the running sum
        int s = 0;
        for (int i = 0; i < n; i++){
            s += a[i];

            // If the current student
            // can't be made happy
            if(s > x){
               break;
            }

            // increment the count
            // if we can make the
            // ith student happy
            cc += 1;
        }

        // If the sum = x
        // then answer is n
        if(a.Sum() == x){
            return n;
        }
        else{
            // If the count is
            // equal to n then
            // the answer is n-1
            if(cc == n){
                return n-1;
            }
            else{
                return cc;
            }
        }
    }

    // Driver function
    public static void Main(){

        int n   = 3;
        int x   = 70;
        int[] a = new int[]{10, 20, 30};

        Console.WriteLine(maxArrayCover(a, n, x));
    }
}

// This code is contributed
// by Harshit Saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find value for
// covering maximum array elements
function maxArrayCover($a, $n, $x){

    // sort the students in
    // ascending based on
    // the candies
    sort($a);

    // To store the number
    // of happy students
    $cc = 0;

    // To store the running sum
    $s = 0;
    for ($i = 0; $i < $n; $i++){
        $s += $a[$i];

        // If the current student
        // can't be made happy
        if($s > $x){
           break;
        }

        // increment the count
        // if we can make the
        // ith student happy
        $cc += 1;
    }

    // If the sum = x
    // then answer is n
    if(array_sum($a) == $x){
        return $n;
    }
    else{
        // If the count is
        // equal to n then
        // the answer is n-1
        if($cc == $n){
            return $n-1;
        }
        else{
            return $cc;
        }
    }
}

$n = 3;
$x = 70;
$a = array(10, 20, 30);

echo maxArrayCover($a, $n, $x);

// This code is contributed
// by Harshit Saini
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to find value for
    // covering maximum array elements
    function maxArrayCover(a, n, x){

        // sort the students in
        // ascending based on
        // the candies
        a.sort();

        // To store the number
        // of happy students
        let cc = 0;

        // To store the running sum
        let s = 0;
        for (let i = 0; i < n; i++){
            s += a[i];

            // If the current student
            // can't be made happy
            if(s > x){
               break;
            }

            // increment the count
            // if we can make the
            // ith student happy
            cc += 1;
        }
         var sum = a.reduce(function(a, b){
        return a + b;
        }, 0);

        // If the sum = x
        // then answer is n
        if(sum == x){
            return n;
        }
        else{
            // If the count is
            // equal to n then
            // the answer is n-1
            if(cc == n){
                return n-1;
            }
            else{
                return cc;
            }
        }
    }

// driver code

        let n   = 3;
        let x   = 70;
        let a = [ 10, 20, 30 ];

        document.write(maxArrayCover(a, n, x));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N * log(N))
T3】空间复杂度: O(N)