# 数组中滑动窗口的中间值

> 原文:[https://www . geeksforgeeks . org/阵列滑动窗口中位数/](https://www.geeksforgeeks.org/median-of-sliding-window-in-an-array/)

给定一个整数**arr【】**和一个整数 **k** 的数组，任务是找到每个大小为 **k** 的窗口的中间值，从左边开始，每次向右移动一个位置。

**示例:**

> **输入:** arr[] = {-1，5，13，8，2，3，3，1}，k = 3
> **输出:**5 8 3 3 3 3
> 
> **输入:** arr[] = {-1，5，13，8，2，3，3，1}，k = 4
> **输出:** 6.5 6.5 5.5 3.0 2.5

**方法:**创建一个配对类来保存项目及其索引。它还实现了[可比接口](https://www.geeksforgeeks.org/comparable-vs-comparator-in-java/)，这样[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)将调用 [compareTo()](https://www.geeksforgeeks.org/java-lang-string-compareto/) 方法来查找节点。请注意，只有当两对的索引相等时，它们才相等。这很重要，因为窗口可能包含重复项，如果我们只检查值，我们可能会在一次 remove()调用中删除多个项。

其思想是维护长度为 **(k / 2)** 和 **(k / 2) + 1** 的 Pair 对象的两个排序集(minSet 和 maxSet)，这取决于 **k** 是偶数还是奇数，minSet 将始终包含窗口 **k** 的第一组数字(较小)，maxSet 将包含第二组数字(较大)。

当我们移动窗口时，我们将从任何一个集合(log n)中移除元素，并添加一个新的元素(log n)来维护上面指定的 minSet 和 maxSet 规则。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.TreeSet;

public class GFG {

    // Pair class for the value and its index
    static class Pair implements Comparable<Pair> {
        private int value, index;

        // Constructor
        public Pair(int v, int p)
        {
            value = v;
            index = p;
        }

        // This method will be used by the treeset to
        // search a value by index and setting the tree
        // nodes (left or right)
        @Override
        public int compareTo(Pair o)
        {

            // Two nodes are equal only when
            // their indices are same
            if (index == o.index) {
                return 0;
            }
            else if (value == o.value) {
                return Integer.compare(index, o.index);
            }
            else {
                return Integer.compare(value, o.value);
            }
        }

        // Function to return the value
        // of the current object
        public int value()
        {
            return value;
        }

        // Update the value and the position
        // for the same object to save space
        public void renew(int v, int p)
        {
            value = v;
            index = p;
        }

        @Override
        public String toString()
        {
            return String.format("(%d, %d)", value, index);
        }
    }

    // Function to print the median for the current window
    static void printMedian(TreeSet<Pair> minSet,
                            TreeSet<Pair> maxSet, int window)
    {

        // If the window size is even then the
        // median will be the average of the
        // two middle elements
        if (window % 2 == 0) {
            System.out.print((minSet.last().value()
                              + maxSet.first().value())
                             / 2.0);
            System.out.print(" ");
        }

        // Else it will be the middle element
        else {
            System.out.print(minSet.size() > maxSet.size()
                                 ? minSet.last().value()
                                 : maxSet.first().value());
            System.out.print(" ");
        }
    }

    // Function to find the median
    // of every window of size k
    static void findMedian(int arr[], int k)
    {
        TreeSet<Pair> minSet = new TreeSet<>();
        TreeSet<Pair> maxSet = new TreeSet<>();

        // To hold the pairs, we will keep renewing
        // these instead of creating the new pairs
        Pair[] windowPairs = new Pair[k];

        for (int i = 0; i < k; i++) {
            windowPairs[i] = new Pair(arr[i], i);
        }

        // Add k/2 items to maxSet
        for (int i = 0; i < k / 2; i++) {
            maxSet.add(windowPairs[i]);
        }

        for (int i = k / 2; i < k; i++) {

            // Below logic is to maintain the
            // maxSet and the minSet criteria
            if (arr[i] < maxSet.first().value()) {
                minSet.add(windowPairs[i]);
            }
            else {
                minSet.add(maxSet.pollFirst());
                maxSet.add(windowPairs[i]);
            }
        }

        printMedian(minSet, maxSet, k);

        for (int i = k; i < arr.length; i++) {

            // Get the pair at the start of the window, this
            // will reset to 0 at every k, 2k, 3k, ...
            Pair temp = windowPairs[i % k];
            if (temp.value() <= minSet.last().value()) {

                // Remove the starting pair of the window
                minSet.remove(temp);

                // Renew window start to new window end
                temp.renew(arr[i], i);

                // Below logic is to maintain the
                // maxSet and the minSet criteria
                if (temp.value() < maxSet.first().value()) {
                    minSet.add(temp);
                }
                else {
                    minSet.add(maxSet.pollFirst());
                    maxSet.add(temp);
                }
            }
            else {
                maxSet.remove(temp);
                temp.renew(arr[i], i);

                // Below logic is to maintain the
                // maxSet and the minSet criteria
                if (temp.value() > minSet.last().value()) {
                    maxSet.add(temp);
                }
                else {
                    maxSet.add(minSet.pollLast());
                    minSet.add(temp);
                }
            }

            printMedian(minSet, maxSet, k);
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = new int[] { 0, 9, 1, 8, 2,
                                7, 3, 6, 4, 5 };
        int k = 3;

        findMedian(arr, k);
    }
}
```

**Output:**

```
1 8 2 7 3 6 4 5

```