# 找出数组中所有局部最大值和局部最小值的索引

> 原文:[https://www . geesforgeks . org/find-indexes-of-all-local-maxima-and-local-minima-in-a-array/](https://www.geeksforgeeks.org/find-indices-of-all-local-maxima-and-local-minima-in-an-array/)

给定一个整数数组**【arr】**。任务是找到给定数组中所有[局部最小值](https://www.geeksforgeeks.org/find-local-minima-array/)和[局部最大值](https://www.geeksforgeeks.org/maximum-number-local-extrema/)的索引。
**示例:**

> **输入:**arr =【100，180，260，310，40，535，695】
> **输出:**
> 局部极小点:0 4
> 
> 局部极大值点:3 ^ 6
> **说明:**
> 给定阵可以分解为以下子阵:
> 1。第一子阵
> 【100，180，260，310】
> 局部极小的指数= 0
> 局部极大的指数= 3
> 2。第二子阵列
> 【40，535，695】
> 局部最小值指数= 4
> 局部最大值指数= 6
> 
> **输入:**arr =【23，13，25，29，33，19，34，45，65，67】
> **输出:**
> 局部最小值点:1 5
> 局部最大值点:0 4 9

**方法:**想法是迭代给定的数组 **arr[]** ，并检查数组的每个元素在它们的相邻元素中是最小还是最大。如果它最小，那么它就是局部最小值，如果它最大，那么它就是局部最大值。以下是步骤:

1.  创建两个数组 **max[]** 和 **min[]** 来存储所有的局部最大值和局部最小值。
2.  遍历给定数组，根据以下条件将数组的索引追加到数组 **max[]** 和 **min[]** 中:
    *   如果**arr[I–1]>arr[I]<arr[I+1]**，则将索引附加到 **min[]** 。
    *   如果**arr[I–1]<arr[I]>arr[I+1]**，则将索引附加到 **max[]** 上。
3.  分别检查第一个和最后一个元素的局部最大值和最小值条件。
4.  打印存储在**min【】**和**max【】**中的索引。

以下是上述方法的实施:

## C++

```
// C++ program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find all the local maxima 
// and minima in the given array arr[] 
void findLocalMaximaMinima(int n, int arr[]) 
{ 

    // Empty vector to store points of 
    // local maxima and minima 
    vector<int> mx, mn; 

    // Checking whether the first point is 
    // local maxima or minima or none 
    if (arr[0] > arr[1]) 
        mx.push_back(0); 

    else if (arr[0] < arr[1]) 
        mn.push_back(0); 

    // Iterating over all points to check 
    // local maxima and local minima 
    for(int i = 1; i < n - 1; i++) 
    { 

    // Condition for local minima 
    if ((arr[i - 1] > arr[i]) and 
        (arr[i] < arr[i + 1])) 
        mn.push_back(i); 

    // Condition for local maxima 
    else if ((arr[i - 1] < arr[i]) and 
                (arr[i] > arr[i + 1])) 
        mx.push_back(i); 
    } 

    // Checking whether the last point is 
    // local maxima or minima or none 
    if (arr[n - 1] > arr[n - 2]) 
        mx.push_back(n - 1); 

    else if (arr[n - 1] < arr[n - 2]) 
        mn.push_back(n - 1); 

    // Print all the local maxima and 
    // local minima indexes stored 
    if (mx.size() > 0) 
    { 
        cout << "Points of Local maxima are : "; 
        for(int a : mx) 
        cout << a << " "; 
        cout << endl; 
    } 
    else
        cout << "There are no points of "
            << "Local Maxima \n"; 

    if (mn.size() > 0) 
    { 
        cout << "Points of Local minima are : "; 
        for(int a : mn) 
        cout << a << " "; 
        cout << endl; 
    } 
    else
        cout << "There are no points of "
            << "Local Minima \n"; 
} 

// Driver Code 
int main() 
{ 
    int N = 9; 

    // Given array arr[] 
    int arr[] = { 10, 20, 15, 14, 13, 
                25, 5, 4, 3 }; 

    // Function call 
    findLocalMaximaMinima(N, arr); 
    return 0;     
} 

// This code is contributed by himanshu77 
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
import java.util.*; 
class GFG{ 

// Function to find all the local maxima 
// and minima in the given array arr[] 
public static void findLocalMaximaMinima(int n, 
                                        int[] arr) 
{ 

    // Empty vector to store points of 
    // local maxima and minima 
    Vector<Integer> mx = new Vector<Integer>(); 
    Vector<Integer> mn = new Vector<Integer>(); 

    // Checking whether the first point is 
    // local maxima or minima or none 
    if (arr[0] > arr[1]) 
        mx.add(0); 

    else if (arr[0] < arr[1]) 
        mn.add(0); 

    // Iterating over all points to check 
    // local maxima and local minima 
    for(int i = 1; i < n - 1; i++) 
    { 
        // Condition for local minima 
        if ((arr[i - 1] > arr[i]) && 
            (arr[i] < arr[i + 1])) 
            mn.add(i); 

        // Condition for local maxima 
        else if ((arr[i - 1] < arr[i]) && 
                (arr[i] > arr[i + 1])) 
            mx.add(i); 
    } 

    // Checking whether the last point is 
    // local maxima or minima or none 
    if (arr[n - 1] > arr[n - 2]) 
        mx.add(n - 1); 

    else if (arr[n - 1] < arr[n - 2]) 
        mn.add(n - 1); 

    // Print all the local maxima and 
    // local minima indexes stored 
    if (mx.size() > 0) 
    { 
        System.out.print("Points of Local " + 
                        "maxima are : "); 
        for(Integer a : mx) 
            System.out.print(a + " "); 
        System.out.println(); 
    } 
    else
        System.out.println("There are no points " + 
                        "of Local Maxima "); 

    if (mn.size() > 0) 
    { 
        System.out.print("Points of Local " + 
                        "minima are : "); 
        for(Integer a : mn) 
            System.out.print(a + " "); 
        System.out.println(); 
    } 
    else
        System.out.println("There are no points of " + 
                        "Local Maxima "); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int N = 9; 

    // Given array arr[] 
    int arr[] = { 10, 20, 15, 14, 13, 
                25, 5, 4, 3 }; 

    // Function call 
    findLocalMaximaMinima(N, arr); 
} 
} 

// This code is contributed by divyeshrabadiya07 
```

## 蟒蛇 3

```
# Python3 program for the above approach 

# Function to find all the local maxima 
# and minima in the given array arr[] 

def findLocalMaximaMinima(n, arr): 

    # Empty lists to store points of 
    # local maxima and minima 
    mx = [] 
    mn = [] 

    # Checking whether the first point is 
    # local maxima or minima or neither 
    if(arr[0] > arr[1]): 
        mx.append(0) 
    elif(arr[0] < arr[1]): 
        mn.append(0) 

    # Iterating over all points to check 
    # local maxima and local minima 
    for i in range(1, n-1): 

        # Condition for local minima 
        if(arr[i-1] > arr[i] < arr[i + 1]): 
            mn.append(i) 

        # Condition for local maxima 
        elif(arr[i-1] < arr[i] > arr[i + 1]): 
            mx.append(i) 

    # Checking whether the last point is 
    # local maxima or minima or neither 
    if(arr[-1] > arr[-2]): 
        mx.append(n-1) 
    elif(arr[-1] < arr[-2]): 
        mn.append(n-1) 

        # Print all the local maxima and 
        # local minima indexes stored 
    if(len(mx) > 0): 
        print("Points of Local maxima"\ 
            " are : ", end ='') 
        print(*mx) 
    else: 
        print("There are no points of"\ 
            " Local maxima.") 

    if(len(mn) > 0): 
        print("Points of Local minima"\ 
            " are : ", end ='') 
        print(*mn) 
    else: 
        print("There are no points"\ 
            " of Local minima.") 

# Driver Code 
if __name__ == '__main__': 

    N = 9
    # Given array arr[] 
    arr = [10, 20, 15, 14, 13, 25, 5, 4, 3] 

    # Function Call 
    findLocalMaximaMinima(N, arr) 
```

## C#

```
// C# program for the above approach 
using System; 
using System.Collections; 
using System.Collections.Generic; 

class GFG{

// Function to find all the local maxima 
// and minima in the given array arr[] 
public static void findLocalMaximaMinima(int n,
                                         int[] arr) 
{ 

    // Empty vector to store points of 
    // local maxima and minima 
    ArrayList mx = new ArrayList();
    ArrayList mn = new ArrayList();

    // Checking whether the first point is 
    // local maxima or minima or none 
    if (arr[0] > arr[1]) 
        mx.Add(0); 

    else if (arr[0] < arr[1]) 
        mn.Add(0); 

    // Iterating over all points to check 
    // local maxima and local minima 
    for(int i = 1; i < n - 1; i++)
    {

        // Condition for local minima  
        if ((arr[i - 1] > arr[i]) &&  
            (arr[i] < arr[i + 1])) 
            mn.Add(i); 

        // Condition for local maxima 
        else if ((arr[i - 1] < arr[i]) &&  
                 (arr[i] > arr[i + 1]))  
            mx.Add(i); 
    } 

    // Checking whether the last point is 
    // local maxima or minima or none 
    if (arr[n - 1] > arr[n - 2]) 
        mx.Add(n - 1);

    else if (arr[n - 1] < arr[n - 2])  
        mn.Add(n - 1);  

    // Print all the local maxima and  
    // local minima indexes stored  
    if (mx.Count > 0)  
    { 
        Console.Write("Points of Local " + 
                      "maxima are : ");
        foreach(int a in mx) 
            Console.Write(a + " ");

        Console.Write("\n");
    } 
    else
        Console.Write("There are no points " + 
                      "of Local Maxima ");

    if (mn.Count > 0) 
    { 
        Console.Write("Points of Local " +
                        "minima are : ");
        foreach(int a in mn) 
            Console.Write(a + " ");

        Console.Write("\n");
    } 
    else
        Console.Write("There are no points of " +
                      "Local Maxima ");
} 

// Driver code 
public static void Main(string[] args)
{
    int N = 9; 

    // Given array arr[] 
    int []arr = { 10, 20, 15, 14, 13, 
                  25, 5, 4, 3 }; 

    // Function call 
    findLocalMaximaMinima(N, arr); 
}
}

// This code is contributed by rutvik_56
```

**Output:** 

```
Points of Local maxima are : 1 5
Points of Local minima are : 0 4 8

```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*