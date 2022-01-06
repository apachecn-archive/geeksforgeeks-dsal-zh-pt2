# 两栋建筑之间可储存的最大水量

> 原文:[https://www . geesforgeks . org/两栋建筑之间可储存的最大水量/](https://www.geeksforgeeks.org/maximum-water-that-can-be-stored-between-two-buildings/)

给定一个代表 N 个建筑高度的整数数组，任务是删除 N-2 个建筑，使得剩余两个建筑之间能够截留的水量最大。请注意，两栋建筑之间的总积水量是它们之间的间隙(拆除的建筑数量)乘以较小建筑的高度。

**示例:**

> **输入:** arr[] = {1，3，4}
> **输出:** 1
> 我们要计算任意两栋楼之间可以储存的最大水量。
> 高度 1 和高度 3 的建筑物之间的水= 0。
> 高度 1 和高度 4 的建筑物之间的水= 1。
> 高度 3 和高度 4 的建筑物之间的水= 0。
> 因此所有情况的最大值为 1。
> 
> **输入:** arr[] = {2，1，3，4，6，5}
> **输出:** 8
> 我们移除中间 4 栋建筑，得到总存水量为 2 * 4 = 8

**天真的方法:**
检查所有可能的对，能容纳最大水量的对就是答案。高度为 h <sub>1</sub> 和 h <sub>2</sub> 的两栋建筑之间储存的水等于:

```
minimum(h1, h2)*(distance between the buildings-1)
```

我们的任务是最大化每对的价值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Return the maximum water that can be stored
int maxWater(int height[], int n)
{
    int maximum = 0;

    // Check all possible pairs of buildings
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            int current = (min(height[i],
                               height[j])
                           * (j - i - 1));

            // Maximum so far
            maximum = max(maximum, current);
        }
    }
    return maximum;
}

// Driver code
int main()
{
    int height[] = { 2, 1, 3, 4, 6, 5 };
    int n = sizeof(height) / sizeof(height[0]);
    cout << maxWater(height, n);
    return 0;
}

