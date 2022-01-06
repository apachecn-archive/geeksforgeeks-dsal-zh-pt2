# 在 Java 中使用 HashSet 对包含重复项的字符串进行不同的排列

> 原文:[https://www . geesforgeks . org/distinct-置换字符串-包含重复项-使用-hashset-in-java/](https://www.geeksforgeeks.org/distinct-permutations-of-a-string-containing-duplicates-using-hashset-in-java/)

给定一个可能包含重复字符的字符串**字符串**，任务是打印给定字符串的所有不同排列，以便在输出中不重复任何排列。

**示例:**

> **输入:**str = " ABA "
> T3】输出:T5】ABA
> AAB
> BAA
> 
> **输入:**【str = " ABC】
> **输出:**
> 【ABC】
> 【ACB】
> 【BAC】
> 【CBA】
> cab

**方法:**在[这篇](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)文章中已经讨论了生成给定字符串的所有排列的方法。这种方法产生的所有排列可以存储在[哈希集中](https://www.geeksforgeeks.org/hashset-in-java/)以避免重复。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.util.HashSet;

public class GFG {

    // To store all the generated permutations
    public static HashSet<String> h = new HashSet<String>();

    public static void permute(char s[], int i, int n)
    {

        // If the permutation is complete
        if (i == n) {

            // If set doesn't contain
            // the permutation already
            if (!(h.contains(String.copyValueOf(s)))) {

                h.add(String.copyValueOf(s));

                // Print the generated permutation
                System.out.println(s);
            }
        }

        else {

            // One by one swap the jth
            // character with the ith
            for (int j = i; j <= n; j++) {

                // Swapping a[i] and a[j];
                char temp = s[i];
                s[i] = s[j];
                s[j] = temp;

                // Revert the swapping
                permute(s, i + 1, n);

                temp = s[i];
                s[i] = s[j];
                s[j] = temp;
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        char s[] = { 'A', 'B', 'A' };
        permute(s, 0, s.length - 1);
    }
}
```

**Output:**

```
ABA
AAB
BAA

```