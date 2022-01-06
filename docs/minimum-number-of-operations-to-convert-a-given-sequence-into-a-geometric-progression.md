# 将给定序列转换为几何级数的最小运算次数

> 原文:[https://www . geeksforgeeks . org/将给定序列转换为几何级数的最小操作数/](https://www.geeksforgeeks.org/minimum-number-of-operations-to-convert-a-given-sequence-into-a-geometric-progression/)

给定 N 个元素的序列，一次最多只能对任何元素执行三个操作。这些操作是:

1.  向元素中添加一个。
2.  从元素中减去一。
3.  保持元素不变。

对数组中的所有元素执行任意一个操作。任务是找到可以对序列执行的最小操作数(加法和减法)，以便将其转换为[几何级数](https://en.wikipedia.org/wiki/Geometric_progression)。如果无法通过执行上述操作生成 GP，请打印-1。

**示例**:

> **输入** : a[] = {1，1，4，7，15，33}
> 输出:最小操作数为 4。
> 步骤:
> 
> 1.  保持 a <sub>1</sub> 不变
> 2.  在 <sub>2</sub> 上加一。
> 3.  保持 a <sub>3</sub> 不变
> 4.  从 <sub>4</sub> 中减去一。
> 5.  从 <sub>5</sub> 中减去一。
> 6.  给 <sub>6</sub> 加一。
> 
> 结果序列是{1，2，4，8，16，32}
> 
> **输入** : a[] = {20，15，20，15}
> **输出** : -1

**方法**这里要进行的关键观察是，任何几何级数仅由其前两个元素唯一确定(因为接下来的每对之间的比率必须与由前两个元素组成的这一对之间的比率相同)。因为只有 **3*3** 排列是可能的。操作的可能组合是(+1，+1)、(+1，0)、(+1，-1)、(-1，+1)、(-1，0)、(-1，-1)、(0，+1)、(0，0)和(0，-1)。使用蛮力所有这些 **9** 排列，并检查它们是否在线性时间内形成一个 GP，将会给我们答案。在 GP 中产生组合的最小运算将是答案。

下面是上述方法的实现:

## C++

```
// C++ program to find minimum number
// of operations to convert a given
// sequence to an Geometric Progression
#include <bits/stdc++.h>
using namespace std;

// Function to print the GP series
void construct(int n, pair<double, double> ans_pair)
{
    // Check for possibility
    if (ans_pair.first == -1) {
        cout << "Not possible";
        return;
    }
    double a1 = ans_pair.first;
    double a2 = ans_pair.second;
    double r = a2 / a1;

    cout << "The resultant sequence is:\n";
    for (int i = 1; i <= n; i++) {
        double ai = a1 * pow(r, i - 1);
        cout << ai << " ";
    }
}

// Function for getting the Arithmetic Progression
void findMinimumOperations(double* a, int n)
{
    int ans = INT_MAX;
    // The array c describes all the given set of
    // possible operations.
    int c[] = { -1, 0, 1 };
    // Size of c
    int possibilities = 3;

    // candidate answer
    int pos1 = -1, pos2 = -1;

    // loop through all the permutations of the first two
    // elements.
    for (int i = 0; i < possibilities; i++) {
        for (int j = 0; j < possibilities; j++) {

            // a1 and a2 are the candidate first two elements
            // of the possible GP.
            double a1 = a[1] + c[i];
            double a2 = a[2] + c[j];

            // temp stores the current answer, including the
            // modification of the first two elements.
            int temp = abs(a1 - a[1]) + abs(a2 - a[2]);

            if (a1 == 0 || a2 == 0)
                continue;

            // common ratio of the possible GP
            double r = a2 / a1;

            // To check if the chosen set is valid, and id yes
            // find the number of operations it takes.
            for (int pos = 3; pos <= n; pos++) {

                // ai is value of a[i] according to the assumed
                // first two elements a1, a2
                // ith element of an GP = a1*((a2-a1)^(i-1))
                double ai = a1 * pow(r, pos - 1);

                // Check for the "proposed" element to be only
                // differing by one
                if (a[pos] == ai) {
                    continue;
                }
                else if (a[pos] + 1 == ai || a[pos] - 1 == ai) {
                    temp++;
                }
                else {
                    temp = INT_MAX; // set the temporary ans
                    break; // to infinity and break
                }
            }

            // update answer
            if (temp < ans) {
                ans = temp;
                pos1 = a1;
                pos2 = a2;
            }
        }
    }
    if (ans == -1) {
        cout << "-1";
        return;
    }

    cout << "Minimum Number of Operations are " << ans << "\n";
    pair<double, double> ans_pair = { pos1, pos2 };

    // Calling function to print the sequence
    construct(n, ans_pair);
}

// Driver Code
int main()
{

    // array is 1-indexed, with a[0] = 0
    // for the sake of simplicity
    double a[] = { 0, 7, 20, 49, 125 };

    int n = sizeof(a) / sizeof(a[0]);

    // Function to print the minimum operations
    // and the sequence of elements
    findMinimumOperations(a, n - 1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of operations to convert a given
// sequence to an Geometric Progression
import java.util.*;

class GFG
{

static class pair
{
    double first, second;
    public pair(double first, double second)
    {
        this.first = first;
        this.second = second;
    }
}
// Function to print the GP series
static void construct(int n, pair ans_pair)
{
    // Check for possibility
    if (ans_pair.first == -1)
    {
        System.out.print("Not possible");
        return;
    }
    double a1 = ans_pair.first;
    double a2 = ans_pair.second;
    double r = a2 / a1;

    System.out.print("The resultant sequence is:\n");
    for (int i = 1; i <= n; i++)
    {
        int ai = (int) (a1 * Math.pow(r, i - 1));
        System.out.print(ai + " ");
    }
}

// Function for getting the Arithmetic Progression
static void findMinimumOperations(double []a, int n)
{
    int ans = Integer.MAX_VALUE;

    // The array c describes all the given set of
    // possible operations.
    int c[] = { -1, 0, 1 };

    // Size of c
    int possibilities = 3;

    // candidate answer
    int pos1 = -1, pos2 = -1;

    // loop through all the permutations of the first two
    // elements.
    for (int i = 0; i < possibilities; i++)
    {
        for (int j = 0; j < possibilities; j++)
        {

            // a1 and a2 are the candidate first two elements
            // of the possible GP.
            double a1 = a[1] + c[i];
            double a2 = a[2] + c[j];

            // temp stores the current answer, including the
            // modification of the first two elements.
            int temp = (int) (Math.abs(a1 - a[1]) + Math.abs(a2 - a[2]));

            if (a1 == 0 || a2 == 0)
                continue;

            // common ratio of the possible GP
            double r = a2 / a1;

            // To check if the chosen set is valid, and id yes
            // find the number of operations it takes.
            for (int pos = 3; pos <= n; pos++)
            {

                // ai is value of a[i] according to the assumed
                // first two elements a1, a2
                // ith element of an GP = a1*((a2-a1)^(i-1))
                double ai = a1 * Math.pow(r, pos - 1);

                // Check for the "proposed" element to be only
                // differing by one
                if (a[pos] == ai)
                {
                    continue;
                }
                else if (a[pos] + 1 == ai || a[pos] - 1 == ai)
                {
                    temp++;
                }
                else
                {
                    temp = Integer.MAX_VALUE; // set the temporary ans
                    break; // to infinity and break
                }
            }

            // update answer
            if (temp < ans)
            {
                ans = temp;
                pos1 = (int) a1;
                pos2 = (int) a2;
            }
        }
    }
    if (ans == -1)
    {
        System.out.print("-1");
        return;
    }

    System.out.print("Minimum Number of Operations are " + ans+ "\n");
    pair ans_pair = new pair( pos1, pos2 );

    // Calling function to print the sequence
    construct(n, ans_pair);
}

// Driver Code
public static void main(String[] args)
{

    // array is 1-indexed, with a[0] = 0
    // for the sake of simplicity
    double a[] = { 0, 7, 20, 49, 125 };

    int n = a.length;

    // Function to print the minimum operations
    // and the sequence of elements
    findMinimumOperations(a, n - 1);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find minimum number
# of operations to convert a given
# sequence to an Geometric Progression
from sys import maxsize as INT_MAX

# Function to print the GP series
def construct(n: int, ans_pair: tuple):

    # Check for possibility
    if ans_pair[0] == -1:
        print("Not possible")
        return

    a1 = ans_pair[0]
    a2 = ans_pair[1]
    r = a2 / a1

    print("The resultant sequence is")
    for i in range(1, n + 1):
        ai = a1 * pow(r, i - 1)
        print(int(ai), end=" ")

# Function for getting the Arithmetic Progression
def findMinimumOperations(a: list, n: int):
    ans = INT_MAX

    # The array c describes all the given set of
    # possible operations.
    c = [-1, 0, 1]

    # Size of c
    possibilities = 3

    # candidate answer
    pos1 = -1
    pos2 = -1

    # loop through all the permutations of the first two
    # elements.
    for i in range(possibilities):
        for j in range(possibilities):

            # a1 and a2 are the candidate first two elements
            # of the possible GP.
            a1 = a[1] + c[i]
            a2 = a[2] + c[j]

            # temp stores the current answer, including the
            # modification of the first two elements.
            temp = abs(a1 - a[1]) + abs(a2 - a[2])

            if a1 == 0 or a2 == 0:
                continue

            # common ratio of the possible GP
            r = a2 / a1

            # To check if the chosen set is valid, and id yes
            # find the number of operations it takes.
            for pos in range(3, n + 1):

                # ai is value of a[i] according to the assumed
                # first two elements a1, a2
                # ith element of an GP = a1*((a2-a1)^(i-1))
                ai = a1 * pow(r, pos - 1)

                # Check for the "proposed" element to be only
                # differing by one
                if a[pos] == ai:
                    continue
                elif a[pos] + 1 == ai or a[pos] - 1 == ai:
                    temp += 1
                else:
                    temp = INT_MAX # set the temporary ans
                    break # to infinity and break

            # update answer
            if temp < ans:
                ans = temp
                pos1 = a1
                pos2 = a2
    if ans == -1:
        print("-1")
        return

    print("Minimum number of Operations are", ans)
    ans_pair = (pos1, pos2)

    # Calling function to print the sequence
    construct(n, ans_pair)

# Driver Code
if __name__ == "__main__":

    # array is 1-indexed, with a[0] = 0
    # for the sake of simplicity
    a = [0, 7, 20, 49, 125]
    n = len(a)

    # Function to print the minimum operations
    # and the sequence of elements
    findMinimumOperations(a, n - 1)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find minimum number
// of operations to convert a given
// sequence to an Geometric Progression
using System;

class GFG
{

class pair
{
    public double first, second;
    public pair(double first, double second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to print the GP series
static void construct(int n, pair ans_pair)
{
    // Check for possibility
    if (ans_pair.first == -1)
    {
        Console.Write("Not possible");
        return;
    }
    double a1 = ans_pair.first;
    double a2 = ans_pair.second;
    double r = a2 / a1;

    Console.Write("The resultant sequence is:\n");
    for (int i = 1; i <= n; i++)
    {
        int ai = (int) (a1 * Math.Pow(r, i - 1));
        Console.Write(ai + " ");
    }
}

// Function for getting the Arithmetic Progression
static void findMinimumOperations(double []a, int n)
{
    int ans = int.MaxValue;

    // The array c describes all the given set of
    // possible operations.
    int []c = { -1, 0, 1 };

    // Size of c
    int possibilities = 3;

    // candidate answer
    int pos1 = -1, pos2 = -1;

    // loop through all the permutations of the first two
    // elements.
    for (int i = 0; i < possibilities; i++)
    {
        for (int j = 0; j < possibilities; j++)
        {

            // a1 and a2 are the candidate first two elements
            // of the possible GP.
            double a1 = a[1] + c[i];
            double a2 = a[2] + c[j];

            // temp stores the current answer, including the
            // modification of the first two elements.
            int temp = (int) (Math.Abs(a1 - a[1]) + Math.Abs(a2 - a[2]));

            if (a1 == 0 || a2 == 0)
                continue;

            // common ratio of the possible GP
            double r = a2 / a1;

            // To check if the chosen set is valid, and id yes
            // find the number of operations it takes.
            for (int pos = 3; pos <= n; pos++)
            {

                // ai is value of a[i] according to the assumed
                // first two elements a1, a2
                // ith element of an GP = a1*((a2-a1)^(i-1))
                double ai = a1 * Math.Pow(r, pos - 1);

                // Check for the "proposed" element to be only
                // differing by one
                if (a[pos] == ai)
                {
                    continue;
                }
                else if (a[pos] + 1 == ai || a[pos] - 1 == ai)
                {
                    temp++;
                }
                else
                {
                    temp = int.MaxValue; // set the temporary ans
                    break; // to infinity and break
                }
            }

            // update answer
            if (temp < ans)
            {
                ans = temp;
                pos1 = (int) a1;
                pos2 = (int) a2;
            }
        }
    }
    if (ans == -1)
    {
        Console.Write("-1");
        return;
    }

    Console.Write("Minimum Number of Operations are " + ans+ "\n");
    pair ans_pair = new pair( pos1, pos2 );

    // Calling function to print the sequence
    construct(n, ans_pair);
}

// Driver Code
public static void Main(String[] args)
{

    // array is 1-indexed, with a[0] = 0
    // for the sake of simplicity
    double []a = { 0, 7, 20, 49, 125 };

    int n = a.Length;

    // Function to print the minimum operations
    // and the sequence of elements
    findMinimumOperations(a, n - 1);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find minimum number
// of operations to convert a given
// sequence to an Geometric Progression
class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to print the GP series
function construct(n, ans_pair)
{

    // Check for possibility
    if (ans_pair.first == -1)
    {
        document.write("Not possible");
        return;
    }
    var a1 = ans_pair.first;
    var a2 = ans_pair.second;
    var r = a2 / a1;

    document.write("The resultant sequence is:<br>");
    for(var i = 1; i <= n; i++)
    {
        var ai = parseInt(a1 * Math.pow(r, i - 1));
        document.write(ai + " ");
    }
}

// Function for getting the Arithmetic Progression
function findMinimumOperations(a, n)
{
    var ans = 1000000000;

    // The array c describes all the given
    // set of possible operations.
    var c = [-1, 0, 1];

    // Size of c
    var possibilities = 3;

    // candidate answer
    var pos1 = -1, pos2 = -1;

    // Loop through all the permutations
    // of the first two elements.
    for(var i = 0; i < possibilities; i++)
    {
        for(var j = 0; j < possibilities; j++)
        {

            // a1 and a2 are the candidate first
            // two elements of the possible GP.
            var a1 = a[1] + c[i];
            var a2 = a[2] + c[j];

            // temp stores the current answer,
            // including the modification of
            // the first two elements.
            var temp = (Math.abs(a1 - a[1]) +
                        Math.abs(a2 - a[2]));

            if (a1 == 0 || a2 == 0)
                continue;

            // Common ratio of the possible GP
            var r = a2 / a1;

            // To check if the chosen set is valid,
            // and id yes find the number of
            // operations it takes.
            for(var pos = 3; pos <= n; pos++)
            {

                // ai is value of a[i] according to
                // the assumed first two elements a1, a2
                // ith element of an GP = a1*((a2-a1)^(i-1))
                var ai = a1 * Math.pow(r, pos - 1);

                // Check for the "proposed" element to
                // be only differing by one
                if (a[pos] == ai)
                {
                    continue;
                }
                else if (a[pos] + 1 == ai ||
                         a[pos] - 1 == ai)
                {
                    temp++;
                }
                else
                {

                    // Set the temporary ans
                    temp = 1000000000;

                    // To infinity and break
                    break;
                }
            }

            // Update answer
            if (temp < ans)
            {
                ans = temp;
                pos1 = a1;
                pos2 = a2;
            }
        }
    }
    if (ans == -1)
    {
        document.write("-1");
        return;
    }

    document.write("Minimum Number of " +
                   "Operations are " + ans + "<br>");
    var ans_pair = new pair( pos1, pos2 );

    // Calling function to print the sequence
    construct(n, ans_pair);
}

// Driver Code

// Array is 1-indexed, with a[0] = 0
// for the sake of simplicity
var a = [ 0, 7, 20, 49, 125 ];
var n = a.length;

// Function to print the minimum operations
// and the sequence of elements
findMinimumOperations(a, n - 1);

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
Minimum Number of Operations are 2
The resultant sequence is:
8 20 50 125
```

**时间复杂度** : O(9*N)