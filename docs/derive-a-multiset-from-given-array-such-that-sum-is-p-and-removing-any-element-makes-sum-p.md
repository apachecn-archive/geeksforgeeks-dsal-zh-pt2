# 从给定数组中导出一个多集，这样和就是> P，去掉任何元素就是和< P

> 原文:[https://www . geeksforgeeks . org/derivate-a-multist-from-给定数组-这样-sum-is-p-and-remove-any-element-make-sum-p/](https://www.geeksforgeeks.org/derive-a-multiset-from-given-array-such-that-sum-is-p-and-removing-any-element-makes-sum-p/)

给定一个由 **N** 个元素组成的数组**arr【】**，任务是从给定的数组中导出一个**多集**,该多集在可能的重复中具有这些数字，这样多集的和就严格大于给定的数字 **P** ，如果任何一个元素被移除，那么和就严格小于 **P** 。打印给定数组的对应元素被导出到多集的次数。如果不能导出这样的多集，打印 **-1** 。

**示例:**

> **输入:**arr[]=【1，5】，P = 4
> **输出:**【0，1】
> **解释:**
> 这里，如果数字 1 取 0 次，5 取 1 次，则 MultiSet 变成:【5】
> 因此，sum = 5 ( > P)，去掉 5 使 sum = 0 ( < P)。因此，所需的 MultiSet 是[5]。
> 因此，分别取 1 和 5 的次数，输出为[0，1]。
> 
> **输入:** arr[] = [1，5]，P = 10
> **输出:** -1
> **解释:**
> 如果我们把一个多集作为【1，5，5】，和将是> P，但是去掉 1 不会使和< P。因此，在这种情况下不能导出这样的多集。

**方法:**
对上述问题的主要观察是，如果 P **不可被 arr[]数组中的任何元素**分割， 然后我们取该元素的所有倍数，使得和严格大于 P。但是如果数组中没有这样的元素，并且多集是可能的，那么我们以降序对数组进行排序，并且取每个元素的倍数小于 **P % arr[i]** 并继续更新 P。如果每次更新的 P 都被 arr[i+1]整除直到 N.

以下是上述方法的实现:

## 蟒蛇 3

```
# Python implementation to Derive a
# MultiSet from given Array such that
# sum is > P and removing any
# element makes sum < P

# Function to derive the multiset
def Multiset (n, p, arr):

    c = 0

    for j in arr:

        # Check if p is indivisible
        # by any element in arr
        if (p % j != 0):
            c = j
            break

    # Check if there is no element in
    # arr which cannot divide p    
    if (c == 0):

        d = sorted(arr)

        # Sort arr in descending order
        d = d[::-1]         
        coun = 0
        pri = [0] * n

        # Assigning multiples of each element
        while (coun != n and p % d[coun] == 0): 

            b = arr.index(d[coun])
            pri[b] = ((p//d[coun]) - 1)
            p = p - (d[coun]*((p//d[coun]) - 1))
            coun += 1

        # Check if there is no case
        # of getting sum > p
        if (coun == n):
            return ("NO")

        elif (p % d[coun] != 0):
            y = (p//d[coun]) + 1
            k = arr.index(d[coun])

            pri[k] = y
            s = ""

            # Multi set
            for j in pri:                     
                s = s + str(j) + " "
            return (s)

    else:
        k = p//c
        b = c * (k + 1)
        m = [0] * n
        q = arr.index(c)
        m[q] = b//c
        s = ""
        for j in m:
            s = s + str(j) + " "
        return (s)

# Driver code
N, P = 2, 4
arr = [1, 5]
print (Multiset(N, P, arr))
```

**Output**

```
0 1 

```

**时间复杂度:**O(N)
T3】辅助空间: O(1)