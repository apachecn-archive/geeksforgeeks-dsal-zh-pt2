# 所有患者感染所需的最长时间

> 原文:[https://www . geesforgeks . org/所有患者感染所需的最长时间/](https://www.geeksforgeeks.org/maximum-time-required-for-all-patients-to-get-infected/)

给定一个仅由 0、1 和 2 组成的[矩阵](https://www.geeksforgeeks.org/matrix/)**arr【】【】**，分别代表**一个空病房**、一个**未感染患者**和一个**感染患者**。在一个时间单位内，指数 **(i，j)** 处的**感染者可以感染与其相邻的**未感染者**，即指数**(I–1，j)** 、 **(i + 1，j)** 、 **(i，j–1)**和 **(i，j + 1)** 。任务是找到感染所有病人所需的最短时间。如果不可能感染所有的患者，那么打印 **"-1"** 。**

**示例:**

> **输入:** arr[][] = {{2，1，0，2，1}，{1，0，1，2，1}，{1，0，0，2，1}}
> **输出:** 2
> **解释:**
> **在时间 t = 1:** 位置{0，0}、{0，3}、{1，3}和{2，3}的患者将在{{0，1}、{ 3 }感染患者
> **在时间 t = 2:** 在{1，0}的患者将被感染，并将在{2，0}感染患者。
> 
> 在上述时间间隔后，所有未感染的患者都被感染。因此，所需的总时间为 2。
> 
> **输入:** arr[][] = {{2，1，0，2，1}，{0，0，1，2，1}，{1，0，0，2，1}}
> **输出:** -1

**方法:**给定的问题可以通过在 2D 矩阵上使用 [BFS 遍历来解决。按照以下步骤解决给定的问题:](https://www.geeksforgeeks.org/breadth-first-traversal-bfs-on-a-2d-array/)

*   初始化一个 [2D 数组](https://www.geeksforgeeks.org/dynamically-allocate-2d-array-c/)，用 **-1** 表示**感染时间[][]** ，这样**感染时间[i][j]** 存储索引 **(i，j)** 的患者被感染的时间。
*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)来存储感染患者及其感染时间的指数。
*   [遍历给定矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/) **arr[][]** 并执行以下操作:
    *   如果单元格 **(i，j)** 的值为 **2** ，则[将该单元格推入队列](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)，感染时间为 **0** ，即 **{i，j，0}** 。
    *   迭代直到[队列为非空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下步骤:
        *   [弹出队列的前元素](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)并将其存储在变量中，比如**当前**。
        *   从当前弹出的单元格 **(i，j)** 开始，如果相邻单元格有未被访问的感染者，则将带有**(当前弹出单元格的感染时间为 1 +时间)**的相邻单元格的索引推入队列。
*   完成上述步骤后，如果访问了所有**感染者**，即所有感染者的感染时间均为非阴性，则[打印矩阵中存在的最大元素](https://www.geeksforgeeks.org/program-to-find-the-maximum-element-in-a-matrix/) **感染时间【】【】**作为感染所有患者所需的最大时间单位。
*   否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Direction arrays
vector<pair<int, int> > direction
    = { { 1, 0 }, { 0, -1 }, { -1, 0 }, { 0, 1 } };

// Function to find the maximum time
// required for all patients to get infected
int maximumTime(vector<vector<int> > arr)
{
    // Stores the number of rows
    int n = arr.size();

    // Stores the number of columns
    int m = arr[0].size();

    // Stores the time of infection
    // of the patient at index (i, j)
    int timeofinfection[n][m];

    // Stores index and time of
    // infection of infected persons
    queue<pair<pair<int, int>, int> > q;

    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // Set the cell as unvisited
            timeofinfection[i][j] = -1;

            // If the current patient
            // is already infected
            if (arr[i][j] == 2) {

                // Push the index and time of
                // infection of current patient
                q.push({ { i, j }, 0 });
                timeofinfection[i][j] = 0;
            }
        }
    }

    // Iterate until queue becomes empty
    while (!q.empty()) {
        // Stores the front element of queue
        pair<pair<int, int>, int> current
            = q.front();

        // Pop out the front element
        q.pop();

        // Check for all four
        // adjacent indices
        for (auto it : direction) {

            // Find the index of the
            // adjacent cell
            int i = current.first.first
                    + it.first;
            int j = current.first.second
                    + it.second;

            // If the current adjacent
            // cell is invalid or it
            // contains an infected patient
            if (i < 0 || j < 0 || i >= n
                || j >= m || arr[i][j] != 1
                || timeofinfection[i][j] != -1) {

                // Continue to the next
                // neighbouring cell
                continue;
            }

            // Push the infected
            // neighbour into queue
            q.push({ { i, j },
                     current.second + 1 });
            timeofinfection[i][j]
                = current.second + 1;
        }
    }

    // Stores the maximum time
    int maxi = INT_MIN;

    // Stores if any uninfected
    // patient exists or not
    int flag = 0;

    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            // If no patient is
            // present at index (i, j)
            if (arr[i][j] != 1)
                continue;

            // If an uninfected patient
            // is present at index (i, j)
            if (arr[i][j] == 1
                && timeofinfection[i][j] == -1) {
                // Set flag as true
                flag = 1;
                break;
            }

            // Update the maximum time of infection
            maxi = max(maxi, timeofinfection[i][j]);
        }
    }

    // If an uninfected patient is present
    if (flag)
        return -1;

    // Return the final result
    return maxi;
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 2, 1, 0, 2, 1 },
            { 1, 0, 1, 2, 1 },
            { 1, 0, 0, 2, 1 } };
    cout << maximumTime(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

static class pair
{
    int first, second, third;

    pair(int first,int second,int third)
    {
         this.first = first;
         this.second = second;
         this.third = third;
    }
}   

// Direction arrays
static int[][] direction = { { 1, 0 }, { 0, -1 },
                             { -1, 0 }, { 0, 1 } };

// Function to find the maximum time
// required for all patients to get infected
static int maximumTime(int[][] arr)
{

    // Stores the number of rows
    int n = arr.length;

    // Stores the number of columns
    int m = arr[0].length;

    // Stores the time of infection
    // of the patient at index (i, j)
    int[][] timeofinfection = new int[n][m];

    // Stores index and time of
    // infection of infected persons
    Queue<pair> q = new LinkedList<>();

    // Traverse the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // Set the cell as unvisited
            timeofinfection[i][j] = -1;

            // If the current patient
            // is already infected
            if (arr[i][j] == 2)
            {

                // Push the index and time of
                // infection of current patient
                q.add(new pair(i, j, 0));
                timeofinfection[i][j] = 0;
            }
        }
    }

    // Iterate until queue becomes empty
    while (!q.isEmpty())
    {

        // Stores the front element of queue
        pair current = q.peek();

        // Pop out the front element
        q.poll();

        // Check for all four
        // adjacent indices
        for(int[] it : direction)
        {

            // Find the index of the
            // adjacent cell
            int i = current.first + it[0];
            int j = current.second + it[1];

            // If the current adjacent
            // cell is invalid or it
            // contains an infected patient
            if (i < 0 || j < 0 || i >= n ||
               j >= m || arr[i][j] != 1 ||
               timeofinfection[i][j] != -1)
            {

                // Continue to the next
                // neighbouring cell
                continue;
            }

            // Push the infected
            // neighbour into queue
            q.add(new pair(i, j ,
                           current.second + 1 ));
            timeofinfection[i][j] = current.third + 1;
        }
    }

    // Stores the maximum time
    int maxi = Integer.MIN_VALUE;

    // Stores if any uninfected
    // patient exists or not
    int flag = 0;

    // Traverse the matrix
    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < m; j++)
        {

            // If no patient is
            // present at index (i, j)
            if (arr[i][j] != 1)
                continue;

            // If an uninfected patient
            // is present at index (i, j)
            if (arr[i][j] == 1 && timeofinfection[i][j] == -1)
            {

                // Set flag as true
                flag = 1;
                break;
            }

            // Update the maximum time of infection
            maxi = Math.max(maxi, timeofinfection[i][j]);
        }
    }

    // If an uninfected patient is present
    if (flag == 1)
        return -1;

    // Return the final result
    return maxi;
}

