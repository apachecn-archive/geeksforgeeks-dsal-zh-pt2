# 确定不一致的加权对象

> 原文:[https://www . geeksforgeeks . org/确定权重不一致的对象/](https://www.geeksforgeeks.org/determining-the-inconsistently-weighted-object/)

给定从 1 到 N 的 N 个对象，除了一个事先不知道的对象之外，所有对象的权重都相同。我们还被给予 Q 比较，在每个比较中，相等数量的物体被放置在天平的两侧，我们被告知较重的一侧。
任务是找到权重不一致的对象，或者确定数据是否不够充分。
**示例** :

```
Input : N = 6
Q = 3
1 2 = 5 6
1 2 3 > 4 5 6
3 4 < 5 6
Output : 4
Explanation: Object 4 is lighter than all other objects.

Input : N = 10
Q = 4
1 2 3 4 < 7 8 9 10
1 = 9
2 3 4 > 1 5 10
6 = 2
Output : Insufficient data
```

据说除了一个元素，其余元素的权重相同。所以，如果我们仔细观察，可以说:

1.  在“=”比较中，两边的对象都不是权重不一致的对象。

2.  如果一个物体在一次比较中出现在较重的一侧，而在另一次比较中出现在较轻的一侧，那么它就不是不一致加权的物体。这是因为，如果一个物体出现在较重的一侧，那么它的重量最大，如果它出现在较轻的一侧，那么它的重量最小。因为单个元素不能同时是最大值和最小值。所以，这种情况永远不会发生。

3.  权重不一致的对象必须出现在所有非平衡('>'或')中

我们可以使用以上三个观察来缩小权重不一致的对象的潜在候选。我们将只考虑那些重的或轻的物体；如果只有一个这样的对象，那么它就是所需的对象。如果没有这样的对象，那么我们将考虑所有那些没有出现在任何比较中的对象。如果只有一个这样的对象，那么它就是权重不一致的对象。如果这些情况都没有出现，数据就不足。
以下是上述方法的实现:

## 蟒蛇 3

```
# Python program to determine the
# inconsistently weighted object

# Function to get the difference of two lists
def subt(A, B):
    return list(set(A) - set(B))

# Function to get the intersection of two lists
def intersection(A, B):
    return list(set(A).intersection(set(B)))

# Function to get the intersection of two lists
def union(A, B):
    return list(set(A).union(set(B)))

# Function to find the inconsistently weighted object
def inconsistentlyWeightedObject(N, Q, comparisons):
    # Objects which appear on the heavier side
    heavierObj = [i for i in range(1, N + 1)]

    # Objects which appear on the lighter side
    lighterObj = [i for i in range(1, N + 1)]
    equalObj = [] # Objects which appear in '=' comparisons

    # Objects which don't appear in any comparison
    objectNotCompared = [i for i in range(1, N + 1)]

    for c in comparisons:
        objectNotCompared = subt(objectNotCompared, union(c[0], c[2]))

        if c[1] == '=':
            equalObj = union(equalObj, union(c[0], c[2]))
        elif c[1] == '<':
            # Removing those objects which do
            # not appear on the lighter side
            lighterObj = intersection(lighterObj, c[0])

            # Removing those objects which do
            # not appear on the heavier side
            heavierObj = intersection(heavierObj, c[2])
        else:
            # Removing those objects which do
            # not appear on the lighter side
            lighterObj = intersection(lighterObj, c[2])

            # Removing those objects which do
            # not appear on the heavier side
            heavierObj = intersection(heavierObj, c[0])

    L_iwo = subt(union(heavierObj, lighterObj), equalObj) # Potential candidates

    if len(L_iwo) == 1:
        return L_iwo[0]
    elif not len(L_iwo):
        if len(objectNotCompared) == 1:
            return objectNotCompared[0]
        else:
            return 'Insufficient data'
    else:
        return 'Insufficient data'

# Driver code
N = 6
Q = 3
comparisons = [ [[1, 2], '=', [5, 6]], [[1, 2, 3], '>', [4, 5, 6]],
                                        [[3, 4], '<', [5, 6]] ]
print(inconsistentlyWeightedObject(N, Q, comparisons))
```

**Output:** 

```
4
```