# 找出两个数组中和最小的 k 对|集合 2

> 原文:[https://www . geeksforgeeks . org/find-k-双数组最小和对-set-2/](https://www.geeksforgeeks.org/find-k-pairs-with-smallest-sums-in-two-arrays-set-2/)

给定两个按升序排序的数组 arr1[]和 arr2[]，以及一个整数 k。任务是找到具有最小和的 k 对，使得一对中的一个元素属于 arr1[]，另一个元素属于 arr2[]。数组的大小可能不同。假设每个数组中的所有元素都是不同的。
**例:**

```
Input: a1[] = {1, 7, 11}
       a2[] = {2, 4, 6}
       k = 3
Output: [1, 2], [1, 4], [1, 6]
The first 3 pairs are returned 
from the sequence [1, 2], [1, 4], [1, 6], [7, 2],
[7, 4], [11, 2], [7, 6], [11, 4], [11, 6].

Input: a1[] = { 2, 3, 4 }
       a2[] = { 1, 6, 5, 8 }  
       k = 4
Output: [1, 2] [1, 3] [1, 4] [2, 6] 
```

时间复杂度为 O(k*n1)的方法已经讨论过[这里](https://www.geeksforgeeks.org/find-k-pairs-smallest-sums-two-arrays/)。
**高效进场:**因为阵列已经整理好了。下面给出的算法可以用来解决这个问题:

*   其思想是维护两个指针，一个指针指向(a1，a2)中的一对，另一个指向(a2，a1)。每次，比较两对指向的元素的总和，并打印最小的一对。此后，递增指向打印对中大于另一个元素的指针。这有助于获得下一个可能的 k 最小对。
*   一旦指针更新到元素，使其再次指向数组的第一个元素，就将另一个指针更新到下一个值。此更新循环进行。
*   此外，当两个对都指向同一个元素时，更新两个对中的指针以避免额外的对打印。根据规则 1 更新一对指针，并根据规则 1 更新另一对指针。这样做是为了确保考虑所有的排列，并且没有重复的对。

以下是示例 1 的算法工作情况:

> a1[] = {1，7，11}，a2[] = {2，4}，k = 3
> 让成对的指针为 _ 一，_ 二
> _ 一.第一个指向 1，_ 一.第二个指向 2；
> _two.first 指向 2，_two.second 指向 1
> **第一对:**
> 由于 _one 和 _two 指向相同的元素，请打印该对并更新
> 
> *   打印[1，2]
> 
> 然后更新 _one.first 为 1，_one.second 为 4(遵循规则 1)；
> _two .第一分至 2，_two .第二分至 7(与规则 1 相反)。
> 如果两者都遵循规则 1，那么它们都会指向 1 和 4，
> 并且不可能得到所有可能的排列。
> **第二对:**
> 从 a1[_ one . first]+a2[_ one . second]<a1[_ two . second]+a2[_ two . first]开始，打印并更新
> 
> *   打印[1，4]
> 
> 然后 update _one.first 到 1，_one.second 到 2
> 由于 _one.second 再次来到数组的第一个元素，
> 因此 _one.first 指向 7
> 对剩余的 K 对重复上述过程

下面是上述方法的 C++实现:

## C++

```
// C++ program to print the k smallest
// pairs | Set 2
#include <bits/stdc++.h>
using namespace std;

typedef struct _pair {
    int first, second;
} _pair;

// Function to print the K smallest pairs
void printKPairs(int a1[], int a2[],
                 int size1, int size2, int k)
{

    // if k is greater than total pairs
    if (k > (size2 * size1)) {
        cout << "k pairs don't exist\n";
        return;
    }

    // _pair _one keeps track of
    // 'first' in a1 and 'second' in a2
    // in _two, _two.first keeps track of
    // element in the a2[] and _two.second in a1[]
    _pair _one, _two;
    _one.first = _one.second = _two.first = _two.second = 0;

    int cnt = 0;

    // Repeat the above process till
    // all K pairs are printed
    while (cnt < k) {

        // when both the pointers are pointing
        // to the same elements (point 3)
        if (_one.first == _two.second
            && _two.first == _one.second) {
            if (a1[_one.first] < a2[_one.second]) {
                cout << "[" << a1[_one.first]
                     << ", " << a2[_one.second] << "] ";

                // updates according to step 1
                _one.second = (_one.second + 1) % size2;
                if (_one.second == 0) // see point 2
                    _one.first = (_one.first + 1) % size1;

                // updates opposite to step 1
                _two.second = (_two.second + 1) % size2;
                if (_two.second == 0)
                    _two.first = (_two.first + 1) % size2;
            }
            else {
                cout << "[" << a2[_one.second]
                     << ", " << a1[_one.first] << "] ";

                // updates according to rule 1
                _one.first = (_one.first + 1) % size1;
                if (_one.first == 0) // see point 2
                    _one.second = (_one.second + 1) % size2;

                // updates opposite to rule 1
                _two.first = (_two.first + 1) % size2;
                if (_two.first == 0) // see point 2
                    _two.second = (_two.second + 1) % size1;
            }
        }
        // else update as necessary (point 1)
        else if (a1[_one.first] + a2[_one.second]
                 <= a2[_two.first] + a1[_two.second]) {
            if (a1[_one.first] < a2[_one.second]) {
                cout << "[" << a1[_one.first] << ", "
                     << a2[_one.second] << "] ";

                // updating according to rule 1
                _one.second = ((_one.second + 1) % size2);
                if (_one.second == 0) // see point 2
                    _one.first = (_one.first + 1) % size1;
            }
            else {
                cout << "[" << a2[_one.second] << ", "
                     << a1[_one.first] << "] ";

                // updating according to rule 1
                _one.first = ((_one.first + 1) % size1);
                if (_one.first == 0) // see point 2
                    _one.second = (_one.second + 1) % size2;
            }
        }
        else if (a1[_one.first] + a2[_one.second]
                 > a2[_two.first] + a1[_two.second]) {
            if (a2[_two.first] < a1[_two.second]) {
                cout << "[" << a2[_two.first] << ", " << a1[_two.second] << "] ";

                // updating according to rule 1
                _two.first = ((_two.first + 1) % size2);
                if (_two.first == 0) // see point 2
                    _two.second = (_two.second + 1) % size1;
            }
            else {
                cout << "[" << a1[_two.second]
                     << ", " << a2[_two.first] << "] ";

                // updating according to rule 1
                _two.second = ((_two.second + 1) % size1);
                if (_two.second == 0) // see point 2
                    _two.first = (_two.first + 1) % size1;
            }
        }
        cnt++;
    }
}

// Driver Code
int main()
{

    int a1[] = { 2, 3, 4 };
    int a2[] = { 1, 6, 5, 8 };
    int size1 = sizeof(a1) / sizeof(a1[0]);
    int size2 = sizeof(a2) / sizeof(a2[0]);
    int k = 4;
    printKPairs(a1, a2, size1, size2, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print
// the k smallest pairs
// | Set 2
import java.util.*;
class GFG{

static class _pair
{
  int first, second;
};

// Function to print the K
// smallest pairs
static void printKPairs(int a1[], int a2[],
                        int size1, int size2,
                        int k)
{
  // if k is greater than
  // total pairs
  if (k > (size2 * size1))
  {
    System.out.print("k pairs don't exist\n");
    return;
  }

  // _pair _one keeps track of
  // 'first' in a1 and 'second' in a2
  // in _two, _two.first keeps track of
  // element in the a2[] and _two.second
  // in a1[]
  _pair _one = new _pair();
  _pair  _two = new _pair();
  _one.first = _one.second =
  _two.first = _two.second = 0;

  int cnt = 0;

  // Repeat the above process
  // till all K pairs are printed
  while (cnt < k)
  {
    // when both the pointers are
    // pointing to the same elements
    // (point 3)
    if (_one.first == _two.second &&
        _two.first == _one.second)
    {
      if (a1[_one.first] <
          a2[_one.second])
      {
        System.out.print("[" +  a1[_one.first] +
                         ", " +  a2[_one.second] +
                         "] ");

        // updates according to step 1
        _one.second = (_one.second + 1) %
                       size2;

        // see point 2
        if (_one.second == 0)
          _one.first = (_one.first + 1) %
                        size1;

        // updates opposite to step 1
        _two.second = (_two.second + 1) %
                       size2;

        if (_two.second == 0)
          _two.first = (_two.first + 1) %
                        size2;
      }
      else
      {
        System.out.print("[" +  a2[_one.second] +
                         ", " +  a1[_one.first] +
                         "] ");

        // updates according to rule 1
        _one.first = (_one.first + 1) %
                      size1;

        // see point 2
        if (_one.first == 0)
          _one.second = (_one.second + 1) %
                         size2;

        // updates opposite to rule 1
        _two.first = (_two.first + 1) %
                      size2;

        // see point 2
        if (_two.first == 0)

          _two.second = (_two.second + 1) %
                         size1;
      }
    }

    // else update as
    // necessary (point 1)
    else if (a1[_one.first] +
             a2[_one.second] <=
             a2[_two.first] +
             a1[_two.second])
    {
      if (a1[_one.first] <
          a2[_one.second])
      {
        System.out.print("[" +  a1[_one.first] +
                         ", " + a2[_one.second] +
                         "] ");

        // updating according to rule 1
        _one.second = ((_one.second + 1) %
                        size2);

        // see point 2
        if (_one.second == 0)
          _one.first = (_one.first + 1) %
                        size1;
      }
      else
      {
        System.out.print("[" +  a2[_one.second] +
                         ", " + a1[_one.first] +
                         "] ");

        // updating according to rule 1
        _one.first = ((_one.first + 1) %
                       size1);

        // see point 2
        if (_one.first == 0)
          _one.second = (_one.second + 1) %
                         size2;
      }
    }
    else if (a1[_one.first] +
             a2[_one.second] >
             a2[_two.first] +
             a1[_two.second])
    {
      if (a2[_two.first] <
          a1[_two.second])
      {
        System.out.print("[" +  a2[_two.first] +
                         ", " +  a1[_two.second] +
                         "] ");

        // updating according to rule 1
        _two.first = ((_two.first + 1) %
                       size2);

        // see point 2
        if (_two.first == 0)
          _two.second = (_two.second + 1) %
                         size1;
      }
      else {
        System.out.print("[" +  a1[_two.second] +
                         ", " +  a2[_two.first] +
                         "] ");

        // updating according to rule 1
        _two.second = ((_two.second + 1) %
                        size1);

        // see point 2
        if (_two.second == 0)
          _two.first = (_two.first + 1) %
                        size1;
      }
    }
    cnt++;
  }
}

// Driver Code
public static void main(String[] args)
{
  int a1[] = {2, 3, 4};
  int a2[] = {1, 6, 5, 8};
  int size1 = a1.length;
  int size2 = a2.length;
  int k = 4;
  printKPairs(a1, a2,
              size1, size2, k);
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to print the k smallest
# pairs | Set 2

# Function to print the K smallest pairs
def printKPairs(a1, a,size1, size2, k):

    # if k is greater than total pairs
    if (k > (size2 * size1)):
        print("k pairs don't exist\n")
        return

    # _pair _one keeps track of
    # 'first' in a1 and 'second' in a2
    # in _two, _two[0] keeps track of
    # element in the a2and _two[1] in a1[]
    _one, _two = [0, 0], [0, 0]

    cnt = 0

    # Repeat the above process till
    # all K pairs are printed
    while (cnt < k):

        # when both the pointers are pointing
        # to the same elements (po3)
        if (_one[0] == _two[1]
            and _two[0] == _one[1]):
            if (a1[_one[0]] < a2[_one[1]]):
                print("[", a1[_one[0]], ", ",
                        a2[_one[1]],"] ", end=" ")

                # updates according to step 1
                _one[1] = (_one[1] + 1) % size2
                if (_one[1] == 0): #see po2
                    _one[0] = (_one[0] + 1) % size1

                # updates opposite to step 1
                _two[1] = (_two[1] + 1) % size2
                if (_two[1] == 0):
                    _two[0] = (_two[0] + 1) % size2

            else:
                print("[",a2[_one[1]]
                    ,", ",a1[_one[0]],"] ",end=" ")

                # updates according to rule 1
                _one[0] = (_one[0] + 1) % size1
                if (_one[0] == 0): #see po2
                    _one[1] = (_one[1] + 1) % size2

                # updates opposite to rule 1
                _two[0] = (_two[0] + 1) % size2
                if (_two[0] == 0): #see po2
                    _two[1] = (_two[1] + 1) % size1

        # else update as necessary (po1)
        elif (a1[_one[0]] + a2[_one[1]]
                <= a2[_two[0]] + a1[_two[1]]):
            if (a1[_one[0]] < a2[_one[1]]):
                print("[",a1[_one[0]],", ",
                    a2[_one[1]],"] ",end=" ")

                # updating according to rule 1
                _one[1] = ((_one[1] + 1) % size2)
                if (_one[1] == 0): # see po2
                    _one[0] = (_one[0] + 1) % size1
            else:
                print("[",a2[_one[1]],", ",
                    a1[_one[0]],"] ", end=" ")

                # updating according to rule 1
                _one[0] = ((_one[0] + 1) % size1)
                if (_one[0] == 0): # see po2
                    _one[1] = (_one[1] + 1) % size2

        elif (a1[_one[0]] + a2[_one[1]]
                > a2[_two[0]] + a1[_two[1]]):
            if (a2[_two[0]] < a1[_two[1]]):
                print("[",a2[_two[0]],", ",a1[_two[1]],"] ",end=" ")

                # updating according to rule 1
                _two[0] = ((_two[0] + 1) % size2)
                if (_two[0] == 0): #see po2
                    _two[1] = (_two[1] + 1) % size1

            else:
                print("[",a1[_two[1]]
                    ,", ",a2[_two[0]],"] ",end=" ")

                # updating according to rule 1
                _two[1] = ((_two[1] + 1) % size1)
                if (_two[1] == 0): #see po2
                    _two[0] = (_two[0] + 1) % size1

        cnt += 1

# Driver Code
if __name__ == '__main__':

    a1= [2, 3, 4]
    a2= [1, 6, 5, 8]
    size1 = len(a1)
    size2 = len(a2)
    k = 4
    printKPairs(a1, a2, size1, size2, k)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print
// the k smallest pairs
// | Set 2
using System;
class GFG{

public class _pair
{
  public int first,
             second;
};

// Function to print the K
// smallest pairs
static void printKPairs(int []a1, int []a2,
                        int size1, int size2,
                        int k)
{
  // if k is greater than
  // total pairs
  if (k > (size2 * size1))
  {
    Console.Write("k pairs don't exist\n");
    return;
  }

  // _pair _one keeps track of
  // 'first' in a1 and 'second' in a2
  // in _two, _two.first keeps track of
  // element in the a2[] and _two.second
  // in a1[]
  _pair _one = new _pair();
  _pair  _two = new _pair();
  _one.first = _one.second =
  _two.first = _two.second = 0;

  int cnt = 0;

  // Repeat the above process
  // till all K pairs are printed
  while (cnt < k)
  {
    // when both the pointers are
    // pointing to the same elements
    // (point 3)
    if (_one.first == _two.second &&
        _two.first == _one.second)
    {
      if (a1[_one.first] <
          a2[_one.second])
      {
        Console.Write("[" +  a1[_one.first] +
                      ", " +  a2[_one.second] +
                      "] ");

        // updates according to step 1
        _one.second = (_one.second + 1) %
                        size2;

        // see point 2
        if (_one.second == 0)
          _one.first = (_one.first + 1) %
                         size1;

        // updates opposite to step 1
        _two.second = (_two.second + 1) %
                        size2;

        if (_two.second == 0)
          _two.first = (_two.first + 1) %
                         size2;
      }
      else
      {
        Console.Write("[" + a2[_one.second] +
                      ", " + a1[_one.first] +
                      "] ");

        // updates according to rule 1
        _one.first = (_one.first + 1) %
                       size1;

        // see point 2
        if (_one.first == 0)
          _one.second = (_one.second + 1) %
                          size2;

        // updates opposite to rule 1
        _two.first = (_two.first + 1) %
                       size2;

        // see point 2
        if (_two.first == 0)
          _two.second = (_two.second + 1) %
                          size1;
      }
    }

    // else update as
    // necessary (point 1)
    else if (a1[_one.first] +
             a2[_one.second] <=
             a2[_two.first] +
             a1[_two.second])
    {
      if (a1[_one.first] <
          a2[_one.second])
      {
        Console.Write("[" + a1[_one.first] +
                      ", " + a2[_one.second] +
                      "] ");

        // updating according to rule 1
        _one.second = ((_one.second + 1) %
                         size2);

        // see point 2
        if (_one.second == 0)
          _one.first = (_one.first + 1) %
                         size1;
      }
      else
      {
        Console.Write("[" + a2[_one.second] +
                      ", " + a1[_one.first] +
                      "] ");

        // updating according to rule 1
        _one.first = ((_one.first + 1) %
                        size1);

        // see point 2
        if (_one.first == 0)
          _one.second = (_one.second + 1) %
                          size2;
      }
    }
    else if (a1[_one.first] +
             a2[_one.second] >
             a2[_two.first] +
             a1[_two.second])
    {
      if (a2[_two.first] <
          a1[_two.second])
      {
        Console.Write("[" + a2[_two.first] +
                      ", " + a1[_two.second] +
                      "] ");

        // updating according to rule 1
        _two.first = ((_two.first + 1) %
                        size2);

        // see point 2
        if (_two.first == 0)
          _two.second = (_two.second + 1) %
                          size1;
      }
      else {
        Console.Write("[" + a1[_two.second] +
                      ", " + a2[_two.first] +
                      "] ");

        // updating according to rule 1
        _two.second = ((_two.second + 1) %
                         size1);

        // see point 2
        if (_two.second == 0)
          _two.first = (_two.first + 1) %
                         size1;
      }
    }
    cnt++;
  }
}

// Driver Code
public static void Main(String[] args)
{
  int []a1 = {2, 3, 4};
  int []a2 = {1, 6, 5, 8};
  int size1 = a1.Length;
  int size2 = a2.Length;
  int k = 4;
  printKPairs(a1, a2,
              size1,
              size2, k);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program to print
// the k smallest pairs
// | Set 2

// Function to print the K
// smallest pairs
function printKPairs(a1,a2,size1,size2,k)
{
    // if k is greater than
  // total pairs
  if (k > (size2 * size1))
  {
    document.write("k pairs don't exist\n");
    return;
  }

  // _pair _one keeps track of
  // 'first' in a1 and 'second' in a2
  // in _two, _two[0] keeps track of
  // element in the a2[] and _two[1]
  // in a1[]
  let _one = [0,0];
  let  _two = [0,0];

  let cnt = 0;

  // Repeat the above process
  // till all K pairs are printed
  while (cnt < k)
  {
    // when both the pointers are
    // pointing to the same elements
    // (point 3)
    if (_one[0] == _two[1] &&
        _two[0] == _one[1])
    {
      if (a1[_one[0]] <
          a2[_one[1]])
      {
        document.write("[" +  a1[_one[0]] +
                         ", " +  a2[_one[1]] +
                         "] ");

        // updates according to step 1
        _one[1] = (_one[1] + 1) %
                       size2;

        // see point 2
        if (_one[1] == 0)
          _one[0] = (_one[0] + 1) %
                        size1;

        // updates opposite to step 1
        _two[1] = (_two[1] + 1) %
                       size2;

        if (_two[1] == 0)
          _two[0] = (_two[0] + 1) %
                        size2;
      }
      else
      {
        document.write("[" +  a2[_one[1]] +
                         ", " +  a1[_one[0]] +
                         "] ");

        // updates according to rule 1
        _one[0] = (_one[0] + 1) %
                      size1;

        // see point 2
        if (_one[0] == 0)
          _one[1] = (_one[1] + 1) %
                         size2;

        // updates opposite to rule 1
        _two[0] = (_two[0] + 1) %
                      size2;

        // see point 2
        if (_two[0] == 0)

          _two[1] = (_two[1] + 1) %
                         size1;
      }
    }

    // else update as
    // necessary (point 1)
    else if (a1[_one[0]] +
             a2[_one[1]] <=
             a2[_two[0]] +
             a1[_two[1]])
    {
      if (a1[_one[0]] <
          a2[_one[1]])
      {
        document.write("[" +  a1[_one[0]] +
                         ", " + a2[_one[1]] +
                         "] ");

        // updating according to rule 1
        _one[1] = ((_one[1] + 1) %
                        size2);

        // see point 2
        if (_one[1] == 0)
          _one[0] = (_one[0] + 1) %
                        size1;
      }
      else
      {
        document.write("[" +  a2[_one[1]] +
                         ", " + a1[_one[0]] +
                         "] ");

        // updating according to rule 1
        _one[0] = ((_one[0] + 1) %
                       size1);

        // see point 2
        if (_one[0] == 0)
          _one[1] = (_one[1] + 1) %
                         size2;
      }
    }
    else if (a1[_one[0]] +
             a2[_one[1]] >
             a2[_two[0]] +
             a1[_two[1]])
    {
      if (a2[_two[0]] <
          a1[_two[1]])
      {
        document.write("[" +  a2[_two[0]] +
                         ", " +  a1[_two[1]] +
                         "] ");

        // updating according to rule 1
        _two[0] = ((_two[0] + 1) %
                       size2);

        // see point 2
        if (_two[0] == 0)
          _two[1] = (_two[1] + 1) %
                         size1;
      }
      else {
        document.write("[" +  a1[_two[1]] +
                         ", " +  a2[_two[0]] +
                         "] ");

        // updating according to rule 1
        _two[1] = ((_two[1] + 1) %
                        size1);

        // see point 2
        if (_two[1] == 0)
          _two[0] = (_two[0] + 1) %
                        size1;
      }
    }
    cnt++;
  }
}

// Driver Code
let a1=[2, 3, 4];
let a2=[1, 6, 5, 8];
let size1 = a1.length;
let size2 = a2.length;
let k = 4;
printKPairs(a1, a2,
              size1, size2, k);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
[1, 2] [1, 3] [1, 4] [2, 6]
```

**时间复杂度** : O(K)