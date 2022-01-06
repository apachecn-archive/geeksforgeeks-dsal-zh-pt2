# 调试所有程序的最小天数

> 原文:[https://www . geesforgeks . org/调试所有程序的最小天数/](https://www.geeksforgeeks.org/minimum-number-of-days-to-debug-all-programs/)

给定一个数组**代码时间**和一个整数**工作持续时间**中的**和**程序代码及其各自的调试时间，第一个**程序需要**代码时间【I】**个小时才能完成。**工作时间**定义了一个阈值时间，你最多工作**工作时间**连续**个小时然后休息。如果工作时间**少于**6 小时，那么每天可以进行 2 个工作时段，否则每天只能进行一个工作时段。****

**调试应在下列条件下完成:**

*   **一个调试序列应该在同一个会话中完成(以任何顺序)。**
*   **完成前一个调试任务后，可以立即开始新的调试任务。**

**任务是按照上述条件打印调试所有程序所需的**最小天数**。假设**工作时间**大于或等于**编码时间**数组中的最大元素。**

****示例**:**

> ****输入** : codeTime[] = {1，2，3}，WorkingSessionTime = 3
> **输出** : 1
> **说明**:第一个工作环节我们会在 1+2 = 3 个小时内完成第一个和第二个任务，我们可以在第二个工作环节完成最后一个任务，所以完成任务总共需要 2 个工作环节。工作持续时间小于 6，因此我们每天可以进行两次会话，因此最少天数为 1 天**
> 
> ****输入** : codeTime [] = {1，2，3，1，1，3}，WorkingSessionTime = 4
> **输出** : 2
> **解释**:在第一个工作会话中我们将在 1+3 = 4 小时内完成第一个和第三个任务，在第二个会话中我们可以在 1+3 = 4 小时内完成第四个和第六个任务，在第三个会话中我们可以在 2 + 1 = 3 小时内完成第二个和第五个任务。工作时间少于 6 分钟，因此我们每天可以进行两次工作。第一天我们将进行两次工作会议，第二天我们将进行一次工作会议。所以最少需要 2 天**

****方法:**一个简单的解决方法是尝试所有**可能的任务顺序**。首先从数组中选择第一个元素，将其标记为已访问，**递归**处理剩余任务，并在所有可能的订单中找出**最小**会话。这基本上是一个基于[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)的解决方案。找到最少的会议次数后，我们将检查会议的工作时间是否少于 6 小时。如果小于 6，我们将进一步检查最小会话数是偶数还是奇数。** 

****最优方法**:更好的解决方案是使用[位屏蔽和 DP](https://www.geeksforgeeks.org/bitmasking-dynamic-programming-set-2-tsp/)**

**这个想法是利用最多有 14 个任务的事实，所以我们可以使用一个整数变量作为**掩码**来表示哪些元素是**处理的**。如果 ith 位为 **off** ，这意味着 ith 任务还没有处理完，我们还有当前会话的剩余时间。如果 ith 位被**置位**，则表示 ith 程序代码调试任务被处理。**

*   **将掩码初始化为 000…000，表示所有元素的**初始**(未处理)状态。**
*   **将剩余时间作为 0 传递，这意味着当前会话没有剩余时间，我们必须创建一个新会话。**
*   **检查 ith 位是否已处理，如果任务为**未处理**则进行调用。如果 ith 程序代码调试任务未处理，将其标记为已处理。**
*   **如果剩余时间**大于**代码时间【I】，我们将在当前会话中包含第一个程序代码调试任务，**更新**剩余时间，否则我们必须创建新会话，**将**会话数增加 1。**
*   **一旦所有元素都被处理，或者掩码变成 1，我们将获得最少可能的会话。**
*   **如果工作会话时间**小于**6，我们将进一步检查最小可能会话数是偶数还是奇数，如果是偶数，最小天数将是最小会话数的一半，如果是奇数，最小天数将是最小会话数的一半+1，否则最小天数将等于答案。**

**为了处理重叠的子问题，创建一个 2D DP 表来存储**子问题**的答案。对于每个元素 dp[i][j]， **i** 是面具， **j** 是剩余时间。**

**下面是上述方法的实现:**

## **C++14**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// the minimum work sessions
int minSessions(vector<int>& codeTime,
                vector<vector<int> >& dp,
                int ones, int n,
                int mask, int currTime,
                int WorkingSessionTime)
{
    // Break condition
    if (currTime > WorkingSessionTime)
        return INT_MAX;

    // All bits are set
    if (mask == ones)
        return 1;

    // Check if already calculated
    if (dp[mask][currTime] != -1)
        return dp[mask][currTime];

    // Store the answer
    int ans = INT_MAX;
    for (int i = 0; i < n; i++) {
        // Check if ith bit is set or unset
        if ((mask & (1 << i)) == 0) {

            // Including in current work session
            int inc = minSessions(
                codeTime, dp, ones,
                n, mask | (1 << i),
                currTime + codeTime[i],
                WorkingSessionTime);

            // Including in next work session
            int inc_next
                = 1
                  + minSessions(
                        codeTime, dp, ones, n,
                        mask | (1 << i), codeTime[i],
                        WorkingSessionTime);

            // Resultant answer will be minimum of both
            ans = min({ ans, inc, inc_next });
        }
    }
    return dp[mask][currTime] = ans;
}

// Function to initialize DP array
// and solve the problem
int solve(vector<int> codeTime, int n,
          int WorkingSessionTime)
{

    // Initialize dp table with -1
    vector<vector<int> > dp((1 << 14),
                            vector<int>(15, -1));

    // Resultant mask
    int ones = (1 << n) - 1;

    int ans = minSessions(codeTime, dp,
                          ones, n, 0, 0,
                          WorkingSessionTime);

    // no. of minimum work sessions is even
    if (WorkingSessionTime < 6) {
        if (ans % 2 == 0)
            ans = ans / 2;

        // no. of minimum work sessions is odd
        else
            ans = (ans / 2) + 1;
    }

    return ans;
}

// Driver code
int main()
{
    vector<int> codeTime = { 1, 2, 3, 1, 1, 3 };
    int n = codeTime.size();

    int WorkingSessionTime = 4;

    cout
        << solve(codeTime, n, WorkingSessionTime)
        << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.Arrays;

class GFG
{

    // Function to calculate
    // the minimum work sessions
    public static int minSessions(int[] codeTime, int[][] dp,
                                  int ones, int n, int mask,
                                  int currTime,
                                  int WorkingSessionTime)

    {
        // Break condition
        if (currTime > WorkingSessionTime)
            return Integer.MAX_VALUE;

        // All bits are set
        if (mask == ones)
            return 1;

        // Check if already calculated
        if (dp[mask][currTime] != -1)
            return dp[mask][currTime];

        // Store the answer
        int ans = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            // Check if ith bit is set or unset
            if ((mask & (1 << i)) == 0) {

                // Including in current work session
                int inc = minSessions(codeTime, dp, ones, n,
                                      mask | (1 << i), currTime +
                                      codeTime[i], WorkingSessionTime);

                // Including in next work session
                int inc_next = 1 + minSessions(codeTime, dp,
                                               ones, n, mask | (1 << i),
                                               codeTime[i], WorkingSessionTime);

                // Resultant answer will be minimum of both
                ans = Math.min(ans, Math.min(inc, inc_next));
            }
        }
        return dp[mask][currTime] = ans;
    }

    // Function to initialize DP array
    // and solve the problem
    public static int solve(int[] codeTime, int n,
                            int WorkingSessionTime)
    {

        // Initialize dp table with -1
        int[][] dp = new int[(1 << 14)][];

        for (int i = 0; i < 1 << 14; i++) {
            dp[i] = new int[15];
            Arrays.fill(dp[i], -1);
        }

        // Resultant mask
        int ones = (1 << n) - 1;
        int ans = minSessions(codeTime, dp,
                              ones, n, 0, 0,
                              WorkingSessionTime);

        // no. of minimum work sessions is even
        if (WorkingSessionTime < 6)
        {
            if (ans % 2 == 0)
                ans = ans / 2;

            // no. of minimum work sessions is odd
            else
                ans = (ans / 2) + 1;
        }

        return ans;
    }

    // Driver code
    public static void main(String args[]) {
        int[] codeTime = { 1, 2, 3, 1, 1, 3 };
        int n = codeTime.length;

        int WorkingSessionTime = 4;

        System.out.println(solve(codeTime, n, WorkingSessionTime));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## **蟒蛇 3**

```
# Python 3 program for the above approach
import sys

# Function to calculate
# the minimum work sessions
def minSessions(codeTime, dp, ones, n, mask, currTime, WorkingSessionTime):

    # Break condition
    if (currTime > WorkingSessionTime):
        return sys.maxsize

    # All bits are set
    if (mask == ones):
        return 1

    # Check if already calculated
    if (dp[mask][currTime] != -1):
        return dp[mask][currTime]

    # Store the answer
    ans = sys.maxsize
    for i in range(n):

        # Check if ith bit is set or unset
        if ((mask & (1 << i)) == 0):

            # Including in current work session
            inc = minSessions(codeTime, dp, ones, n, mask | (1 << i),currTime + codeTime[i],WorkingSessionTime)

            # Including in next work session
            inc_next = 1 + minSessions(codeTime, dp, ones, n,mask | (1 << i), codeTime[i],WorkingSessionTime)

            # Resultant answer will be minimum of both
            ans = min([ans, inc, inc_next])
    dp[mask][currTime] = ans
    return ans

# Function to initialize DP array
# and solve the problem
def solve(codeTime, n, WorkingSessionTime):

    # Initialize dp table with -1
    dp = [[-1 for i in range(15)] for j in range(1 << 14)]

    # Resultant mask
    ones = (1 << n) - 1

    ans = minSessions(codeTime, dp, ones, n, 0, 0, WorkingSessionTime)

    # no. of minimum work sessions is even
    if (WorkingSessionTime < 6):
        if (ans % 2 == 0):
            ans = ans // 2

        # no. of minimum work sessions is odd
        else:
            ans = (ans / 2) + 1

    return int(ans)

# Driver code
if __name__ == '__main__':
    codeTime = [1, 2, 3, 1, 1, 3]
    n = len(codeTime)

    WorkingSessionTime = 4
    print(solve(codeTime, n, WorkingSessionTime))

    # This code is contributed by SURENDRA_GANGWAR.
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{

      // Function to calculate
    // the minimum work sessions
    public static int minSessions(int[] codeTime, int[, ] dp,
                                  int ones, int n, int mask,
                                  int currTime,
                                  int WorkingSessionTime)

    {

        // Break condition
        if (currTime > WorkingSessionTime)
            return Int32.MaxValue;

        // All bits are set
        if (mask == ones)
            return 1;

        // Check if already calculated
        if (dp[mask, currTime] != -1)
            return dp[mask, currTime];

        // Store the answer
        int ans = Int32.MaxValue;
        for (int i = 0; i < n; i++) {
            // Check if ith bit is set or unset
            if ((mask & (1 << i)) == 0) {

                // Including in current work session
                int inc = minSessions(codeTime, dp, ones, n,
                                      mask | (1 << i), currTime +
                                      codeTime[i], WorkingSessionTime);

                // Including in next work session
                int inc_next = 1 + minSessions(codeTime, dp,
                                               ones, n, mask | (1 << i),
                                               codeTime[i], WorkingSessionTime);

                // Resultant answer will be minimum of both
                ans = Math.Min(ans, Math.Min(inc, inc_next));
            }
        }
        return dp[mask, currTime] = ans;
    }

    // Function to initialize DP array
    // and solve the problem
    public static int solve(int[] codeTime, int n,
                            int WorkingSessionTime)
    {

        // Initialize dp table with -1
        int[, ] dp = new int[(1 << 14), 15];

        for (int i = 0; i < 1 << 14; i++) {

            for(int j = 0; j < 15; j++) {

              dp[i, j] = -1;
            }
        }

        // Resultant mask
        int ones = (1 << n) - 1;
        int ans = minSessions(codeTime, dp,
                              ones, n, 0, 0,
                              WorkingSessionTime);

        // no. of minimum work sessions is even
        if (WorkingSessionTime < 6)
        {
            if (ans % 2 == 0)
                ans = ans / 2;

            // no. of minimum work sessions is odd
            else
                ans = (ans / 2) + 1;
        }

        return ans;
    }

    // Driver code
    static public void Main (){

           int[] codeTime = { 1, 2, 3, 1, 1, 3 };
        int n = codeTime.Length;
        int WorkingSessionTime = 4;
        Console.WriteLine(solve(codeTime, n, WorkingSessionTime));
    }
}

// This code is contributed by Dharanendra L V.
```

## **java 描述语言**

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to calculate
       // the minimum work sessions
       function minSessions(codeTime,
           dp, ones, n, mask, currTime,
           WorkingSessionTime)
       {

           // Break condition
           if (currTime > WorkingSessionTime)
               return Number.MAX_VALUE;

           // All bits are set
           if (mask == ones)
               return 1;

           // Check if already calculated
           if (dp[mask][currTime] != -1)
               return dp[mask][currTime];

           // Store the answer
           let ans = Number.MAX_VALUE;
           for (let i = 0; i < n; i++)
           {

               // Check if ith bit is set or unset
               if ((mask & (1 << i)) == 0)
               {

                   // Including in current work session
                   let inc = minSessions(
                       codeTime, dp, ones,
                       n, mask | (1 << i),
                       currTime + codeTime[i],
                       WorkingSessionTime);

                   // Including in next work session
                   let inc_next = 1 + minSessions(
                           codeTime, dp, ones, n,
                           mask | (1 << i), codeTime[i],
                           WorkingSessionTime);

                   // Resultant answer will be minimum of both
                   ans = Math.min(ans, Math.min(inc, inc_next));
               }
           }
           return dp[mask][currTime] = ans;
       }

       // Function to initialize DP array
       // and solve the problem
       function solve(codeTime, n,
           WorkingSessionTime) {

           // Initialize dp table with -1
           let dp = new Array(1 << 14);

           for (let i = 0; i < dp.length; i++) {
               dp[i] = new Array(15).fill(-1);
           }

           // Resultant mask
           let ones = (1 << n) - 1;

           let ans = minSessions(codeTime, dp,
               ones, n, 0, 0,
               WorkingSessionTime);

           // no. of minimum work sessions is even
           if (WorkingSessionTime < 6) {
               if (ans % 2 == 0)
                   ans = Math.floor(ans / 2);

               // no. of minimum work sessions is odd
               else
                   ans = Math.floor(ans / 2) + 1;
           }

           return ans;
       }

       // Driver code
       let codeTime = [1, 2, 3, 1, 1, 3];
       let n = codeTime.length;

       let WorkingSessionTime = 4;

       document.write(
           solve(codeTime, n, WorkingSessionTime))

    // This code is contributed by Potta Lokesh

   </script>
```

****Output:** 

```
2
```** 

*****时间复杂度*** : O(2^N *工作时间* N)，这里 n 是数组 codeTime 的长度。
***辅助空间*** : O(2^N *工作时间)，dp 表的大小。**