# 第一个和最后一个元素相同的子阵列的最大长度

> 原文:[https://www . geesforgeks . org/子数组的最大长度-其第一个和最后一个元素相同/](https://www.geeksforgeeks.org/maximum-length-of-the-sub-array-whose-first-and-last-elements-are-same/)

给定一个只包含小写英文字母的字符数组 **arr[]** ，任务是打印子数组的最大长度，使得子数组的第一个和最后一个元素相同。
**例:**

> **输入:** arr[] = {'g '，' e '，' e '，' k '，' s'}
> **输出:** 2
> {'e '，' e'}是满足给定条件的最大长度子阵。
> **输入:** arr[] = {'a '，' b '，' c '，' d '，' a'}
> **输出:** 5
> {'a '，' b '，' c '，' d '，' a'}为所需子数组

**方法:**对于数组 **ch** 的每个元素，存储它的第一次和最后一次出现。那么以相同元素 **ch** 开始和结束的子阵列的最大长度将是**最后一次出现(ch)–第一次出现(ch) + 1** 。所有元素中这个值的最大值就是要求的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Class that represents a single element
// of the given array and stores it's first
// and the last occurrence in the array
class Element
{
public:
    int firstOcc, lastOcc;
    Element();
    void updateOccurence(int);
};

Element::Element()
{
    firstOcc = lastOcc = -1;
}

// Function to update the occurrence
// of a particular character in the array
void Element::updateOccurence(int index)
{
    // If first occurrence is set to something
    // other than -1 then it doesn't need updating
    if (firstOcc == -1)
        firstOcc = index;

    // Last occurrence will be updated everytime
    // the character appears in the array
    lastOcc = index;
}

// Function to return the maximum length of the
// sub-array that starts and ends with the same element
int maxLenSubArr(string arr, int n)
{
    Element elements[26];

    for (int i = 0; i < n; i++)
    {
        int ch = arr[i] - 'a';

        // Update current character's occurrence
        elements[ch].updateOccurence(i);
    }

    int maxLen = 0;
    for (int i = 0; i < 26; i++)
    {
        // Length of the longest sub-array that starts
        // and ends with the same element
        int len = elements[i].lastOcc -
                  elements[i].firstOcc + 1;
        maxLen = max(maxLen, len);
    }

    // Return the maximum length of
    // the required sub-array
    return maxLen;
}

// Driver Code
int main()
{
    string arr = "geeks";
    int n = arr.length();

    cout << maxLenSubArr(arr, n) << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

// Class that represents a single element
// of the given array and stores it's first
// and the last occurrence in the array
class Element {
    int firstOcc, lastOcc;

    public Element()
    {
        firstOcc = lastOcc = -1;
    }

    // Function to update the occurrence
    // of a particular character in the array
    public void updateOccurrence(int index)
    {

        // If first occurrence is set to something
        // other than -1 then it doesn't need updating
        if (firstOcc == -1)
            firstOcc = index;

        // Last occurrence will be updated everytime
        // the character appears in the array
        lastOcc = index;
    }
}

class GFG {

    // Function to return the maximum length of the
    // sub-array that starts and ends with the same element
    public static int maxLenSubArr(char arr[], int n)
    {

        Element elements[] = new Element[26];
        for (int i = 0; i < n; i++) {
            int ch = arr[i] - 'a';

            // Initialize the current character
            // if haven't already
            if (elements[ch] == null)
                elements[ch] = new Element();

            // Update current character's occurrence
            elements[ch].updateOccurrence(i);
        }

        int maxLen = 0;
        for (int i = 0; i < 26; i++) {

            // If current character appears in the given array
            if (elements[i] != null) {

                // Length of the longest sub-array that starts
                // and ends with the same element
                int len = elements[i].lastOcc - elements[i].firstOcc + 1;
                maxLen = Math.max(maxLen, len);
            }
        }

        // Return the maximum length of
        // the required sub-array
        return maxLen;
    }

    // Driver code
    public static void main(String[] args)
    {
        char arr[] = { 'g', 'e', 'e', 'k', 's' };
        int n = arr.length;

        System.out.print(maxLenSubArr(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Class that represents a single element
# of the given array and stores it's first
# and the last occurrence in the array
class Element:

    def __init__(self):
        self.firstOcc = -1
        self.lastOcc = -1

    # Function to update the occurrence
    # of a particular character in the array
    def updateOccurrence(self, index):

        # If first occurrence is set to
        # something other than -1 then it
        # doesn't need updating
        if self.firstOcc == -1:
            self.firstOcc = index

        # Last occurrence will be updated
        # everytime the character appears
        # in the array
        self.lastOcc = index

# Function to return the maximum length
# of the sub-array that starts and ends
# with the same element
def maxLenSubArr(arr, n):

    elements = [None] * 26
    for i in range(0, n):
        ch = ord(arr[i]) - ord('a')

        # Initialize the current character
        # if haven't already
        if elements[ch] == None:
            elements[ch] = Element()

        # Update current character's occurrence
        elements[ch].updateOccurrence(i)

    maxLen = 0
    for i in range(0, 26):

        # If current character appears in
        # the given array
        if elements[i] != None:

            # Length of the longest sub-array that
            # starts and ends with the same element
            length = (elements[i].lastOcc -
                      elements[i].firstOcc + 1)
            maxLen = max(maxLen, length)

    # Return the maximum length of
    # the required sub-array
    return maxLen

# Driver code
if __name__ == "__main__":

    arr = ['g', 'e', 'e', 'k', 's']
    n = len(arr)

    print(maxLenSubArr(arr, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the above approach
using System;

// Class that represents a single element
// of the given array and stores it's first
// and the last occurrence in the array
public class Element
{

    public int firstOcc, lastOcc;

    public Element()
    {
        firstOcc = lastOcc = -1;
    }

    // Function to update the occurrence
    // of a particular character in the array
    public void updateOccurrence(int index)
    {

        // If first occurrence is set to something
        // other than -1 then it doesn't need updating
        if (firstOcc == -1)
            firstOcc = index;

        // Last occurrence will be updated everytime
        // the character appears in the array
        lastOcc = index;
    }
}

class GFG
{

    // Function to return the maximum
    // length of the sub-array that
    //  starts and ends with the same element
    public static int maxLenSubArr(char []arr, int n)
    {

        Element []elements = new Element[26];
        for (int i = 0; i < n; i++)
        {
            int ch = arr[i] - 'a';

            // Initialize the current character
            // if haven't already
            if (elements[ch] == null)
                elements[ch] = new Element();

            // Update current character's occurrence
            elements[ch].updateOccurrence(i);
        }

        int maxLen = 0;
        for (int i = 0; i < 26; i++)
        {

            // If current character appears
            // in the given array
            if (elements[i] != null)
            {

                // Length of the longest sub-array that starts
                // and ends with the same element
                int len = elements[i].lastOcc - elements[i].firstOcc + 1;
                maxLen = Math.Max(maxLen, len);
            }
        }

        // Return the maximum length of
        // the required sub-array
        return maxLen;
    }

    // Driver code
    public static void Main()
    {
        char []arr = { 'g', 'e', 'e', 'k', 's' };
        int n = arr.Length;

        Console.WriteLine(maxLenSubArr(arr, n));
    }
}

// This code is contributed by Ryuga
```

**Output:** 

```
2
```

**时间复杂度**:O(N)
T3】辅助空间: O(N)