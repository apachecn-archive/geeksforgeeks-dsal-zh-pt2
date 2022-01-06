# 满足给定条件的数组中按字典顺序最小的字符

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的满足给定条件的数组中的最小字符/](https://www.geeksforgeeks.org/lexicographically-smallest-character-from-an-array-that-satisfies-the-given-conditions/)

给定一个由小写字母组成的[字符数组](https://www.geeksforgeeks.org/arrays-in-java/)、**字符串[]** ，以及一个由范围**【0，N–1】**内的数字组成的整数数组 **arr[]** 。以下是将在问题中执行的操作:

1.  [从左到右遍历字符数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **str[]** 。
2.  对于每一个 **i <sup>th</sup>** 索引，存储最小的奇数长度(**>【1】**)间隔(如果存在)，说**【L，R】**，这样 **str[L] = str[R]** 。

任务是从**字符串[]** 中找到恰好满足以下条件之一的字典最小字符:

*   其中**字符串[L] ==字符串[R]** 的字符不存在奇数长度间隔。
*   字符的所有间隔必须包含不同的索引数组元素。

**示例:**

> **输入:** str[] = { 'a '，' b '，' c '，' a '，' e '，' a' }，arr[] = { 4，6 }
> **输出:** a
> **解释:**
> str 中字符' a '可能的最小奇数长度间隔是{ [0，6]，[3，5] }
> 因为间隔[0，6]包含 arr[1]，间隔[3，5]包含 arr[0]。因此，所需的输出是“a”。
> 
> **输入:** str[] = { 'a '，' b '，' c '，' d' }，arr[] = { 3，4 }
> **输出:** a
> **解释:**
> 因为字符数组的任何元素都不存在间隔。因此，str[]的字典最小字符是“a”。
> 
> **输入:** str[] = { 'z '，' z '，' z '，' z' }，arr[] = { 2 }
> **输出:** -1
> **解释:**
> 字符' z '可能的最小奇数长度间隔是{ [0，2]，[1，3] }
> 因为间隔[0，2]包含 arr[0]，并且间隔[1，3]也包含 arr[0]，arr[0]不是不同的索引数组元素。因此，所需的输出为-1。

**方法:**想法是为**str【】**的每个可能的指数找到最小的奇数长度区间。[遍历 str[]](https://www.geeksforgeeks.org/iterating-arrays-java/) 的每个不同字符，检查该字符是否满足上述条件。如果超过一个字符满足上述条件，则打印其中字典序最小的字符。按照以下步骤解决问题:

1.  初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-java/)，比如说**哈希[]** ，检查字符数组中是否有字符，**字符串[]** 。
2.  初始化一个 **{ X，Y }** 形式的[数组列表](https://www.geeksforgeeks.org/arraylist-in-java/)，比如**区间[]** ，以存储最小奇数长度区间的起点和终点。
3.  [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **哈希[]** ，存储 **str[]** 每个不同字符的所有最小奇数长度间隔。
4.  [按照 x 的递增顺序对间隔[]进行排序。](https://www.geeksforgeeks.org/check-if-any-two-intervals-overlap-among-a-given-set-of-intervals/)
5.  [按递增顺序对数组 arr[]进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
6.  通过执行以下操作，检查字符的所有间隔是否满足上述条件:
    *   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-class-in-java-2/)比如说 **PQ** 按照区间的 **Y** 的递增顺序存储区间。
    *   使用变量 **i** 从左到右遍历 **arr[]** 数组。对于**arr【】**的每一个 **i <sup>第</sup>T7】索引，使用变量 **j** 遍历**区间【】**，检查**区间【j】**的起始点是否小于**arr【I】**。如果发现为真，则将间隔插入 **PQ** 。**
    *   如果区间范围内存在**arr【I】**，则移除 **PQ** 的顶部元素，以确保不同的索引数组元素被分配到不同的区间。
    *   如果在任何时间点 **arr[i]** 小于**间隔的终点【I】**或者 **PQ** 的顶部元素的终点小于 **arr[i]** ，则打印 **-1** 。
    *   否则，打印满足条件的数组**arr【】**中字典序最小的字符。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Structure of an interval
    static class SpecialInterval {

        // Stores start point of
        // an interval
        int low = 0;

        // Stores end point of
        // an interval
        int high = 0;

        // Initialize a interval
        SpecialInterval(int low, int high)
        {
            this.low = low;
            this.high = high;
        }
    }

    // Function to check if a character
    // present in arr[] or not
    static boolean[] checkChar(char[] str)
    {

        // hash[i]: Check if character i
        // is present in arr[] or not
        boolean[] hash = new boolean[26];

        // Traverse the character array
        for (int i = 0; i < str.length; i++) {

            // Mark arr[i] as true
            hash[str[i] - 'a'] = true;
        }

        return hash;
    }

    // Function to check if all the intervals of a
    // character satisfies the condition or not
    private static boolean
    checkIfValid(List<SpecialInterval> intervals,
                 int[] arr)
    {

        // If no intervals found for
        // the current character
        if (intervals.size() == 0) {

            return true;
        }

        // Sort intervals on increasing
        // order of start point
        Collections.sort(intervals,
                         (interval1, interval2)
                             -> interval1.low - interval2.low);

        // Store the intervals on increasing
        // order of end point of interval
        PriorityQueue<SpecialInterval> pq
            = new PriorityQueue<SpecialInterval>(
                intervals.size(),
                (interval1, interval2)
                    -> interval1.high - interval2.high);

        // Stores count of array elements that
        // is present in different intervals
        int count = 0;

        // Stores index of an interval
        int j = 0;

        // Traverse the character array
        for (int i = 0; i < arr.length
                        && count < intervals.size();
             i++) {

            // Traverse intervals[] array
            while (j < intervals.size()) {

                // Stores interval
                // at j-th index
                SpecialInterval interval
                    = intervals.get(j);

                // If start point of interval
                // greater than arr[i]
                if (interval.low > arr[i])
                    break;

                // Update j
                j++;

                // Insert interval into pq
                pq.offer(interval);
            }

            // If count of intervals
            // in pq greater than 0
            if (pq.size() > 0) {

                // Stores top element of pq
                SpecialInterval interval
                    = pq.poll();

                // arr[i] does not lie in
                // the range of the interval
                if (arr[i] > interval.high) {
                    break;
                }

                // Update count
                count++;
            }
        }

        return count == intervals.size();
    }

    // Function to find the intervals
    // for each distinct character of str[]
    private static List<SpecialInterval>
    findSpecialIntevals(char[] str, char ch)
    {

        // Stores the odd index
        // of the character array
        int oddPrev = -1;

        // Stores even index of
        // the character array
        int evenPrev = -1;

        // Stores all intervals for each
        // distinct character of str
        List<SpecialInterval> intervals
            = new ArrayList<SpecialInterval>();

        // Traverse the character array
        for (int i = 0; i < str.length;
             i++) {
            if (str[i] == ch) {

                // If i is even
                if (i % 2 == 0) {

                    // If evenPrev not
                    // equal to -1
                    if (evenPrev == -1) {

                        // Update evenPrev
                        evenPrev = i;
                    }
                    else {

                        // Initialize an interval
                        SpecialInterval interval
                            = new SpecialInterval(
                                evenPrev, i);

                        // Insert current interval
                        // into intervals
                        intervals.add(interval);

                        // Update evenPrev
                        evenPrev = -1;
                    }
                }
                else {

                    // If oddPrev not
                    // equal to -1
                    if (oddPrev == -1) {

                        // Update oddPrev
                        oddPrev = i;
                    }
                    else {

                        // Initialize an interval
                        SpecialInterval interval
                            = new SpecialInterval(
                                oddPrev, i);

                        // Insert current interval
                        // into intervals
                        intervals.add(interval);

                        // Update oddPrev
                        oddPrev = -1;
                    }
                }
            }
        }
        return intervals;
    }

    // Function to print lexicographically smallest
    // character that satisfies the condition
    static void printAnswer(char[] str, int arr[])
    {

        // Sort the array
        Arrays.sort(arr);

        // Check if a character is present in
        // str that satisfies the condition
        boolean possible = false;

        // hash[i]: Check if character i
        // is present in arr[] or not
        boolean[] hash = checkChar(str);

        // Traverse all possible distinct
        // character of str
        for (int ch = 0; ch < 26; ch++) {

            // If ch present in str
            if (!hash[ch])
                continue;

            // Find all the intervals for
            // current character
            List<SpecialInterval> intervals
                = findSpecialIntevals(str,
                                      (char)(ch + 'a'));

            // Update possible
            possible
                = checkIfValid(intervals, arr);

            // If a character found in str that
            // satisfies the condition
            if (possible) {
                System.out.println(
                    (char)(ch + 'a'));
                break;
            }
        }

        // If no character found that
        // satisfies the condition
        if (!possible)
            System.out.println(-1);
    }

    // Driver Code
    public static void main(String[] args)
    {

        char[] str = { 'a', 'b', 'c', 'a',
                       'e', 'a', 'a' };

        int arr[] = { 4, 6 };

        printAnswer(str, arr);
    }
}
```

**Output:** 

```
a
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*