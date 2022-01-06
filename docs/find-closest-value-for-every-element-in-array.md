# 找到数组中每个元素的最接近值

> 原文:[https://www . geesforgeks . org/find-数组中每个元素的最接近值/](https://www.geeksforgeeks.org/find-closest-value-for-every-element-in-array/)

给定一个整数数组，为每个元素找到最接近的元素。

示例:

> 输入:arr[] = {10，5，11，6，20，12}
> 输出:6，-1，10，5，12，11
> 
> 输入:arr[] = {10，5，11，10，20，12}
> 输出:5 -1 10 5 12 11

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每个拾取的元素，我们遍历剩余的数组并找到最近的元素。该方案的时间复杂度为 O(n*n)

一个**高效的解决方案**是使用自平衡 BST(实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/))。在自平衡 BST 中，我们可以在 O(Log n)时间内完成插入和最近的更大操作。

```
// Java program to demonstrate insertions in TreeSet
import java.util.*;

class TreeSetDemo {
    public static void closestGreater(int[] arr)
    {
        if (arr.length == -1) {
            System.out.print(-1 + " ");
            return;
        }

        // Insert all array elements into a TreeMap.
        // A TreeMap value indicates whether an element
        // appears once or more.
        TreeMap<Integer, Boolean> tm = 
                    new TreeMap<Integer, Boolean>();
        for (int i = 0; i < arr.length; i++) {

            // A value "True" means that the key
            // appears more than once.
            if (tm.containsKey(arr[i]))
                tm.put(arr[i], true);
            else
                tm.put(arr[i], false);
        }

        // Find smallest greater element for every
        // array element
        for (int i = 0; i < arr.length; i++) {

            // If there are multiple occurrences
            if (tm.get(arr[i]) == true)
            {
                System.out.print(arr[i] + " ");
                continue;
            }

            // If element appears only once
            Integer greater = tm.higherKey(arr[i]);
            Integer lower = tm.lowerKey(arr[i]);
            if (greater == null)
                System.out.print(lower + " ");
            else if (lower == null)
                System.out.print(greater + " ");
            else {
                int d1 = greater - arr[i];
                int d2 = arr[i] - lower;
                if (d1 > d2)
                    System.out.print(lower + " ");
                else
                    System.out.print(greater + " ");
            }
        }
    }

    public static void main(String[] args)
    {
        int[] arr = { 10, 5, 11, 6, 20, 12, 10 };
        closestGreater(arr);
    }
}
```

**Output:**

```
10 6 12 5 12 11 10

```

**练习:**另一个有效的解决方案是使用排序，它也在 O(n Log n)时间内工作。为基于排序的解决方案编写完整的算法和代码。