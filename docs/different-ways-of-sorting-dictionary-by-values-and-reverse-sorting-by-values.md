# 字典按值排序和反向按值排序的不同方式

> 原文:[https://www . geesforgeks . org/不同的排序方式-按值字典和按值反向排序/](https://www.geeksforgeeks.org/different-ways-of-sorting-dictionary-by-values-and-reverse-sorting-by-values/)

**先决条件:**[Python 词典](https://www.geeksforgeeks.org/python-dictionary/)

字典是一个无序的、可变的和有索引的集合。在 [Python](https://www.geeksforgeeks.org/python-programming-language/) 中，字典是用花括号写的，有键和值。我们可以使用键访问字典的值。本文讨论了 10 种不同的按值对 Python 字典进行排序的方法，以及按值进行反向排序的方法。

**<u>将 lambda 函数与 items()和 sorted()</u> :** 使用 [**lambda 函数**](https://www.geeksforgeeks.org/python-lambda-anonymous-functions-filter-map-reduce/) 返回特定项元组的键(0 <sup>第</sup>个元素)，当这些被传递到 [sorted()方法](https://www.geeksforgeeks.org/sorted-function-python/)时，它返回一个排序的序列，然后将该序列[类型铸造到字典](https://www.geeksforgeeks.org/python-type-conversion-of-dictionary-items/)中。 **keys()** 方法返回一个视图对象，该对象显示字典中所有键的[列表。 **sorted()** 用于](https://www.geeksforgeeks.org/python-get-dictionary-keys-as-a-list/)[对字典](https://www.geeksforgeeks.org/python-sort-python-dictionaries-by-key-or-value/)的关键字进行排序。

**示例:**

> **输入:**my _ dict = { 2:‘三’，1:‘二’}
> **输出:** [(2，‘三’)，(1，‘二’)]

下面是使用 lambda 函数的实现:

## 蟒蛇 3

```
# Python program to sort dictionary
# by value using lambda function

# Initialize a dictionary
my_dict = {2: 'three',
           1: 'two'}

# Sort the dictionary
sorted_dict = sorted(
  my_dict.items(),
  key = lambda kv: kv[1])

# Print sorted dictionary
print("Sorted dictionary is :",
      sorted_dict)
```

**Output**

```
Sorted dictionary is : [(2, 'three'), (1, 'two')]

```

**<u>单独使用 items()</u>:**方法 [items()](https://www.geeksforgeeks.org/python-dictionary-items-method/) 单独使用 key 和 value 两个变量按值对字典进行排序。

**示例:**

> **输入:** my_dict = {'c': 3，' a': 1，' d': 4，' b': 2}
> **输出:** [(1，' a ')，(2，' b ')，(3，' c '，(4，' d')]

下面是使用方法项()的实现:

## 蟒蛇 3

```
# Python program to sort dictionary
# by value using item function

# Initialize a dictionary
my_dict = {'c': 3,
           'a': 1,
           'd': 4,
           'b': 2}

# Sorting dictionary
sorted_dict = sorted([(value, key)
 for (key, value) in my_dict.items()])

# Print sorted dictionary
print("Sorted dictionary is :")
print(sorted_dict)
```

**Output**

```
Sorted dictionary is :
[(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd')]

```