// Driver code
public static void main(String[] args)
{
    int[][] arr = { { 2, 1, 0, 2, 1 },
                    { 1, 0, 1, 2, 1 },
                    { 1, 0, 0, 2, 1 } };
    System.out.print(maximumTime(arr));
}
}

// This code is contributed by offbeat
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Direction arrays
var direction
    = [ [ 1, 0 ], [ 0, -1 ], [ -1, 0 ], [ 0, 1 ] ];

// Function to find the maximum time
// required for all patients to get infected
function maximumTime(arr)
{
    // Stores the number of rows
    var n = arr.length;

    // Stores the number of columns
    var m = arr[0].length;

    // Stores the time of infection
    // of the patient at index (i, j)
    var timeofinfection = Array.from(Array(n), ()=>Array(m));

    // Stores index and time of
    // infection of infected persons
    var q = [];

    // Traverse the matrix
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {

            // Set the cell as unvisited
            timeofinfection[i][j] = -1;

            // If the current patient
            // is already infected
            if (arr[i][j] == 2) {

                // Push the index and time of
                // infection of current patient
                q.push([ [ i, j ], 0 ]);
                timeofinfection[i][j] = 0;
            }
        }
    }

    // Iterate until queue becomes empty
    while (q.length!=0) {
        // Stores the front element of queue
        var current
            = q[0];

        // Pop out the front element
        q.shift();

        // Check for all four
        // adjacent indices
        for(var it of direction) {

            // Find the index of the
            // adjacent cell
            var i = current[0][0]
                    + it[0];
            var j = current[0][1]
                    + it[1];

            // If the current adjacent
            // cell is invalid or it
            // contains an infected patient
            if (i < 0 || j < 0 || i >= n
                || j >= m || arr[i][j] != 1
                || timeofinfection[i][j] != -1) {

                // Continue to the next
                // neighbouring cell
                continue;
            }

            // Push the infected
            // neighbour into queue
            q.push([[i, j],
                     current[1] + 1 ]);
            timeofinfection[i][j]
                = current[1] + 1;
        }
    }

    // Stores the maximum time
    var maxi = -1000000000;

    // Stores if any uninfected
    // patient exists or not
    var flag = 0;

    // Traverse the matrix
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {
            // If no patient is
            // present at index (i, j)
            if (arr[i][j] != 1)
                continue;

            // If an uninfected patient
            // is present at index (i, j)
            if (arr[i][j] == 1
                && timeofinfection[i][j] == -1) {
                // Set flag as true
                flag = 1;
                break;
            }

            // Update the maximum time of infection
            maxi = Math.max(maxi, timeofinfection[i][j]);
        }
    }

    // If an uninfected patient is present
    if (flag)
        return -1;

    // Return the final result
    return maxi;
}

