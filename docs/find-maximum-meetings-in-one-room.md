# 在一个房间内找到最大会议次数

> 原文:[https://www . geeksforgeeks . org/find-最多在一个房间内开会/](https://www.geeksforgeeks.org/find-maximum-meetings-in-one-room/)

一家公司有一个会议室。有 **(S[i]，F[i])** 形式的 **N** 次会议，其中 **S[i]** 为会议 **i** 的开始时间， **F[i]** 为会议 **i** 的结束时间。任务是找到会议室可以容纳的最大会议数量。打印所有会议号码

**示例:**

> **输入:** s[] = {1，3，0，5，8，5}，f[] = {2，4，6，7，9，9}
> **输出:** 1 2 4 5
> 第一次会议【1，2】
> 第二次会议【3，4】
> 第四次会议【5，7】
> 第五次会议【8，9】
> 
> **输入:** s[] = {75250，50074，43659，8931，11273，27545，50879，77924}，
> f[] = {112960，114515，81825，93424，54316，35533，73383，160252 }
> **输出:【T0**

**方法:**
思路是用和活动选择问题一样的贪婪方法来解决问题。

*   按照每对的第二个数字(完成时间)的递增顺序对所有对(会议)进行排序。
*   选择已排序对的第一次会议作为房间中的第一次会议，并将其推入结果向量，并使用第一次选定会议的第二个值(结束时间)设置可变的 time_limit(比方说)。
*   从数组的第二对迭代到最后一对，如果当前对的第一个元素(会议开始时间)的值大于先前选择的对结束时间(time_limit)，则选择当前对并更新结果向量(将选定的会议号推入向量)和可变 time_limit。
*   从矢量打印会议顺序。

下面是上述方法的实现。

## C++

```
// C++ program to find maximum number of meetings
#include <bits/stdc++.h>
using namespace std;

// Function for finding maximum meeting in one room
void maxMeetings(int s[], int f[], int n)
{
    pair<int, int> a[n + 1];
    int i;
    for (i = 0; i < n; i++) {
        a[i].first = f[i];
        a[i].second = i;
    }
    // Sorting of meeting according to their finish time.
    sort(a, a + n);

    // time_limit to check whether new
    // meeting can be conducted or not.
    int time_limit = a[0].first;

    // Vector for storing selected meeting.
    vector<int> m;

    // Initially select first meeting.
    m.push_back(a[0].second + 1);

    // Check for all meeting whether it
    // can be selected or not.
    for (i = 1; i < n; i++) {
        if (s[a[i].second] >= time_limit) {
            // Push selected meeting to vector
            m.push_back(a[i].second + 1);

            // update time limit
            time_limit = a[i].first;
        }
    }

    // Print final selected meetings.
    for (int i = 0; i < m.size(); i++) {
        cout << m[i] << " ";
    }
}

// Driver code
int main()
{
    // Starting time
    int s[] = { 1, 3, 0, 5, 8, 5 };

    // Finish time
    int f[] = { 2, 4, 6, 7, 9, 9 };

    // Number of meetings.
    int n = sizeof(s) / sizeof(s[0]);

    // Function call
    maxMeetings(s, f, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of meetings
import java.util.*;

// Comparator function which can compare
// the ending time of the meeting ans
// sort the list
class mycomparator implements Comparator<meeting>
{
    @Override
    public int compare(meeting o1, meeting o2)
    {
        if (o1.end < o2.end)
        {

            // Return -1 if second object is
            // bigger then first
            return -1;
        }
        else if (o1.end > o2.end)

            // Return 1 if second object is
            // smaller then first
            return 1;

        return 0;
    }
}

// Custom class for storing starting time, 
// finishing time and position of meeting.
class meeting
{
    int start;
    int end;
    int pos;

    meeting(int start, int end, int pos)
    {
        this.start = start;
        this.end = end;
        this.pos = pos;
    }
}

class GFG{

// Function for finding maximum meeting in one room
public static void maxMeeting(ArrayList<meeting> al, int s)
{

    // Initialising an arraylist for storing answer
    ArrayList<Integer> m = new ArrayList<>();

    int time_limit = 0;

    mycomparator mc = new mycomparator();

    // Sorting of meeting according to
    // their finish time.
    Collections.sort(al, mc);

    // Initially select first meeting.
    m.add(al.get(0).pos);

    // time_limit to check whether new 
    // meeting can be conducted or not.
    time_limit = al.get(0).end;

    // Check for all meeting whether it 
    // can be selected or not.
    for(int i = 1; i < al.size(); i++)
    {
        if (al.get(i).start > time_limit)
        {

            // Add selected meeting to arraylist
            m.add(al.get(i).pos);

            // Update time limit
            time_limit = al.get(i).end;
        }
    }

    // Print final selected meetings.
     for(int i = 0; i < m.size(); i++)
        System.out.print(m.get(i) + 1 + " ");
}

// Driver Code 
public static void main (String[] args)
{

    // Starting time
    int s[] = { 1, 3, 0, 5, 8, 5 };

    // Finish time
    int f[] = { 2, 4, 6, 7, 9, 9 }; 

    // Defining an arraylist of meet type
    ArrayList<meeting> meet = new ArrayList<>();
    for(int i = 0; i < s.length; i++)

        // Creating object of meeting
        // and adding in the list
        meet.add(new meeting(s[i], f[i], i));

    // Function call
    maxMeeting(meet, meet.size());
}
}

// This code is contributed by Sarthak Sethi
```

## 蟒蛇 3

```
# Python3 program to find maximum number
# of meetings

# Custom class for storing starting time,
# finishing time and position of meeting.
class meeting:

    def __init__(self, start, end, pos):

        self.start = start
        self.end = end
        self.pos = pos

# Function for finding maximum
# meeting in one room
def maxMeeting(l, n):

    # Initialising an arraylist
    # for storing answer
    ans = []

    # Sorting of meeting according to
    # their finish time.
    l.sort(key = lambda x: x.end)

    # Initially select first meeting
    ans.append(l[0].pos)

    # time_limit to check whether new
    # meeting can be conducted or not.
    time_limit = l[0].end

    # Check for all meeting whether it
    # can be selected or not.
    for i in range(1, n):
        if l[i].start > time_limit:
            ans.append(l[i].pos)
            time_limit = l[i].end

    # Print final selected meetings
    for i in ans:
        print(i + 1, end = " ")

    print()

# Driver code
if __name__ == '__main__':

    # Starting time
    s = [ 1, 3, 0, 5, 8, 5 ]

    # Finish time
    f = [ 2, 4, 6, 7, 9, 9 ]

    # Number of meetings.
    n = len(s)

    l = []

    for i in range(n):

        # Creating object of meeting
        # and adding in the list
        l.append(meeting(s[i], f[i], i))

    # Function call
    maxMeeting(l, n)

# This code is contributed by MuskanKalra1
```

**输出:**

```
1 2 4 5
```

**时间复杂度:** O(N log(N))