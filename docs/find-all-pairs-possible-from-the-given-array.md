# 从给定的数组中找到所有可能的对

> 原文:[https://www . geeksforgeeks . org/从给定数组中查找所有可能的对/](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从给定的数组中找到所有可能的对。
**注:**

1.  **(arr[i]，arr[i])** 也被认为是有效对。
2.  **(arr[i]、arr[j])** 和 **(arr[j]、arr[i])** 被认为是两个不同的对。

**例:**

> **输入:** arr[] = {1，2}
> **输出:** (1，1)，(1，2)，(2，1)，(2，2)。
> **输入:** arr[] = {1，2，3}
> **输出:** (1，1)、(1，2)、(1，3)、(2，1)、(2，2)、(2，3)、(3，1)、(3，2)、(3，3)

**方法:**
为了从[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中找到所有可能的对，我们需要[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并选择对的第一个元素。然后我们需要将这个元素与数组中从索引 0 到 N-1 的所有元素配对。
下面是分步走的方法:

*   遍历数组，并在每次遍历中选择一个元素。
*   对于所选的每个元素，在另一个循环的帮助下遍历数组，并与第二个循环的数组中的每个元素形成该元素对。
*   第二个循环中的数组将从其第一个元素执行到最后一个元素，即从索引 0 到 N-1。
*   打印形成的每一对。

以下是上述方法的实现:

## C++

```
// C++ implementation to find all
// Pairs possible from the given Array

#include <bits/stdc++.h>
using namespace std;

// Function to print all possible
// pairs from the array
void printPairs(int arr[], int n)
{

    // Nested loop for all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << "(" << arr[i] << ", "
                 << arr[j] << ")"
                 << ", ";
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 1, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find all
// Pairs possible from the given Array
class GFG{

// Function to print all possible
// pairs from the array
static void printPairs(int arr[], int n)
{

    // Nested loop for all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            System.out.print("(" +  arr[i]+ ", "
                 + arr[j]+ ")"
                + ", ");
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2 };
    int n = arr.length;

    printPairs(arr, n);

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation to find all
# Pairs possible from the given Array

# Function to prall possible
# pairs from the array
def printPairs(arr, n):

    # Nested loop for all possible pairs
    for i in range(n):
        for j in range(n):
            print("(",arr[i],",",arr[j],")",end=", ")

# Driver code

arr=[1, 2]
n = len(arr)

printPairs(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find all
// Pairs possible from the given Array
using System;

class GFG{

// Function to print all possible
// pairs from the array
static void printPairs(int []arr, int n)
{

    // Nested loop for all possible pairs
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            Console.Write("(" +  arr[i]+ ", "
                 + arr[j]+ ")"
                + ", ");
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 1, 2 };
    int n = arr.Length;

    printPairs(arr, n);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation to find all
// Pairs possible from the given Array

// Function to print all possible
// pairs from the array
function printPairs(arr, n)
{
    // Nested loop for all possible pairs
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < n; j++) {
            document.write("(" + arr[i] + ", "
                 + arr[j] + ")"
                 + ", ");
        }
    }
}

// Driver code
var arr = [ 1, 2 ];
var n = arr.length;
printPairs(arr, n);

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
(1, 1), (1, 2), (2, 1), (2, 2), 
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(1)

## 使用合并排序

**进场:**

在合并排序的合并操作中，我们可以获得所有的对，并且可以将这些对存储到一个对向量中。

只需对合并排序算法做一些修改，我们就可以得到所有的对。

## C++

```
/*
    This code was submitted by : Chirag Mittal from IIIT Dharwad ( username : iitjeechirag )
    storing all the pairs while merging
    Time Complexity : O(N logN)
    Space Complexity : O(N) + O(Number Of Pairs)

    using Merge Sort Algorithm
*/

#include<bits/stdc++.h>
using namespace std;
void getPairsMerge(int arr[],int l,int r,int mid,vector<pair<int,int>>&p){
    int b[l+r+1],i=l,k=l,j=mid+1;
    while(i<=mid && j<=r){
        if(arr[i]>arr[j]){
            b[k]=arr[j];
            p.push_back({arr[i],arr[j]});
            p.push_back({arr[j],arr[i]});
            p.push_back({arr[j],arr[j]});
            k++;
            j++;
        }
        else{
            p.push_back({arr[i],arr[j]});
            p.push_back({arr[j],arr[i]});
            p.push_back({arr[i],arr[i]});
            b[k]=arr[i];
            i++;
            k++;
        }
    }

    while(i<=mid){
        b[k]=arr[i];
        p.push_back({arr[i],arr[i]});
        i++;
        k++;
    }
    while(j<=r){
        b[k]=arr[j];
        p.push_back({arr[j],arr[j]});
        j++;
        k++;
    }

    for(int x=l;x<=r;x++){
        arr[x]=b[x];
    }
}

void getAllPairs(int arr[],int l,int r,vector<pair<int,int>>&p){
    if(l<r){
        int mid=(l+r)/2;
        getAllPairs(arr,l,mid,p);
        getAllPairs(arr,mid+1,r,p);
        getPairsMerge(arr,l,r,mid,p);
    }
}

int main(){
    int n=2;
    int arr[n]={1,2};
    vector<pair<int,int>>p;
    getAllPairs(arr,0,n-1,p);
    for(auto it:p){
        cout<<it.first<<" "<<it.second<<endl;
    }
}
```

**Output**

```
1 2
2 1
1 1
2 2
```

**时间复杂度:** O (N LogN)

**辅助空间:** O(l + r)