// Driver Code
var arr
    = [ [ 2, 1, 0, 2, 1 ],
        [ 1, 0, 1, 2, 1 ],
        [ 1, 0, 0, 2, 1 ] ];
document.write( maximumTime(arr));

</script>
```

## 计算机编程语言

```
# function to traverse to nearby possible directions
def bfs(i, j, mat, time):
    # marking position as visited
    mat[i][j] = 0

# stack to store positions that got infected in one unit time
    stack = []

# direction arrays
    row = [-1, 0, 0, 1]
    col = [0, -1, 1, 0]

# traversing to nearby uninfected beds
    for k in range(4):
        x = i+row[k]
        y = j+col[k]

        if x >= 0 and x < r and y >= 0 and y < c and mat[x][y] == 1:
            mat[x][y] = 0
            stack.append((x, y))

# storing the time at which the patient got infected
            time[x][y] = time[i][j]+1

    return stack

# function to calculate maximum time
def maxTime(hospital):

    # array to store the time at which the patients got infected
    time = [[0 for i in range(c)] for j in range(r)]

# to store newly infected ones
    que = []

# initial run
    for i in range(r):
        for j in range(c):
            if hospital[i][j] == 2:
                que += bfs(i, j, hospital, time)

# iterate till every infected patient has done spreading
    while(len(que) != 0):
        for x, y in que:
            temp = bfs(x, y, hospital, time)
        que = temp

# finally calculating maximum time
    res = 0
    for i in range(r):
        for j in range(c):

            # checking if there is any uninfected person
            if hospital[i][j] == 1:
                return -1
            res = max(res, time[i][j])

    return res

# Driver Code Starts
hospital = [[2, 1, 0, 2, 1],
            [1, 0, 1, 2, 1],
            [1, 0, 0, 2, 1]]

r = len(hospital)
c = len(hospital[0])
print(maxTime(hospital))

# Driver Code Ends
```

**Output**

```
2
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*

**方法 2** :这使用了相同的 BFS 遍历技术，但不是使用整数数组来跟踪是否所有患者都被感染，而是使用单个整数，这减少了整体空间消耗和对未感染患者进行额外检查的开销。

基本思想是，我们将在开始时存储未感染的人数，当一个人被感染时，我们将减少这个人数。这将消除最终检查未感染人员的开销。最后一个人被感染的时间将是我们的最终答案。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Direction arrays
vector<pair<int, int> > direction
    = { { 1, 0 }, { 0, -1 }, { -1, 0 }, { 0, 1 } };

