# 找到任意两个可能的矩形坐标，这两个坐标是给定的

> 原文:[https://www . geeksforgeeks . org/find-any-any-any-two-coordinates-of-this-two-coordinates-give-give-give-give-give-give-give-give-give-give-give-give-give-give-give-](https://www.geeksforgeeks.org/find-any-possible-two-coordinates-of-rectangle-whose-two-coordinates-are-given/)

给定大小为 **N×N** 的[矩阵](https://www.geeksforgeeks.org/print-a-given-matrix-in-spiral-form/)**mat【】【】【】**，其中矩阵的两个元素是表示矩形坐标的**‘1’**，以及表示空白空间的**‘0’**，任务是找到矩形的另外两个坐标。
**注**:这个问题可能有多个答案，打印任意一个。

**示例:**

> **输入:** mat[][] = {{0，0，1，0}，{0，0，1，0}，{0， *0，0，0}，{0，0，0，0，0*}
> **输出:** {{0，0，1，1}，{0，0，1，1}，{0，0，0，0}，{0，0，0，0}}
> **解释:**
> 0
> 
> **输入:** mat[][] = {{0，0，1，0}，{0，0，0，0}，{1，0，0，0}，{0，0，0，0} }
> T3】输出: {{1，0，1，0，0}，{0，0，0，0}，{1，0，1，0}，{0，0，0，0，0，0 }

**方法:**使用这些给定的坐标可以找到剩余的坐标，因为一些点可能有一个公共行，一些点可能有一个公共列。按照以下步骤解决问题:

*   初始化两对，说 **p1** 和 **p2** 来存储 **1** 在初始矩阵 **mat[]中的位置。**
*   初始化两对，说 **p3** 和 **p4** 存储新的 **1** 要插入的位置，使其成为矩形。
*   [使用两个嵌套循环遍历矩阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，找到配对 **p1** 和 **p2** 。
*   现在有三种可能的情况:
    *   如果 **p1.first** 和 **p2.first** 在这种情况下相同，将 **1** 加到 **p1.first** 和 **p2.first** 给我们 **p3.first** 和 **p4.first** 而 **p3.second** 和 **p4.second** 保持与 **p1.second** 和 **p2 相同。**
    *   如果 **p1.second** 和 **p2.second** 是**T5【同】在这种情况下在 **p1.second** 和 **p2.second** 给我们 **p3.second** 和 **p4.second** 而 **p3.first** 和 **p4.first** 保持不变 **p1.first** 和**
    *   如果没有坐标相同，那么 **p3.first = p2.first** ， **p3.second = p1.second** ， **p4.first = p1.first** 和 **p4.second = p2.second** 。
*   将 **p3** 和 **p4** 的坐标替换为 **1** 并打印矩阵。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the remaining
// two rectangle coordinates
void Create_Rectangle(vector<string> arr, int n)
{

    // Pairs to store the position of given
    // two coordinates of the rectangle.
    pair<int, int> p1 = { -1, -1 };
    pair<int, int> p2 = { -1, -1 };

    // Pairs to store the remaining two
    // coordinates of the rectangle.
    pair<int, int> p3;
    pair<int, int> p4;

    // Traverse through matrix and
    // find pairs p1 and p2
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (arr[i][j] == '1')
                if (p1.first == -1)
                    p1 = { i, j };
                else
                    p2 = { i, j };
        }
    }

    p3 = p1;
    p4 = p2;

    // First Case
    if (p1.first == p2.first) {
        p3.first = (p1.first + 1) % n;
        p4.first = (p2.first + 1) % n;
    }
    // Second Case
    else if (p1.second == p2.second) {
        p3.second = (p1.second + 1) % n;
        p4.second = (p2.second + 1) % n;
    }
    // Third Case
    else {
        swap(p3.first, p4.first);
    }

    arr[p3.first][p3.second] = '1';
    arr[p4.first][p4.second] = '1';

    // Print the matrix
    for (int i = 0; i < n; i++) {
        cout << arr[i] << endl;
    }
}

// Driver code
int main()
{
    // Given Input
    int n = 4;
    vector<string> arr{ "0010", "0000", "1000", "0000" };

    // Function Call
    Create_Rectangle(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.awt.*;
import java.util.*;
class GFG{
    static class pair<T, V>{
        T first;
        V second;
    }

    // Function to find the remaining
    // two rectangle coordinates
    static void Create_Rectangle(ArrayList<String> arr, int n)
    {

        // Pairs to store the position of given
        // two coordinates of the rectangle.
        pair<Integer, Integer> p1 = new pair<>();
        p1.first = -1;
        p1.second= -1;
        pair<Integer, Integer> p2 = new pair<>();
        p2.first = -1;
        p2.second = -1;

        // Pairs to store the remaining two
        // coordinates of the rectangle.
        pair<Integer,Integer> p3 = new pair<>();
        pair<Integer, Integer> p4 = new pair<>();

        // Traverse through matrix and
        // find pairs p1 and p2
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (arr.get(i).charAt(j) == '1')
                    if (p1.first == -1) {
                        p1.first =i;
                        p1.second = j;
                    }
                    else {
                        p2.first = i;
                        p2.second = j;
                    }
            }
        }

        p3 = p1;
        p4 = p2;

        // First Case
        if (p1.first.intValue() == (p2.first).intValue()) {
            p3.first = (p1.first + 1) % n;
            p4.first = (p2.first + 1) % n;
        }
        // Second Case
        else if (p1.second.intValue()==(p2.second).intValue()) {
            p3.second = (p1.second + 1) % n;
            p4.second = (p2.second + 1) % n;
        }
        // Third Case
        else {
            int temp = p3.first;
            p3.first = p4.first;
            p4.first = temp;
        }

        // Print the matrix
        for (int i = 0; i < n; i++) {
            if(i==p3.first){
                for (int j = 0;j<n;j++){
                    if(j==p3.second)
                        System.out.print('1');
                    else
                        System.out.print(arr.get(i).charAt(j));
                }
            }
            else if(i==p4.first){
                for (int j = 0;j<n;j++){
                    if(j==p4.second)
                        System.out.print('1');
                    else
                        System.out.print(arr.get(i).charAt(j));
                }
            }
            else
                System.out.print(arr.get(i));
            System.out.println();
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int n = 4;
        ArrayList<String> arr = new ArrayList<>();
        arr.add("0010");
        arr.add("0000");
        arr.add("1000");
        arr.add("0000");
        //{ , "0000", "1000", "0000" };

        // Function Call
        Create_Rectangle(arr, n);
    }
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the remaining
# two rectangle coordinates
def Create_Rectangle(arr, n):

    for i in range(n):
        arr[i] = [i for i in arr[i]]

    # Pairs to store the position of given
    # two coordinates of the rectangle.
    p1 = [-1, -1]
    p2 = [-1, -1]

    # Pairs to store the remaining two
    # coordinates of the rectangle.
    p3 = []
    p4 = []

    # Traverse through matrix and
    # find pairs p1 and p2
    for i in range(n):
        for j in range(n):
            if (arr[i][j] == '1'):
                if (p1[0] == -1):
                    p1 = [i, j]
                else:
                    p2 = [i, j]

    p3 = p1
    p4 = p2

    # First Case
    if (p1[0] == p2[0]):
        p3[0] = (p1[0] + 1) % n
        p4[0] = (p2[0] + 1) % n
    # Second Case
    elif (p1[1] == p2[1]):
        p3[1] = (p1[1] + 1) % n
        p4[1] = (p2[1] + 1) % n
    # Third Case
    else:
        p3[0], p4[0] = p4[0],p3[0]

    arr[p3[0]][p3[1]] = '1'
    arr[p4[0]][p4[1]] = '1'

    # Print the matrix
    for i in range(n):
        print("".join(arr[i]))

# Driver code
if __name__ == '__main__':
    # Given Input
    n = 4
    arr = ["0010", "0000", "1000", "0000"]

    # Function Call
    Create_Rectangle(arr, n)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the remaining
// two rectangle coordinates
function Create_Rectangle(arr, n) {

    for (let i = 0; i < n; i++) {
        arr[i] = arr[i].split("")
    }
    // Pairs to store the position of given
    // two coordinates of the rectangle.
    let p1 = [-1, -1];
    let p2 = [-1, -1];

    // Pairs to store the remaining two
    // coordinates of the rectangle.
    let p3 = [];
    let p4 = [];

    // Traverse through matrix and
    // find pairs p1 and p2
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++) {
            if (arr[i][j] == '1')
                if (p1[0] == -1)
                    p1 = [i, j];
                else
                    p2 = [i, j];
        }
    }

    p3 = p1;
    p4 = p2;

    // First Case
    if (p1[0] == p2[0]) {
        p3[0] = (p1[0] + 1) % n;
        p4[0] = (p2[0] + 1) % n;
    }
    // Second Case
    else if (p1[1] == p2[1]) {
        p3[1] = (p1[1] + 1) % n;
        p4[1] = (p2[1] + 1) % n;
    }
    // Third Case
    else {
        let temp = p3[0];
        p3[0] = p4[0];
        p4[0] = temp;
    }

    arr[p3[0]][p3[1]] = '1';
    arr[p4[0]][p4[1]] = '1';

    // Print the matrix
    for (let i = 0; i < n; i++) {
        document.write(arr[i].join("") + "<br>");
    }
}

// Driver code

// Given Input
let n = 4;
let arr = ["0010", "0000", "1000", "0000"];

// Function Call
Create_Rectangle(arr, n);

</script>
```

**Output**

```
1010
0000
1010
0000
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*