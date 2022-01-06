# 要插入的元素数，使数组和为数组异或的两倍

> 原文:[https://www . geeksforgeeks . org/要插入的元素计数-生成数组-数组和-数组异或的两倍/](https://www.geeksforgeeks.org/count-of-elements-to-be-inserted-to-make-array-sum-twice-the-xor-of-array/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找到需要插入到数组中的元素的最小数量，使得数组的[和等于数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)的[异或的两倍。
**举例:**](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/) 

> **输入:** arr[] = {1，2，3，6}
> **输出:** 0
> **解释:**
> Xor = (1 ^ 2 ^ 3 ^ 6) = 6 与数组之和= 12。
> 所需条件(和= 2 * Xor)满足。所以不需要插入更多的元素。
> **输入:** arr[] = {1，2，3}
> **输出:** 1
> **解释:**
> Xor = (1 ^ 2 ^ 3) = 0 和数组之和= (1 + 2 + 3) = 6。
> 这里，我们在数组中插入一个元素{6}。现在，NewXor = (0 ^ 6) = 6，NewSum = (6 + 6) = 12。
> 因此，纽瑟姆= 2 *纽瑟尔。
> 那么，给定条件满足。

**方法:**想法是计算以下步骤，以便找到答案:

*   最初，我们找到数组的和和数组的[异或](https://www.geeksforgeeks.org/find-xor-of-all-elements-in-an-array/)。
*   现在，我们检查给定的条件是否满足。如果它满足，那么打印 0，因为我们不需要插入任何元素。
*   现在，检查异或是否等于 0。如果是，那么需要插入到数组中的元素就是数组中所有元素的总和。
*   这是因为，通过插入 sum，新的 XOR 变为(0 ^和= sum)，并且数组的和变为 sum + sum = 2 * sum。因此条件满足。
*   否则，我们再增加两个元素，即异或和(和+异或)。这是因为:

> NewXor =(异或^(和+异或)^异或)=和+异或。
> NewSum =(Sum+(Sum+Xor)+Xor)= 2 *(Sum+Xor)= 2 * new Xor

以下是上述方法的实现:

## C++

```
// C++ program to find the count
// of elements to be inserted to
// make Array sum twice the XOR of Array
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of elements that need to be
// inserted such that the sum of the
// elements of the array is twice
// the XOR of the array
void insert_element(int a[], int n)
{

    // Variable to store the
    // Xor of all the elements
    int Xor = 0;

    // Variable to store the
    // sum of all elements
    int Sum = 0;

    // Loop to find the Xor
    // and the sum of the array
    for(int i = 0; i < n; i++)
    { 
        Xor ^= a[i];
        Sum += a[i];
    }

    // If sum = 2 * Xor
    if(Sum == 2 * Xor)
    {

        // No need to insert
        // more elements
        cout << "0" << endl;
        return;
     }

    // We insert one more element
    // which is Sum
    if(Xor == 0)
    {
        cout << "1" << endl;
        cout << Sum << endl;
        return;
     }

    // We insert two more elements
    // Sum + Xor and Xor.
    int num1 = Sum + Xor;

    int num2 = Xor;

    // Print the number of elements
    // inserted in the array
    cout << "2";

    // Print the elements that are
    // inserted in the array
    cout << num1 << " "
         << num2 << endl; 
}

// Driver code
int main()
{   
    int a[] = {1, 2, 3};
    int n = sizeof(a) / sizeof(a[0]);

    insert_element(a, n);
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of elements to be inserted to
// make Array sum twice the XOR of Array
class GFG{

// Function to find the minimum
// number of elements that need to be
// inserted such that the sum of the
// elements of the array is twice
// the XOR of the array
static void insert_element(int a[], int n)
{

    // Variable to store the
    // Xor of all the elements
    int Xor = 0;

    // Variable to store the
    // sum of all elements
    int Sum = 0;

    // Loop to find the Xor
    // and the sum of the array
    for(int i = 0; i < n; i++)
    { 
        Xor ^= a[i];
        Sum += a[i];
    }

    // If sum = 2 * Xor
    if(Sum == 2 * Xor)
    {

        // No need to insert
        // more elements
        System.out.println("0");
        return;
     }

    // We insert one more element
    // which is Sum
    if(Xor == 0)
    {
        System.out.println("1");
        System.out.println(Sum);
        return;
     }

    // We insert two more elements
    // Sum + Xor and Xor.
    int num1 = Sum + Xor;

    int num2 = Xor;

    // Print the number of elements
    // inserted in the array
    System.out.print("2");

    // Print the elements that are
    // inserted in the array
    System.out.println(num1 + " " + num2);
}

// Driver code
public static void main(String[] args)
{   
    int a[] = {1, 2, 3};
    int n = a.length;

    insert_element(a, n);
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python program to find the count
# of elements to be inserted to
# make Array sum twice the XOR of Array

# Function to find the minimum
# number of elements that need to be
# inserted such that the sum of the
# elements of the array is twice
# the XOR of the array
def insert_element(a, n):

    # Variable to store the
    # Xor of all the elements
    Xor = 0

    # Variable to store the
    # sum of all elements
    Sum = 0

    # Loop to find the Xor
    # and the sum of the array
    for i in range(n):

        Xor^= a[i]
        Sum+= a[i]

    # If sum = 2 * Xor
    if(Sum == 2 * Xor):

        # No need to insert
        # more elements
        print(0)
        return

    # We insert one more element
    # which is Sum
    if(Xor == 0):
        print(1)
        print(Sum)
        return

    # We insert two more elements
    # Sum + Xor and Xor.
    num1 = Sum + Xor

    num2 = Xor

    # Print the number of elements
    # inserted in the array
    print(2)

    # Print the elements that are
    # inserted in the array
    print(num1, num2)

# Driver code
if __name__ == "__main__":

    a = [1, 2, 3]
    n = len(a)
    insert_element(a, n)
```

## C#

```
// C# program to find the count
// of elements to be inserted to
// make Array sum twice the XOR of Array
using System;
class GFG{

// Function to find the minimum
// number of elements that need to be
// inserted such that the sum of the
// elements of the array is twice
// the XOR of the array
static void insert_element(int[] a, int n)
{

    // Variable to store the
    // Xor of all the elements
    int Xor = 0;

    // Variable to store the
    // sum of all elements
    int Sum = 0;

    // Loop to find the Xor
    // and the sum of the array
    for(int i = 0; i < n; i++)
    { 
        Xor ^= a[i];
        Sum += a[i];
    }

    // If sum = 2 * Xor
    if(Sum == 2 * Xor)
    {

        // No need to insert
        // more elements
        Console.Write("0");
        return;
     }

    // We insert one more element
    // which is Sum
    if(Xor == 0)
    {
        Console.Write("1" + '\n');
        Console.Write(Sum);
        return;
     }

    // We insert two more elements
    // Sum + Xor and Xor.
    int num1 = Sum + Xor;

    int num2 = Xor;

    // Print the number of elements
    // inserted in the array
    Console.Write("2");

    // Print the elements that are
    // inserted in the array
    Console.Write(num1 + " " + num2);
}

// Driver code
public static void Main(string[] args)
{   
    int[] a = {1, 2, 3};
    int n = a.Length;

    insert_element(a, n);
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

    // Javascript program to find the count
    // of elements to be inserted to
    // make Array sum twice the XOR of Array

    // Function to find the minimum
    // number of elements that need to be
    // inserted such that the sum of the
    // elements of the array is twice
    // the XOR of the array
    function insert_element(a, n)
    {

        // Variable to store the
        // Xor of all the elements
        let Xor = 0;

        // Variable to store the
        // sum of all elements
        let Sum = 0;

        // Loop to find the Xor
        // and the sum of the array
        for(let i = 0; i < n; i++)
        {
            Xor ^= a[i];
            Sum += a[i];
        }

        // If sum = 2 * Xor
        if(Sum == 2 * Xor)
        {

            // No need to insert
            // more elements
            document.write("0" + "</br>");
            return;
         }

        // We insert one more element
        // which is Sum
        if(Xor == 0)
        {
            document.write("1" + "</br>");
            document.write(Sum + "</br>");
            return;
         }

        // We insert two more elements
        // Sum + Xor and Xor.
        let num1 = Sum + Xor;

        let num2 = Xor;

        // Print the number of elements
        // inserted in the array
        document.write("2" + "</br>");

        // Print the elements that are
        // inserted in the array
        document.write(num1 + " " + num2 + "</br>");
    }

    let a = [1, 2, 3];
    let n = a.length;

    insert_element(a, n);

</script>
```

**Output:** 

```
1
6
```