// Function to find the maximum time
// required for all patients to get infected
int maximumTime(vector<vector<int> > arr)
{
    // Stores the number of rows
    int n = arr.size();

    // Stores the number of columns
    int m = arr[0].size();

    // Stores whether particular index(i, j)
    // is visited or not 
    vector<vector<bool>> visited(n,vector<bool>(m,0));

    // Stores index and time of
    // infection of infected persons
    queue<pair<pair<int, int>, int> > q;

    //Stores uninfected patients count 
      int uninfected_count=0;

      //Stores time at which last person got infected
      int time = 0;
    // Traverse the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If the current patient
            // is already infected
            if (arr[i][j] == 2) {

                // Push the index of current patient
                // and mark it as visited
                q.push({ { i, j }, 0 });
                visited[i][j] =  1;
            }

            //If current patient is uninfected
              //increment uninfected count
              if(arr[i][j] == 1){
                uninfected_count++;
            }
        }
    }

    // Iterate until queue becomes empty
    while (!q.empty()) {
        // Stores the front element of queue
        pair<pair<int, int>, int> current
            = q.front();

        time = current.second;
        // Pop out the front element
        q.pop();

        // Check for all four
        // adjacent indices
        for (auto it : direction) {

            // Find the index of the
            // adjacent cell
            int i = current.first.first
                    + it.first;
            int j = current.first.second
                    + it.second;

            // If the current adjacent
            // cell is invalid or it
            // contains an infected patient
            if (i < 0 || j < 0 || i >= n
                || j >= m || arr[i][j] != 1
                || visited[i][j] != 0) {

                // Continue to the next
                // neighbouring cell
                continue;
            }

            // Push the infected
            // neighbour into queue
            q.push({ { i, j }, time + 1 });
            visited[i][j] = 1;
              uninfected_count--;
        }
    }

    // If an uninfected patient is present
    if (uninfected_count != 0)
        return -1;

      // Return the final result
    return time;
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 2, 1, 0, 2, 1 },
            { 1, 0, 1, 2, 1 },
            { 1, 0, 0, 2, 1 } };
    cout << maximumTime(arr);

    return 0;
}
// Contributed By Devendra Kolhe
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG{

    static class pair
    {
        int first, second, third;

        pair(int first,int second,int third)
        {
             this.first = first;
             this.second = second;
             this.third = third;
        }
    }

    // Direction arrays
    static int direction[][] = { { 1, 0 }, { 0, -1 },
                            { -1, 0 }, { 0, 1 } };

    // Function to find the maximum time
    // required for all patients to get infected
    static int maximumTime(int arr[][])
    {
        // Stores the number of rows
        int n = arr.length;

        // Stores the number of columns
        int m = arr[0].length;

        // Stores whether particular index(i, j)
        // is visited or not
        boolean visited[][] = new boolean[n][m];

        // Stores index and time of
        // infection of infected persons
        Queue<pair> q = new LinkedList<>();

        //Stores uninfected patients count
        int uninfected_count=0;

        //Stores time at which last person got infected
        int time = 0;
        // Traverse the matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {

                // If the current patient
                // is already infected
                if (arr[i][j] == 2) {

                    // Push the index of current patient
                    // and mark it as visited
                    q.add( new pair(i, j, 0 ));
                    visited[i][j] = true;
                }

                //If current patient is uninfected
                //increment uninfected count
                if(arr[i][j] == 1){
                    uninfected_count++;
                }
            }
        }

        // Iterate until queue becomes empty
        while (!q.isEmpty()) {
            // Stores the front element of queue
            pair current = q.peek();

            time = current.third;
            // Pop out the front element
            q.poll();

            // Check for all four
            // adjacent indices
            for (int[] it : direction) {

                // Find the index of the
                // adjacent cell
                int i = current.first
                        + it[0];
                int j = current.second
                        + it[1];

                // If the current adjacent
                // cell is invalid or it
                // contains an infected patient
                if (i < 0 || j < 0 || i >= n
                    || j >= m || arr[i][j] != 1
                    || visited[i][j]) {

                    // Continue to the next
                    // neighbouring cell
                    continue;
                }

                // Push the infected
                // neighbour into queue
                q.add( new pair( i, j, time + 1 ));
                visited[i][j] = true;
                uninfected_count--;
            }
        }

        // If an uninfected patient is present
        if (uninfected_count != 0)
            return -1;

        // Return the final result
        return time;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[][] = { { 2, 1, 0, 2, 1 },
                    { 1, 0, 1, 2, 1 },
                    { 1, 0, 0, 2, 1 } };

        System.out.println(maximumTime(arr));

    }
}

// This code is contributed by adityapande88.
```

**Output**

```
2
```