# 将 N 段分成两个非空组，满足给定条件

> 原文:[https://www . geesforgeks . org/divide-n-segments-in-two-non-empty-group-so-给定条件得到满足/](https://www.geeksforgeeks.org/divide-n-segments-into-two-non-empty-groups-such-that-given-condition-is-satisfied/)

给定由两个非负整数 **L** 和 **R** 表示的 **N** 段(或范围)。将这些线段分成两个非空的组，这样就不会有来自不同组的两个线段共享一个公共点。如果可以这样做，从设置 **{1，2}** 中为每个片段分配一个编号，否则打印**不可能**。
**举例:**

> **输入:** arr[][] = {{5，5}，{2，3}，{3，4}}
> **输出:** 2 1 1
> 由于 2 <sup>nd</sup> 和 3 <sup>rd</sup> 线段有一个公共点，即 3，它们应包含在同一组中。
> **输入:** arr[][] = {{3，5}，{2，3}，{1，4}}
> **输出:**不可能
> 所有线段都应包含在同一组中，因为每对线段都有一个共同点。由于另一组是空的，回答是不可能的。

**先决条件** : [合并重叠区间](https://www.geeksforgeeks.org/merging-intervals/)T4】

**方法:**使用合并重叠区间的概念，我们可以将相同的组分配给所有重叠的段，并交替改变组号。
要合并重叠的线段，请根据其递增的左值对所有线段进行排序，如果左值相等，则首先根据右值对其进行排序，同时保持线段原始索引的顺序。然后，迭代这些段，并检查是否有任何先前的段与当前的段重叠。如果有，就合并成一个片段，如果没有，就创建一个新的片段。
最后，检查其中一个组是否为空。如果其中一个为空，则不可能回答，否则打印所有段的赋值。
以下是上述方法的实施:

## C++

```
// C++ Program to divide N segments
// into two non empty groups such that
// given condition is satisfied

#include<bits/stdc++.h>
using namespace std;

// Function to print the answer if
// it exists using the concept of
// merge overlapping segments
void printAnswer(vector<pair<int,int>> v,int n)
{
      // vec[i].first -> left value
      // vec[i].second.first -> right value
      // vec[i].second.second -> position
    vector<pair<int,pair<int,int>>> vec;
    for(int i=0;i<n;i++)
    {
        vec.push_back({v[i].first,{v[i].second,i}});
    }
    sort(vec.begin(),vec.end());

 // Resultant array
 //   Initialise all the values in resultant array with '2'
 //   except the position at the first index of sorted vec which is initialised as '1'
 //   Initialise maxR to store the maximum of all right values encountered so far
    vector<int> res(n,2);
    int maxR = vec[0].second.first;
    res[vec[0].second.second] = 1;

// If the i-th index has any any point in common with the (i-1)th index classify it as '1'
//    in resultant array and update maxR if necessary
// else we have found the breakpoint and we can exit the loop

    bool ok=false;
    for(int i=1;i<n;i++)
    {
        if(maxR>=vec[i].first)
        {
            res[vec[i].second.second] = res[vec[i-1].second.second];
            maxR=max(maxR,vec[i].second.first);
        }
        else
            {
                ok=true;
                break;
            }
    }
    if(ok)
    {
        for(auto x:res)
            cout << x << " ";
        cout << '\n';
    }
    else
        cout << "Not possible\n";

}

int main()
{
    vector<pair<int,int>> v = {{2,8}, {3,4} , {5,8}, {9,10}};
    int n = (int)v.size();

    printAnswer(v,n);
}
```

## 蟒蛇 3

```
# Python3 Program to divide N segments
# into two non empty groups such that
# given condition is satisfied

# Function to print the answer if
# it exists using the concept of
# merge overlapping segments

def printAnswer(v, n):
    # Sort the indices based on their corresponding value in V   
    indices = list(range(n))
    indices.sort(key=lambda i: v[i])

    # Resultant array
    # Initialise all the values in resultant array with '2'
    # except the first index of 'indices' which is initialised as '1'
    # Initialise maxR to store the maximum of all right values encountered so far
    res = [2] * n
    res[indices[0]] = 1
    maxR=v[indices[0]][1]

    #If the i-th index has any any point in common with the (i-1)th index classify it as '1' in resultant array and update maxR if necessary
    #else we have found the breakpoint and we can exit the loop   
    for i in range(1, n):
        if maxR>=v[indices[i]][0]:
            res[indices[i]]=res[indices[i-1]]
            maxR=max(maxR,v[indices[i]][1])
        else:
            break
    else:
        print("Not possible")
        return
    print(" ".join(map(str,res)))

# Driver Code
if __name__ == "__main__":

    v = [[2, 8], [3, 4], [5, 8], [9, 10]]
    n = len(v)
    printAnswer(v, n)
```

**Output**

```
1 1 1 2 

```

**时间复杂度:** O(n * log n)，其中 n 为段数
**辅助空间** : O(n)。