# 使所有数组元素为零所需的最小操作次数

> 原文:[https://www . geeksforgeeks . org/最小操作数-制作所有数组元素所需的操作数-零/](https://www.geeksforgeeks.org/minimum-no-of-operations-required-to-make-all-array-elements-zero/)

给定一个由 N 个元素组成的数组，每个元素要么是 1，要么是 0。您需要通过执行以下操作使数组的所有元素都等于 0:

*   如果一个元素是 1，你可以改变它的值等于 0，
    *   如果下一个连续的元素是 1，它将自动转换为 0。
    *   如果下一个连续元素已经是 0，则不会发生任何事情。

现在，任务是找到使所有元素等于 0 所需的最小操作数。
**例**:

```
Input : arr[] = {1, 1, 0, 0, 1, 1, 1, 0, 0, 1} 
Output : Minimum changes: 3 

Input : arr[] = {1, 1, 1, 1}
Output : Minimum changes: 1 
```

**<u>进场 1:</u>**

若要找到所需的最小更改数，请从左到右迭代数组，并检查当前元素是否为 1。如果当前元素为 1，则将其更改为 0，并将计数增加 1，并在下一个操作中搜索 0，因为所有连续的 1 将自动转换为 0。

**时间复杂度:** O(n <sup>2</sup>

下面是上述方法的实现:

## C++

```
// CPP program to find  minimum number of
// operations required to make all
// array elements zero

#include <bits/stdc++.h>
using namespace std;

// Function to find  minimum number of
// operations required to make all
// array elements zero
int minimumChanges(int arr[], int n)
{
    int i;

    // It will maintain total changes required
    int changes = 0;

    for (i = 0; i < n; i++)
    {  
        // Check for the first 1
        if (arr[i] == 1)
        {  
            int j;

            // Check for number of
            // consecutive 1's
            for(j = i+1; j<n; j++)
            {
                if(arr[j]==0)
                    break;
            }

            // Increment i to the position of
            // last consecutive 1
            i = j-1;

            changes++;
        }
    }

    return changes;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 0, 0, 0, 1, 0, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Minimum operations: " << minimumChanges(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of operations required
// to make all array elements zero

class GFG
{

// Function to find minimum number
// of operations required to make 
// all array elements zero
static int minimumChanges(int arr[],
                          int n)
{
    int i;

    // It will maintain total
    // changes required
    int changes = 0;

    for (i = 0; i < n; i++)
    {
        // Check for the first 1
        if (arr[i] == 1)
        {
            int j;

            // Check for number of
            // consecutive 1's
            for(j = i + 1; j < n; j++)
            {
                if(arr[j] == 0)
                    break;
            }

            // Increment i to the position 
            // of last consecutive 1
            i = j - 1;

            changes++;
        }
    }

    return changes;
}

// Driver code
public static void main (String args[])
{
    int arr[] = { 1, 1, 0, 0, 0,
                     1, 0, 1, 1 };
    int n = arr.length ;

    System.out.println("Minimum operations: " +
                        minimumChanges(arr, n));

}
}

// This code is contributed by ANKITRAI1
```

## 蟒蛇 3

```
# Python 3 program to find
# minimum number of operations
# required to make all array
# elements zero

# Function to find minimum number
# of operations required to make
# all array elements zero
def minimumChanges(arr, n) :

    # It will maintain total
    # changes required
    changes = 0

    i = 0

    while i < n :

        # Check for the first 1
        if arr[i] == 1 :

            j = i + 1

            # Check for number of
            # consecutive 1's
            while j < n:

                if arr[j] == 0 :
                    break

                j += 1

            # Increment i to the position
            # of last consecutive 1
            i = j - 1

            changes += 1

        i += 1

    return changes

# Driver code    
if __name__ == "__main__" :

    arr = [ 1, 1, 0, 0, 0, 1, 0, 1, 1]
    n = len(arr)

    print("Minimum operations:",
           minimumChanges(arr, n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find minimum
// number of operations required
// to make all array elements zero
class GFG
{

// Function to find minimum number
// of operations required to make
// all array elements zero
static int minimumChanges(int[] arr,
                          int n)
{
    int i;

    // It will maintain total
    // changes required
    int changes = 0;

    for (i = 0; i < n; i++)
    {
        // Check for the first 1
        if (arr[i] == 1)
        {
            int j;

            // Check for number of
            // consecutive 1's
            for(j = i + 1; j < n; j++)
            {
                if(arr[j] == 0)
                    break;
            }

            // Increment i to the position
            // of last consecutive 1
            i = j - 1;

            changes++;
        }
    }

    return changes;
}

// Driver code
static void Main()
{
    int[] arr = new int[]{ 1, 1, 0, 0, 0,
                           1, 0, 1, 1 };
    int n = arr.Length ;

    System.Console.WriteLine("Minimum operations: " +
                             minimumChanges(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum number 
// of operations required to make all
// array elements zero

// Function to find minimum number 
// of operations required to make 
// all array elements zero
function minimumChanges($arr, $n)
{
    $i;

    // It will maintain total
    // changes required
    $changes = 0;

    for ($i = 0; $i < $n; $i++)
    {
        // Check for the first 1
        if ($arr[$i] == 1)
        {
            $j;

            // Check for number of
            // consecutive 1's
            for($j = $i + 1; $j < $n; $j++)
            {
                if($arr[$j] == 0)
                    break;
            }

            // Increment i to the position
            // of last consecutive 1
            $i = $j - 1;

            $changes++;
        }
    }

    return $changes;
}

// Driver code
$arr = array( 1, 1, 0, 0, 0,
                 1, 0, 1, 1 );
$n = sizeof($arr);

echo "Minimum operations: " .
    minimumChanges($arr, $n);

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## java 描述语言

```
<script>

// Javascript program to find  minimum number of
// operations required to make all
// array elements zero

// Function to find  minimum number of
// operations required to make all
// array elements zero
function minimumChanges(arr, n)
{
    var i;

    // It will maintain total changes required
    var changes = 0;

    for (i = 0; i < n; i++)
    {  
        // Check for the first 1
        if (arr[i] == 1)
        {  
            var j;

            // Check for number of
            // consecutive 1's
            for(j = i+1; j<n; j++)
            {
                if(arr[j]==0)
                    break;
            }

            // Increment i to the position of
            // last consecutive 1
            i = j-1;

            changes++;
        }
    }

    return changes;
}

// Driver code
var arr = [1, 1, 0, 0, 0, 1, 0, 1, 1 ];
var n = arr.length;

document.write( "Minimum operations: " + minimumChanges(arr, n));

</script>
```

**Output:** 

```
Minimum operations: 3
```

**<u>进场 2:</u>**

1.  正如我们已经知道的，我们必须寻找“1”的连续组/簇，因为在改变该组的第一个“1”之后，连续“1”的其余部分将被自动改变。因此，为了找到连续的“1”，我们可以遍历数组并找到连续的“1”和“0”对的数量，因为它将指示连续的“1”的断点。
2.  在最后一个索引处，我们将检查数组的最后一个元素是“1”还是“0”，因为如果它是“1”，那么可能有一个连续的“1”组在那里，因此我们的循环在迭代结束时找不到断点。

下面是上述方法的实现:

## C++

```
// CPP program to find minimum number of
// operations required to make all
// array elements zero

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// operations required to make all
// array elements zero
int minimumChanges(int arr[], int n)
{
    int i;

    // It will maintain total changes
    // required and return as
    // answer
    int changes = 0;

    // We iterate from 0 to n-1
    // We can't iterate from 0 to n as
    // the arr[i+1] will be
    // out of index
    for (i = 0; i < n-1; i++) {

        // If we there is a consecutive pair of '1' and
        // '0'(in respective order)
        if ((arr[i] == 1) && (arr[i + 1] == 0)) {

            // We increment our returning variable by 1
            changes++;
        }
    }

    // After the loop ends, we check the last element
    // whether it is '1'
    if (arr[n - 1] == 1) {
        changes++;

        // If it is '1', we again increment our
        // returning variable by 1
    }

    return changes;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 0, 0, 0, 1, 0, 1, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Minimum operations: "
         << minimumChanges(arr, n);

    return 0;
}

// This code is contributed by yashbro
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of
// operations required to make all
// array elements zero
class GFG
{

  // Function to find minimum number of
  // operations required to make all
  // array elements zero
  public static int minimumChanges(int arr[], int n)
  {
    int i;

    // It will maintain total changes
    // required and return as
    // answer
    int changes = 0;

    // We iterate from 0 to n-1
    // We can't iterate from 0 to n as
    // the arr[i+1] will be
    // out of index
    for (i = 0; i < n-1; i++) {

      // If we there is a consecutive pair of '1' and
      // '0'(in respective order)
      if ((arr[i] == 1) && (arr[i + 1] == 0)) {

        // We increment our returning variable by 1
        changes++;
      }
    }

    // After the loop ends, we check the last element
    // whether it is '1'
    if (arr[n - 1] == 1) {
      changes++;

      // If it is '1', we again increment our
      // returning variable by 1
    }

    return changes;
  }

  // Driver code

  public static void main(String[] args)
  {
    int arr[] = { 1, 1, 0, 0, 0, 1, 0, 1, 1 };
    int n = arr.length;

    System.out.println( "Minimum operations: "+ minimumChanges(arr, n));

  }
}

//This code is contributed by sravan kumar
```

## 蟒蛇 3

```
# Python 3 program to find
# minimum number of operations
# required to make all array
# elements zero

# Function to find minimum number
# of operations required to make
# all array elements zero

def minimumChanges(arr, n):
    # It will maintain total
    # changes required
    changes = 0

    # We iterate from 0 to n-1
    # We can't iterate from 0 to n as the arr[i+1] will be out of index
    for i in range(n - 1):

        # If we there is a consecutive pair of '1' and '0'(in respective order)
        if arr[i] == 1 and arr[i + 1] == 0:
            # We increment our returning variable by 1
            changes += 1

    # After the loop ends, we check the last element whether it is '1'
    if arr[n - 1] == 1:
        changes += 1  # If it is '1', we again increment our returning variable by 1

    return changes

# Driver code
if __name__ == "__main__":
    arr = [1, 1, 0, 0, 0, 1, 0, 1, 1]
    n = len(arr)

    print("Minimum operations:",
          minimumChanges(arr, n))

# This code is contributed by yashbro
```

## java 描述语言

```
<script>
// Js program to find minimum number of
// operations required to make all
// array elements zero

// Function to find minimum number of
// operations required to make all
// array elements zero
function minimumChanges( arr, n)
{
    let i;

    // It will maintain total changes
    // required and return as
    // answer
    let changes = 0;

    // We iterate from 0 to n-1
    // We can't iterate from 0 to n as
    // the arr[i+1] will be
    // out of index
    for (i = 0; i < n-1; i++) {

        // If we there is a consecutive pair of '1' and
        // '0'(in respective order)
        if ((arr[i] == 1) && (arr[i + 1] == 0)) {

            // We increment our returning variable by 1
            changes++;
        }
    }

    // After the loop ends, we check the last element
    // whether it is '1'
    if (arr[n - 1] == 1) {
        changes++;

        // If it is '1', we again increment our
        // returning variable by 1
    }

    return changes;
}

// Driver code
let arr= [1, 1, 0, 0, 0, 1, 0, 1, 1];
let n =arr.length;
document.write("Minimum operations: "
         , minimumChanges(arr, n));

</script>
```

**Output**

```
Minimum operations: 3
```

**时间复杂度:** O(N)