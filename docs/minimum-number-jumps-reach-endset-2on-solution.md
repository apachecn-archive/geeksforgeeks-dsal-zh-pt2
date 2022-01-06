# 到达终点的最小跳跃次数|集合 2 (O(n)解)

> 原文:[https://www . geeksforgeeks . org/minimum-number-jumps-reach-endset-2on-solution/](https://www.geeksforgeeks.org/minimum-number-jumps-reach-endset-2on-solution/)

给定一个整数数组，其中每个元素表示从该元素向前可以进行的最大步数。编写一个函数，返回到达数组末尾的最小跳转次数(从第一个元素开始)。如果一个元素是 0，那么我们就不能穿过那个元素。如果我们不能到达终点，返回-1。
**例:**

```
Input:  arr[] = {1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9}
Output: 3 (1-> 3 -> 8 -> 9)
Explanation: Jump from 1st element to 
2nd element as there is only 1 step, 
now there are three options 5, 8 or 9\. 
If 8 or 9 is chosen then the end node 9 
can be reached. So 3 jumps are made.

Input:  arr[] = {1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1}
Output: 10
Explanation: In every step a jump is 
needed so the count of jumps is 10.
```

在这篇文章中，将讨论它的 O(n)解。

在 [Set -1](https://www.geeksforgeeks.org/minimum-number-of-jumps-to-reach-end-of-a-given-array/#comment-3321908697) 中，讨论了 O(n <sup>2</sup> )解。
**实施:**
要使用的变量:

1.  **<u>【maxReach】</u>**变量 maxReach 始终存储数组中的最大可达索引。
2.  <u>跳跃存储到达最大可达位置所需的跳跃次数。这也表明我们正在阵列中进行的**电流跳跃。**</u>
3.  <u>**<u>步</u>** 变量步存储了我们在当前跳转中仍然可以走的步数**(并且用索引 0 处的值初始化，即初始步数)**</u>

<u>给定数组 arr = 1，3，5，8，9，2，6，7，6，8，9</u>

*   <u>**MaxReach**= arr[0]；// arr[0] = 1，所以我们目前能达到的最大指标是 1。
    **步**= arr[0]；// arr[0] = 1，我们还能走的步数也是 1。
    **跳**= 1；//我们目前正在进行第一次跳跃。</u>
*   <u>现在，从索引 1 开始迭代，上面的值更新如下:

    1.  首先，我们测试是否已经到达数组的末尾，在这种情况下，我们只需要返回跳转变量。</u> 

```
if (i == arr.length - 1)
    return jump;
```

<u>2.接下来我们更新 maxReach。这等于 maxReach 和 i+arr[i]的最大值(我们从当前位置可以走的步数)。</u>

```
maxReach = Math.max(maxReach, i+arr[i]);
```

<u>3.我们使用了一个步长来获取当前索引，因此必须减少步长。</u>

```
step--;
```

<u>4.如果没有剩余的步骤(即步骤=0)，那么我们一定使用了跳转。因此增加跳跃。因为我们知道以某种方式达到最大到达是可能的，所以我们再次将步骤初始化为从位置 I 达到最大到达的步骤数。但是在重新初始化步骤之前，我们还会检查一个步骤是变为零还是变负。在这种情况下，不可能达到更远。</u>

```
if (step == 0) {
    jump++;
    if(i>=maxReach)
       return -1;
    step = maxReach - i;
} 
```

## <u>C++</u>

```
// C++ program to count Minimum number
// of jumps to reach end
#include <bits/stdc++.h>
using namespace std;

int max(int x, int y)
{
    return (x > y) ? x : y;
}

// Returns minimum number of jumps
// to reach arr[n-1] from arr[0]
int minJumps(int arr[], int n)
{

    // The number of jumps needed to
    // reach the starting index is 0
    if (n <= 1)
        return 0;

    // Return -1 if not possible to jump
    if (arr[0] == 0)
        return -1;

    // initialization
    // stores all time the maximal
    // reachable index in the array.
    int maxReach = arr[0];

    // stores the number of steps
    // we can still take
    int step = arr[0];

    // stores the number of jumps
    // necessary to reach that maximal
    // reachable position.
    int jump = 1;

    // Start traversing array
    int i = 1;
    for (i = 1; i < n; i++) {
        // Check if we have reached the end of the array
        if (i == n - 1)
            return jump;

        // updating maxReach
        maxReach = max(maxReach, i + arr[i]);

        // we use a step to get to the current index
        step--;

        // If no further steps left
        if (step == 0) {
            // we must have used a jump
            jump++;

            // Check if the current index/position or lesser index
            // is the maximum reach point from the previous indexes
            if (i >= maxReach)
                return -1;

            // re-initialize the steps to the amount
            // of steps to reach maxReach from position i.
            step = maxReach - i;
        }
    }

    return -1;
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };
    int size = sizeof(arr) / sizeof(int);

    // Calling the minJumps function
    cout << ("Minimum number of jumps to reach end is %d ",
             minJumps(arr, size));
    return 0;
}
// This code is contributed by
// Shashank_Sharma
```

## <u>C</u>

```
// C program to count Minimum number
// of jumps to reach end
#include <stdio.h>

int max(int x, int y) { return (x > y) ? x : y; }

// Returns minimum number of jumps
// to reach arr[n-1] from arr[0]
int minJumps(int arr[], int n)
{

    // The number of jumps needed to
    // reach the starting index is 0
    if (n <= 1)
        return 0;

    // Return -1 if not possible to jump
    if (arr[0] == 0)
        return -1;

    // initialization
    // stores all time the maximal
    // reachable index in the array.
    int maxReach = arr[0];

    // stores the number of steps
    // we can still take
    int step = arr[0];

    // stores the number of jumps
    // necessary to reach that maximal
    // reachable position.
    int jump = 1;

    // Start traversing array
    int i = 1;
    for (i = 1; i < n; i++) {
        // Check if we have reached the end of the array
        if (i == n - 1)
            return jump;

        // updating maxReach
        maxReach = max(maxReach, i + arr[i]);

        // we use a step to get to the current index
        step--;

        // If no further steps left
        if (step == 0) {
            // we must have used a jump
            jump++;

            // Check if the current index/position or lesser index
            // is the maximum reach point from the previous indexes
            if (i >= maxReach)
                return -1;

            // re-initialize the steps to the amount
            // of steps to reach maxReach from position i.
            step = maxReach - i;
        }
    }
    return -1;
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };
    int size = sizeof(arr) / sizeof(int);

    // Calling the minJumps function
    printf(
        "Minimum number of jumps to reach end is %d ",
        minJumps(arr, size));
    return 0;
}
// This code is contributed by Abhishek Kumar Singh
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to count Minimum number
// of jumps to reach end

class Test {
    static int minJumps(int arr[])
    {
        if (arr.length <= 1)
            return 0;

        // Return -1 if not possible to jump
        if (arr[0] == 0)
            return -1;

        // initialization
        int maxReach = arr[0];
        int step = arr[0];
        int jump = 1;

        // Start traversing array
        for (int i = 1; i < arr.length; i++) {
            // Check if we have reached
// the end of the array
            if (i == arr.length - 1)
                return jump;

            // updating maxReach
            maxReach = Math.max(maxReach, i + arr[i]);

            // we use a step to get to the current index
            step--;

            // If no further steps left
            if (step == 0) {
                // we must have used a jump
                jump++;

                // Check if the current
// index/position or lesser index
                // is the maximum reach point
// from the previous indexes
                if (i >= maxReach)
                    return -1;

                // re-initialize the steps to the amount
                // of steps to reach maxReach from position i.
                step = maxReach - i;
            }
        }

        return -1;
    }

    // Driver method to test the above function
    public static void main(String[] args)
    {
        int arr[] = new int[] { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };

        // calling minJumps method
        System.out.println(minJumps(arr));
    }
}
```

## <u>计算机编程语言</u>

```
# python program to count Minimum number
# of jumps to reach end

# Returns minimum number of jumps to reach arr[n-1] from arr[0]
def minJumps(arr, n):
  # The number of jumps needed to reach the starting index is 0
  if (n <= 1):
    return 0

  # Return -1 if not possible to jump
  if (arr[0] == 0):
    return -1

  # initialization
  # stores all time the maximal reachable index in the array
  maxReach = arr[0] 
  # stores the amount of steps we can still take
  step = arr[0]
  # stores the amount of jumps necessary to reach that maximal reachable position
  jump = 1

  # Start traversing array

  for i in range(1, n):
    # Check if we have reached the end of the array
    if (i == n-1):
      return jump

    # updating maxReach
    maxReach = max(maxReach, i + arr[i])

    # we use a step to get to the current index
    step -= 1;

    # If no further steps left
    if (step == 0):
      # we must have used a jump
      jump += 1

      # Check if the current index / position or lesser index
      # is the maximum reach point from the previous indexes
      if(i >= maxReach):
        return -1

      # re-initialize the steps to the amount
      # of steps to reach maxReach from position i.
      step = maxReach - i;
  return -1

# Driver program to test above function
arr = [1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9]
size = len(arr)

# Calling the minJumps function
print("Minimum number of jumps to reach end is % d " % minJumps(arr, size))

# This code is contributed by Aditi Sharma
```

## <u>C#</u>

```
// C# program to count Minimum
// number of jumps to reach end
using System;

class GFG {
    static int minJumps(int[] arr)
    {
        if (arr.Length <= 1)
            return 0;

        // Return -1 if not
        // possible to jump
        if (arr[0] == 0)
            return -1;

        // initialization
        int maxReach = arr[0];
        int step = arr[0];
        int jump = 1;

        // Start traversing array
        for (int i = 1; i < arr.Length; i++) {
            // Check if we have reached
            // the end of the array
            if (i == arr.Length - 1)
                return jump;

            // updating maxReach
            maxReach = Math.Max(maxReach, i + arr[i]);

            // we use a step to get
            // to the current index
            step--;

            // If no further steps left
            if (step == 0) {
                // we must have used a jump
                jump++;

                // Check if the current index/position
                // or lesser index is the maximum reach
                // point from the previous indexes
                if (i >= maxReach)
                    return -1;

                // re-initialize the steps to
                // the amount of steps to reach
                // maxReach from position i.
                step = maxReach - i;
            }
        }

        return -1;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = new int[] { 1, 3, 5, 8, 9, 2,
                                6, 7, 6, 8, 9 };

        // calling minJumps method
        Console.Write(minJumps(arr));
    }
}

// This code is contributed
// by nitin mittal
```

## <u>服务器端编程语言（Professional Hypertext Preprocessor 的缩写）</u>

```
<?php
// PHP program to count Minimum number
// of jumps to reach end

// Returns minimum number of jumps to reach arr[n-1] from arr[0]
function minJumps(&$arr, $n)
{

    // The number of jumps needed to reach the starting index is 0
    if ($n <= 1)
        return 0;

    // Return -1 if not possible to jump
    if ($arr[0] == 0)
        return -1;

    // initialization
    // stores all time the maximal reachable index in the array.
    $maxReach = $arr[0];

    // stores the number of steps we can still take
    $step = $arr[0];

    //stores the number of jumps necessary to reach that
    //  maximal reachable position.    
    $jump =1;

    // Start traversing array
    $i=1;
    for ($i = 1; $i < $n; $i++)
    {
        // Check if we have reached the end of the array
        if ($i == $n-1)
            return $jump;

        // updating maxReach
        $maxReach = max($maxReach, $i+$arr[$i]);

        // we use a step to get to the current index
        $step--;

        // If no further steps left
        if ($step == 0)
        {
            // we must have used a jump
            $jump++;

            // Check if the current index/position or lesser index
            // is the maximum reach point from the previous indexes
            if($i >= $maxReach)
                return -1;

            // re-initialize the steps to the amount
            // of steps to reach maxReach from position i.
            $step = $maxReach - $i;
        }
    }

    return -1;
}

// Driver program to test above function

$arr=array(1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9);
$size = sizeof($arr)/sizeof($arr[0]);

// Calling the minJumps function
echo "Minimum number of jumps to reach end is "
     . minJumps($arr, $size);
return 0;
// This code is contribute by Ita_c.
?>
```

## <u>java 描述语言</u>

```
<script>

// Javascript program to count Minimum number

// Returns minimum number of jumps

// to reach arr[n-1] from arr[0]

function minJumps(arr,n)

{

    // The number of jumps needed to

    // reach the starting index is 0

    if (n <= 1)

        return 0;

    // Return -1 if not possible to jump

    if (arr[0] == 0)

        return -1;

    // initialization

    // stores all time the maximal

    // reachable index in the array.

    let maxReach = arr[0];

    // stores the number of steps

    // we can still take

    let step = arr[0];

    // stores the number of jumps

    // necessary to reach that maximal

    // reachable position.

    let jump = 1;

    // Start traversing array

    let i = 1;

    for (i = 1; i < n; i++) {

        // Check if we have reached the end of the array

        if (i == n - 1)

            return jump;

        // updating maxReach

        maxReach =Math.max(maxReach, i + arr[i]);

        // we use a step to get to the current index

        step--;

        // If no further steps left

        if (step == 0) {

            // we must have used a jump

            jump++;

            // Check if the current index/position or lesser index

            // is the maximum reach point from the previous indexes

            if (i >= maxReach)

                return -1;

            // re-initialize the steps to the amount

            // of steps to reach maxReach from position i.

            step = maxReach - i;

        }

    }

    return -1;

}

// Driver program to test above function

    var arr = [ 1, 3, 5, 8, 9, 2, 6, 7, 6, 8,9 ];

    let size = arr.length;

    // Calling the minJumps function

    document.write("Minimum number of jumps to reach end is "+

             minJumps(arr, size));

// This code is contributed by

// Potta Lokesh

</script>
```

<u>**Output**

```
3
```</u> 

<u>**复杂度分析:**</u>

*   <u>**时间复杂度:** O(n)。
    只需要遍历一次数组。</u>
*   <u>**辅助空间:** O(1)。
    不需要空间。</u>

<u>参考资料:StackoverflowThanks 感谢 Chiranjeev Jain 提出这个解决方案。本文由 Sahil Chhabra 和 Gaurav Miglani 供稿。如果你喜欢极客博客并想投稿，你也可以用 write.geeksforgeeks.org 写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。</u>

<u>**另一种方法:**</u>

1.  <u>为了解决到达阵列末端的最小跳跃，</u>
2.  <u>对于每个跳转索引，我们考虑需要评估索引中对应的步长值，并使用该索引值将数组分成子部分，并找出索引覆盖的最大步长。</u>
3.  <u>下面的代码和解释会给你一个清晰的概念:</u>
4.  <u>在每个子阵列中，找出最大距离覆盖索引作为阵列的第一部分，以及第二个阵列</u>

> <u>输入数组:{1，3，5，9，6，2，6，7，6，8，9} ->索引位置以 0 开始</u>
> 
>  <u>步骤:
> 
> 第一步是考虑第一个索引并增加跳转
> 
> 跳转= 1
> 
> 1、{ 3、5、9、6、2、6、7、6、8、9} -> 1 被认为是第一跳
> 
> 下一步
> 
> 从第一步开始，只有一步可走
> 
> 跳转= 2
> 
> 1，3，{ 5，9，6，2，6，7，6，8，9} -> 1 被认为是第一跳
> 
> 下一步
> 
> 现在我们可以灵活选择{5，9，6}中的任何一个，因为最后一步说我们最多可以移动 3 步
> 
> 将其视为一个子阵列，评估每个索引位置的最大距离覆盖范围
> 
> 因为{5，9，6}索引位置是{2，3，4}
> 
> 因此，我们可以涵盖的更远的总步骤:
> 
> {7，12，10} ->我们可以假设{7，12} & {10}是两个子阵列，其中阵列的左边部分表示两个步长覆盖的最大距离，右边的阵列表示剩余值覆盖的最大步长
> 
> 下一步:
> 
> 考虑到第一个数组覆盖的最大距离，我们迭代剩余的下一个元素
> 
> 1,3,9 {6,2, 6, 7, 6, 8, 9}
> 
> 从上面的步骤中，我们已经访问了第 4 个索引，我们继续上面解释的下一个第 5 个索引
> 
> {6，2，6，7，6，8，9}指数位置{4，5，6，7，8，9，10}
> 
> {10,7,12,14,14,17,19}
> 
> 这里的最大步长为 19，对应的索引为 10</u>

## <u>C++</u>

```
// C++ program to illustrate Minimum
// number of jumps to reach end
#include <iostream>
using namespace std;

// Returns minimum number of jumps
// to reach arr[n-1] from arr[0]
int minJumps(int arr[], int n)
{
    // The number of jumps needed to
    // reach the starting index is 0
    if (n <= 1)
        return 0;

    // Return -1 if not possible to jump
    if (arr[0] == 0)
        return -1;

    // Stores the number of jumps
    // necessary to reach that maximal
    // reachable position.
    int jump = 1;

    // Stores the subarray last index
    int subArrEndIndex = arr[0];

    int i = 1;

    // Maximum steps covers in
    // first half of sub array
    int subArrFistHalfMaxSteps = 0;

    // Maximum steps covers
    // in second half of sub array
    int subArrSecondHalfMaxSteps = 0;

    // Start traversing array
    for (i = 1; i < n;) {

        subArrEndIndex = i + subArrEndIndex;

        // Check if we have reached
        // the end of the array
        if (subArrEndIndex >= n)
            return jump;

        int firstHalfMaxStepIndex = 0;

        // Iterate the sub array
        // and find out the maxsteps
        // cover index
        for (; i < subArrEndIndex; i++) {
            int stepsCanCover = arr[i] + i;
            if (subArrFistHalfMaxSteps < stepsCanCover) {
                subArrFistHalfMaxSteps = stepsCanCover;
                subArrSecondHalfMaxSteps = 0;
                firstHalfMaxStepIndex = i;
            }
            else if (subArrSecondHalfMaxSteps
                     < stepsCanCover) {
                subArrSecondHalfMaxSteps = stepsCanCover;
            }
        }
        if (i > subArrFistHalfMaxSteps)
            return -1;
        jump++;

        // Next subarray end index
        // and so far calculated sub
        // array max step cover value
        subArrEndIndex = arr[firstHalfMaxStepIndex];
        subArrFistHalfMaxSteps = subArrSecondHalfMaxSteps;
    }

    return -1;
}

// Driver program to test above function
int main()
{
    int arr[] = { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };
    int size = sizeof(arr) / sizeof(int);

    // Calling the minJumps function
    cout << ("Minimum number of jumps to reach end is %d ",
             minJumps(arr, size));
    return 0;
}
// This code is contributed by praveen.kanike
```

## <u>Java 语言(一种计算机语言，尤用于创建网站)</u>

```
// Java program to illustrate Minimum
// number of jumps to reach end
import java.io.*;
class GFG {

  // Returns minimum number of jumps
  // to reach arr[n-1] from arr[0]
  static int minJumps(int arr[], int n)
  {

    // The number of jumps needed to
    // reach the starting index is 0
    if (n <= 1)
      return 0;

    // Return -1 if not possible to jump
    if (arr[0] == 0)
      return -1;

    // Stores the number of jumps
    // necessary to reach that maximal
    // reachable position.
    int jump = 1;

    // Stores the subarray last index
    int subArrEndIndex = arr[0];

    int i = 1;

    // Maximum steps covers in
    // first half of sub array
    int subArrFistHalfMaxSteps = 0;

    // Maximum steps covers
    // in second half of sub array
    int subArrSecondHalfMaxSteps = 0;

    // Start traversing array
    for (i = 1; i < n;) {

      subArrEndIndex = i + subArrEndIndex;

      // Check if we have reached
      // the end of the array
      if (subArrEndIndex >= n)
        return jump;

      int firstHalfMaxStepIndex = 0;

      // Iterate the sub array
      // and find out the maxsteps
      // cover index
      for (; i < subArrEndIndex; i++) {
        int stepsCanCover = arr[i] + i;
        if (subArrFistHalfMaxSteps < stepsCanCover) {
          subArrFistHalfMaxSteps = stepsCanCover;
          subArrSecondHalfMaxSteps = 0;
          firstHalfMaxStepIndex = i;
        }
        else if (subArrSecondHalfMaxSteps
                 < stepsCanCover) {
          subArrSecondHalfMaxSteps = stepsCanCover;
        }
      }
      if (i > subArrFistHalfMaxSteps)
        return -1;
      jump++;

      // Next subarray end index
      // and so far calculated sub
      // array max step cover value
      subArrEndIndex = arr[firstHalfMaxStepIndex];
      subArrFistHalfMaxSteps = subArrSecondHalfMaxSteps;
    }

    return -1;
  }

  // Driver program to test above function
  public static void main (String[] args)
  {

    int arr[] = { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };
    int size=arr.length;

    // Calling the minJumps function
    System.out.println("Minimum number of jumps to reach end is "+minJumps(arr, size));
  }
}

// This code is contributed by rag2127
```

## <u>C#</u>

```
// C# program to illustrate Minimum
// number of jumps to reach end
using System;
public class GFG
{

  // Returns minimum number of jumps
  // to reach arr[n-1] from arr[0]
  static int minJumps(int[] arr, int n)
  {

    // The number of jumps needed to
    // reach the starting index is 0
    if (n <= 1)
      return 0;

    // Return -1 if not possible to jump
    if (arr[0] == 0)
      return -1;

    // Stores the number of jumps
    // necessary to reach that maximal
    // reachable position.
    int jump = 1;

    // Stores the subarray last index
    int subArrEndIndex = arr[0];

    int i = 1;

    // Maximum steps covers in
    // first half of sub array
    int subArrFistHalfMaxSteps = 0;

    // Maximum steps covers
    // in second half of sub array
    int subArrSecondHalfMaxSteps = 0;

    // Start traversing array
    for (i = 1; i < n;) {

      subArrEndIndex = i + subArrEndIndex;

      // Check if we have reached
      // the end of the array
      if (subArrEndIndex >= n)
        return jump;

      int firstHalfMaxStepIndex = 0;

      // Iterate the sub array
      // and find out the maxsteps
      // cover index
      for (; i < subArrEndIndex; i++)
      {
        int stepsCanCover = arr[i] + i;
        if (subArrFistHalfMaxSteps < stepsCanCover)
        {
          subArrFistHalfMaxSteps = stepsCanCover;
          subArrSecondHalfMaxSteps = 0;
          firstHalfMaxStepIndex = i;
        }
        else if (subArrSecondHalfMaxSteps
                 < stepsCanCover)
        {
          subArrSecondHalfMaxSteps = stepsCanCover;
        }
      }
      if (i > subArrFistHalfMaxSteps)
        return -1;
      jump++;

      // Next subarray end index
      // and so far calculated sub
      // array max step cover value
      subArrEndIndex = arr[firstHalfMaxStepIndex];
      subArrFistHalfMaxSteps = subArrSecondHalfMaxSteps;
    }

    return -1;
  }

  // Driver code
  static public void Main ()
  {
    int[] arr = { 1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 };
    int size = arr.Length;

    // Calling the minJumps function
    Console.WriteLine("Minimum number of jumps to reach end is " +
                      minJumps(arr, size));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## <u>java 描述语言</u>

```
<script>

// Javascript program to count Minimum number

// Returns minimum number of jumps

// to reach arr[n-1] from arr[0]

function minJumps(arr,n)

{

    // The number of jumps needed to

    // reach the starting index is 0

    if (n <= 1)

        return 0;

    // Return -1 if not possible to jump

    if (arr[0] == 0)

        return -1;

    // Stores the number of jumps

    // necessary to reach that maximal

    // reachable position.

    let jump = 1;

    // Stores the subarray last index

    let subArrEndIndex = arr[0];

    let i = 1;

    // Maximum steps covers in

    // first half of sub array

    let subArrFistHalfMaxSteps = 0;

    // Maximum steps covers

    // in second half of sub array

    let subArrSecondHalfMaxSteps = 0;

    // Start traversing array

    for (i = 1; i < n;) {

        subArrEndIndex = i + subArrEndIndex;

        // Check if we have reached

        // the end of the array

        if (subArrEndIndex >= n)

            return jump;

        let firstHalfMaxStepIndex = 0;

        // Iterate the sub array

        // and find out the maxsteps

        // cover index

        for (; i < subArrEndIndex; i++) {

            let stepsCanCover = arr[i] + i;

            if (subArrFistHalfMaxSteps < stepsCanCover) {

                subArrFistHalfMaxSteps = stepsCanCover;

                subArrSecondHalfMaxSteps = 0;

                firstHalfMaxStepIndex = i;

            }

            else if (subArrSecondHalfMaxSteps

                     < stepsCanCover) {

                subArrSecondHalfMaxSteps = stepsCanCover;

            }

        }

        if (i > subArrFistHalfMaxSteps)

            return -1;

        jump++;

        // Next subarray end index

        // and so far calculated sub

        // array max step cover value

        subArrEndIndex = arr[firstHalfMaxStepIndex];

        subArrFistHalfMaxSteps = subArrSecondHalfMaxSteps;

    }

    return -1;

}

// Driver program to test above function

    var arr =[1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9 ];

    let size = arr.length;

    // Calling the minJumps function

    document.write ("Minimum number of jumps to reach end is "+

             minJumps(arr, size));

// This code is contributed by

// Potta Lokesh

</script>
```

<u>**Output**

```
3
```</u> 

<u>**时间复杂度:** O(n)。</u>

<u>**辅助空间:** O(1)。</u>