// This code is contributed by ihritik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG {

    // Return the maximum water that can be stored
    static int maxWater(int height[], int n)
    {
        int max = 0;

        // Check all possible pairs of buildings
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int current = (Math.min(height[i],
                                        height[j])
                               * (j - i - 1));

                // Maximum so far
                max = Math.max(max, current);
            }
        }
        return max;
    }

    // Driver code
    public static void main(String[] args)
    {
        int height[] = { 2, 1, 3, 4, 6, 5 };
        int n = height.length;
        System.out.print(maxWater(height, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Return the maximum water
# that can be stored
def maxWater(height, n) :
    maximum = 0;

    # Check all possible pairs of buildings
    for i in range(n - 1) :
        for j in range(i + 1, n) :
            current = min(height[i],
                          height[j]) * (j - i - 1);

            # Maximum so far
            maximum = max(maximum, current);

    return maximum;

# Driver code
if __name__ == "__main__" :
    height = [ 2, 1, 3, 4, 6, 5 ];

    n = len(height);
    print(maxWater(height, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {

    // Return the maximum water that can be stored
    static int maxWater(int[] height, int n)
    {
        int max = 0;

        // Check all possible pairs of buildings
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                int current = (Math.Min(height[i],
                                        height[j])
                               * (j - i - 1));

                // Maximum so far
                max = Math.Max(max, current);
            }
        }
        return max;
    }

    // Driver code
    static public void Main()
    {
        int[] height = { 2, 1, 3, 4, 6, 5 };
        int n = height.Length;
        Console.WriteLine(maxWater(height, n));
    }
}

// This code is ontributed by @tushil.
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Return the maximum water that can be stored
function maxWater( height, n)
{
    let maximum = 0;

    // Check all possible pairs of buildings
    for (let i = 0; i < n - 1; i++) {
        for (let j = i + 1; j < n; j++) {
            let current = (Math.min(height[i],
                               height[j])
                           * (j - i - 1));

            // Maximum so far
            maximum = Math.max(maximum, current);
        }
    }
    return maximum;
}

    // Driver program

    let height = [ 2, 1, 3, 4, 6, 5 ];
    let n = height.length;
    document.write(maxWater(height, n));

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(N*N)

**高效方法:**

*   根据增加的高度对数组进行排序，而不影响原始索引，即(元素，索引)成对出现。
*   然后，对于每个元素，假设它是两个建筑中所需高度最小的建筑，那么所需水的高度将等于所选建筑的高度，宽度将等于所选建筑和要找到的建筑之间的指数差。
*   为了选择最大化水的另一个建筑，另一个建筑必须尽可能远，并且与当前选择的建筑相比必须更高。
*   现在，问题简化为找到排序数组中每栋建筑右边的最小和最大索引。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

bool compareTo(pair<int, int> p1,
               pair<int, int> p2)
{
    return p1.second < p2.second;
}

// Return the maximum water that
// can be stored
int maxWater(int height[], int n)
{

    // Make pairs with indices
    pair<int, int> pairs[n];
    for(int i = 0; i < n; i++)
        pairs[i] = make_pair(i, height[i]);

    // Sort array based on heights
    sort(pairs, pairs + n, compareTo);       

    // To store the min and max index so far
    // from the right
    int minIndSoFar = pairs[n - 1].first;
    int maxIndSoFar = pairs[n - 1].first;
    int maxi = 0;

    for(int i = n - 2; i >= 0; i--)
    {

        // Current building paired with
        // the building greater in height
        // and on the extreme left
        int left = 0;
        if (minIndSoFar < pairs[i].first)
        {
            left = (pairs[i].second *
                   (pairs[i].first -
                        minIndSoFar - 1));
        }

        // Current building paired with
        // the building greater in height
        // and on the extreme right
        int right = 0;
        if (maxIndSoFar > pairs[i].first)
        {
            right = (pairs[i].second *
                        (maxIndSoFar -
                      pairs[i].first - 1));
        }

        // Maximum so far
        maxi = max(left, max(right, maxi));

        // Update the maximum and minimum so far
        minIndSoFar = min(minIndSoFar,
                          pairs[i].first);
        maxIndSoFar = max(maxIndSoFar,
                          pairs[i].first);
    }
    return maxi;
}

// Driver code
int main( )
{
    int height[] = { 2, 1, 3, 4, 6, 5 };
    int n = sizeof(height) / sizeof(height[0]);

    cout << maxWater(height, n);
}

// This code is contributed by manupathria
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.Arrays;

// Class to store the pairs
class Pair implements Comparable<Pair> {
    int ind, val;

    Pair(int ind, int val)
    {
        this.ind = ind;
        this.val = val;
    }

    @Override
    public int compareTo(Pair o)
    {
        if (this.val > o.val)
            return 1;
        return -1;
    }
}

class GFG {

    // Return the maximum water that can be stored
    static int maxWater(int height[], int n)
    {

        // Make pairs with indices
        Pair pairs[] = new Pair[n];
        for (int i = 0; i < n; i++)
            pairs[i] = new Pair(i, height[i]);

        // Sort array based on heights
        Arrays.sort(pairs);

        // To store the min and max index so far
        // from the right
        int minIndSoFar = pairs[n - 1].ind;
        int maxIndSoFar = pairs[n - 1].ind;
        int max = 0;
        for (int i = n - 2; i >= 0; i--) {

            // Current building paired with the building
            // greater in height and on the extreme left
            int left = 0;
            if (minIndSoFar < pairs[i].ind) {
                left = (pairs[i].val * (pairs[i].ind - minIndSoFar - 1));
            }

            // Current building paired with the building
            // greater in height and on the extreme right
            int right = 0;
            if (maxIndSoFar > pairs[i].ind) {
                right = (pairs[i].val * (maxIndSoFar - pairs[i].ind - 1));
            }

            // Maximum so far
            max = Math.max(left, Math.max(right, max));

            // Update the maximum and minimum so far
            minIndSoFar = Math.min(minIndSoFar,
                                   pairs[i].ind);
            maxIndSoFar = Math.max(maxIndSoFar,
                                   pairs[i].ind);
        }

        return max;
    }

    // Driver code
    public static void main(String[] args)
    {
        int height[] = { 2, 1, 3, 4, 6, 5 };
        int n = height.length;

        System.out.print(maxWater(height, n));
    }
}
```

**Output:** 

```
8
```

**时间复杂度:** O(N*log(N))

**两个指针进场:**取两个指针 **i** 和 **j** 分别指向第一个和最后一个建筑，计算这两个建筑之间可以储存的水量。现在增加 **i** 如果**高度【I】<高度【j】**否则减少 **j** 。这是因为可以截留的水取决于小建筑物的高度，从较高的建筑物移动只会减少水量，而不是最大化。最后，打印到目前为止计算出的最大水量。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Return the maximum water that can be stored
int maxWater(int height[], int n)
{

    // To store the maximum water so far
    int maximum = 0;

    // Both the pointers are pointing at the first
    // and the last buildings respectively
    int i = 0, j = n - 1;

    // While the water can be stored between
    // the currently chosen buildings
    while (i < j)
    {

        // Update maximum water so far and increment i
        if (height[i] < height[j])
        {
            maximum = max(maximum, (j - i - 1) * height[i]);
            i++;
        }

        // Update maximum water so far and decrement j
        else if (height[j] < height[i])
        {
            maximum = max(maximum, (j - i - 1) * height[j]);
            j--;
        }

        // Any of the pointers can be updated (or both)
        else
        {
            maximum = max(maximum, (j - i - 1) * height[i]);
            i++;
            j--;
        }
    }

    return maximum;
}

// Driver code
int main()
{

    int height[] = { 2, 1, 3, 4, 6, 5 };

    int n = sizeof(height)/sizeof(height[0]);

    cout<<(maxWater(height, n));
}

// This code is contributed by CrazyPro
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG {

    // Return the maximum water that can be stored
    static int maxWater(int height[], int n)
    {

        // To store the maximum water so far
        int max = 0;

        // Both the pointers are pointing at the first
        // and the last buildings respectively
        int i = 0, j = n - 1;

        // While the water can be stored between
        // the currently chosen buildings
        while (i < j) {

            // Update maximum water so far and increment i
            if (height[i] < height[j]) {
                max = Math.max(max, (j - i - 1) * height[i]);
                i++;
            }

            // Update maximum water so far and decrement j
            else if (height[j] < height[i]) {
                max = Math.max(max, (j - i - 1) * height[j]);
                j--;
            }

            // Any of the pointers can be updated (or both)
            else {
                max = Math.max(max, (j - i - 1) * height[i]);
                i++;
                j--;
            }
        }

        return max;
    }

    // Driver code
    public static void main(String[] args)
    {
        int height[] = { 2, 1, 3, 4, 6, 5 };
        int n = height.length;

        System.out.print(maxWater(height, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Return the maximum water that can be stored
def maxWater(height, n):

    # To store the maximum water so far
    maximum = 0;

    # Both the pointers are pointing at the first
    # and the last buildings respectively
    i = 0
    j = n - 1

    # While the water can be stored between
    # the currently chosen buildings
    while (i < j):

        # Update maximum water so far and increment i
        if (height[i] < height[j]):    
            maximum = max(maximum, (j - i - 1) * height[i]);
            i += 1;

        # Update maximum water so far and decrement j
        elif (height[j] < height[i]):
            maximum = max(maximum, (j - i - 1) * height[j]);
            j -= 1;

        # Any of the pointers can be updated (or both)
        else:    
            maximum = max(maximum, (j - i - 1) * height[i]);
            i += 1;
            j -= 1;

    return maximum;

# Driver code
height = [2, 1, 3, 4, 6, 5]

n = len(height)

print (maxWater(height, n));

# This code is contributed by CrazyPro
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Return the maximum water that can be stored
    static int maxWater(int []height, int n)
    {

        // To store the maximum water so far
        int max = 0;

        // Both the pointers are pointing at the first
        // and the last buildings respectively
        int i = 0, j = n - 1;

        // While the water can be stored between
        // the currently chosen buildings
        while (i < j)
        {

            // Update maximum water so far and increment i
            if (height[i] < height[j])
            {
                max = Math.Max(max, (j - i - 1) * height[i]);
                i++;
            }

            // Update maximum water so far and decrement j
            else if (height[j] < height[i])
            {
                max = Math.Max(max, (j - i - 1) * height[j]);
                j--;
            }

            // Any of the pointers can be updated (or both)
            else
            {
                max = Math.Max(max, (j - i - 1) * height[i]);
                i++;
                j--;
            }
        }

        return max;
    }

    // Driver code
    static public void Main ()
    {

        int []height = { 2, 1, 3, 4, 6, 5 };
        int n = height.Length;

        Console.Write(maxWater(height, n));
    }
}

// This code is contributed by jit_t
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Return the maximum water that can be stored
function maxWater(height, n)
{

    // To store the maximum water so far
    var maximum = 0;

    // Both the pointers are pointing at the first
    // and the last buildings respectively
    var i = 0, j = n - 1;

    // While the water can be stored between
    // the currently chosen buildings
    while (i < j)
    {

        // Update maximum water so far and increment i
        if (height[i] < height[j])
        {
            maximum = Math.max(maximum, (j - i - 1) * height[i]);
            i++;
        }

        // Update maximum water so far and decrement j
        else if (height[j] < height[i])
        {
            maximum = Math.max(maximum, (j - i - 1) * height[j]);
            j--;
        }

        // Any of the pointers can be updated (or both)
        else
        {
            maximum = Math.max(maximum, (j - i - 1) * height[i]);
            i++;
            j--;
        }
    }

    return maximum;
}

// Driver code
var height = [ 2, 1, 3, 4, 6, 5 ];
var n = height.length;
document.write(maxWater(height, n))

</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(N)