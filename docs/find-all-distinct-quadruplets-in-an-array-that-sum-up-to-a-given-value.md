# 找出一个数组中所有不同的四胞胎，这些四胞胎相加得到一个给定值

> 原文:[https://www . geeksforgeeks . org/find-all-distinct-数组中的四胞胎对给定值求和/](https://www.geeksforgeeks.org/find-all-distinct-quadruplets-in-an-array-that-sum-up-to-a-given-value/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是打印所有可能的唯一四胞胎 **(arr[i]、arr[j]、arr[k]、arr[l])** ，它们的和为 **K** ，这样它们的所有索引都是不同的。

**示例:**

> **输入:** arr[] = {1，0，-1，0，-2，2}，K = 0
> **输出:**
> -2-1 1 2
> -2 0 0 2
> -1 0 0 1
> **说明:**
> 下面是和为 K (= 0)的四胞胎:
> 
> *   {-2, -1, 1, 2}
> *   {-2, 0, 0, 2}
> *   {-1, 0, 0, 1}
> 
> **输入:** arr[] = {1，2，3，-1}，目标= 5
> **输出:**
> 1 2 3 -1

**天真方法:**最简单的方法是[从给定数组](https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-set-2/)**arr【】**中生成所有可能的四胞胎，如果四胞胎的元素之和为 **K** ，则在 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 中插入当前四胞胎，避免重复四胞胎的计数。检查完所有四胞胎后，打印存储在 HashSet 中的所有四胞胎。

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(N <sup>4</sup> )*

**有效方法:**上述方法也可以通过使用[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能对的思想来优化。按照给定的步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如说**和**，存储所有可能的四胞胎。
*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java/) ，比如说 **M** ，它存储给定数组的所有可能对的和以及它们相应的索引。
*   [生成给定数组的所有可能对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)并将所有元素对 **(arr[i]，arr[j])** 及其索引 **(i，j)** 存储在哈希表 **M** 中。
*   现在，[再次生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能的对，对于所有元素对的每个和 **(arr[i]，arr[j])** 如果值**(K–sum)**存在于 HashMap **M** 中，则在 HashMap **ans** 中存储当前的四胞胎。
*   完成上述步骤后，打印散列表**和**中存储的所有四胞胎。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

public class GFG {

    // Stores the pair of indices
    static class Pair {

        int index1;
        int index2;

        // Constructor
        Pair(int x, int y)
        {
            index1 = x;
            index2 = y;
        }
    }

    // Function to find the all the
    // unique quadruplets with the
    // elements at different indices
    public static void
    GetQuadruplets(ArrayList<Integer> nums,
                   int target)
    {

        // Stores the sum mapped to
        // a List Of Pair<i, j>
        HashMap<Integer, ArrayList<Pair> > map
            = new HashMap<>();

        // Generate all possible pairs
        // for the HashMap
        for (int i = 0;
             i < nums.size() - 1; i++) {

            for (int j = i + 1;
                 j < nums.size(); j++) {

                // Find the sum of pairs
                // of elements
                int sum = nums.get(i)
                          + nums.get(j);

                // If the sum doesn't
                // exists then update
                // with the new pairs
                if (!map.containsKey(sum)) {

                    ArrayList<Pair> temp
                        = new ArrayList<>();
                    Pair p = new Pair(i, j);
                    temp.add(p);

                    // Update the hashmap
                    map.put(sum, temp);
                }

                // Otherwise, push the new
                // pair of indices to the
                // current sum
                else {

                    ArrayList<Pair> temp
                        = map.get(sum);

                    Pair p = new Pair(i, j);
                    temp.add(p);

                    // Update the hashmap
                    map.put(sum, temp);
                }
            }
        }

        // Stores all the Quadruplets
        HashSet<ArrayList<Integer> > ans
            = new HashSet<ArrayList<Integer> >();

        for (int i = 0;
             i < nums.size() - 1; i++) {

            for (int j = i + 1;
                 j < nums.size(); j++) {

                int lookUp = target
                             - (nums.get(i)
                                + nums.get(j));

                // If the sum with value
                // (K - sum) exists
                if (map.containsKey(lookUp)) {

                    // Get the pair of
                    // indices of sum
                    ArrayList<Pair> temp
                        = map.get(lookUp);

                    for (Pair pair : temp) {

                        // Check if i, j, k
                        // and l are distinct
                        // or not
                        if (pair.index1 != i
                            && pair.index1 != j
                            && pair.index2 != i
                            && pair.index2 != j) {

                            ArrayList<Integer> values
                                = new ArrayList<>();
                            values.add(
                                nums.get(pair.index1));
                            values.add(
                                nums.get(pair.index2));
                            values.add(nums.get(i));
                            values.add(nums.get(j));

                            // Sort the list to
                            // avoid duplicacy
                            Collections.sort(values);

                            // Update the hashset
                            ans.add(values);
                        }
                    }
                }
            }
        }

        // Print all the Quadruplets
        for (ArrayList<Integer> arr : ans) {
            System.out.println(arr);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        ArrayList<Integer> arr = new ArrayList<>();
        arr.add(1);
        arr.add(0);
        arr.add(-1);
        arr.add(0);
        arr.add(-2);
        arr.add(2);
        int K = 0;
        GetQuadruplets(arr, K);
    }
}
```

**Output:**

```
[-2, 0, 0, 2]
[-1, 0, 0, 1]
[-2, -1, 1, 2]

```

***时间复杂度:**O(N<sup>2</sup>* log N)*
***辅助空间:** O(N <sup>2</sup> )*