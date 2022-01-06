# 统计串联有每个元音的字符串对

> 原文:[https://www . geesforgeks . org/count-对字符串-其串联具有每个元音/](https://www.geeksforgeeks.org/count-pair-of-strings-whose-concatenation-has-every-vowel/)

给定一个由 **N** 弦组成的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】。任务是找到所有可能的字符串对的计数，这样它们的连接至少每个元音都有一次。

**示例:**

> **输入:**str[]= {“oaki tie”、“aemiounau”、“aazuaxvbga”、“eltdgo”}
> **输出:** 4
> **说明:**
> 成对字符串的串联为:
> 1。(“oakitie”、“aazuaxvbga”)，
> 2。(《oakitie》、《aemiounau》)，
> 3。(《aazuaxvbga》、《aemiounau》)，
> 4。(“aemiounau”、“eltdgo”)
> 它们都至少有一次元音。
> 
> **输入:**str[]= {“aaweiolkju”、“oxdfgukmi”}
> **输出:** 1
> **解释:**
> 一对字符串的串联(“aaweiolkju”、“oxdfgukmi”)至少有一次所有的元音字符。

**天真方法:**想法是[从给定数组](https://www.geeksforgeeks.org/print-all-possible-combinations-of-r-elements-in-a-given-array-of-size-n/)生成所有可能的对，并检查两个字符串的每个可能对的连接是否至少有一次所有元音。如果是的话，就把这个算进去。在所有操作后打印计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of all
// concatenated string with each vowel
// at least once
int good_pair(string str[], int N)
{

    int countStr = 0;

    // Concatenating all possible
    // pairs of string
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N; j++) {

            string res = str[i] + str[j];

            // Creating an array which checks,
            // the presence of each vowel
            int vowel[5] = { 0 };

            // Checking for each vowel by
            // traversing the concatenated
            // string
            for (int k = 0;
                 k < res.length(); k++) {

                if (res[k] == 'a')
                    vowel[0] = 1;

                else if (res[k] == 'e')
                    vowel[1] = 1;

                else if (res[k] == 'i')
                    vowel[2] = 1;

                else if (res[k] == 'o')
                    vowel[3] = 1;

                else if (res[k] == 'u')
                    vowel[4] = 1;
            }

            // Checking if all the elements
            // are set in vowel[]
            int temp = 0;
            for (int ind = 0; ind < 5; ind++) {
                if (vowel[ind] == 1)
                    temp++;
            }

            // Check if all vowels are
            // present or not
            if (temp == 5)
                countStr++;
        }
    }

    // Return the final count
    return countStr;
}

// Driver Code
int main()
{
    // Given array of strings
    string arr[] = { "aaweiolkju", "oxdfgujkmi" };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << good_pair(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to return the count of all
// concatenated String with each vowel
// at least once
static int good_pair(String str[], int N)
{

    int countStr = 0;

    // Concatenating all possible
    // pairs of String
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++) 
        {
            String res = str[i] + str[j];

            // Creating an array which checks,
            // the presence of each vowel
            int vowel[] = new int[5];

            // Checking for each vowel by
            // traversing the concatenated
            // String
            for (int k = 0;
                     k < res.length(); k++) 
            {

                if (res.charAt(k) == 'a')
                    vowel[0] = 1;

                else if (res.charAt(k) == 'e')
                    vowel[1] = 1;

                else if (res.charAt(k) == 'i')
                    vowel[2] = 1;

                else if (res.charAt(k) == 'o')
                    vowel[3] = 1;

                else if (res.charAt(k) == 'u')
                    vowel[4] = 1;
            }

            // Checking if all the elements
            // are set in vowel[]
            int temp = 0;
            for (int ind = 0; ind < 5; ind++) 
            {
                if (vowel[ind] == 1)
                    temp++;
            }

            // Check if all vowels are
            // present or not
            if (temp == 5)
                countStr++;
        }
    }

    // Return the final count
    return countStr;
}

// Driver Code
public static void main(String[] args)
{
    // Given array of Strings
    String arr[] = { "aaweiolkju", "oxdfgujkmi" };
    int N = arr.length;

    // Function Call
    System.out.print(good_pair(arr, N));
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return the count of all
# concatenated string with each vowel
# at least once
def good_pair(st, N):

    countStr = 0

    # Concatenating all possible
    # pairs of string
    for i in range(N):
        for j in range(i + 1, N):

            res = st[i] + st[j]

            # Creating an array which checks,
            # the presence of each vowel
            vowel = [0] * 5

            # Checking for each vowel by
            # traversing the concatenated
            # string
            for k in range(len(res)):
                if (res[k] == 'a'):
                    vowel[0] = 1

                elif (res[k] == 'e'):
                    vowel[1] = 1

                elif (res[k] == 'i'):
                    vowel[2] = 1

                elif (res[k] == 'o'):
                    vowel[3] = 1

                elif (res[k] == 'u'):
                    vowel[4] = 1

            # Checking if all the elements
            # are set in vowel[]
            temp = 0
            for ind in range(5):
                if (vowel[ind] == 1):
                    temp += 1

            # Check if all vowels are
            # present or not
            if (temp == 5):
                countStr += 1

    # Return the final count
    return countStr

# Driver Code
if __name__ == "__main__":

    # Given array of strings
    arr = [ "aaweiolkju", "oxdfgujkmi" ]
    N = len(arr)

    # Function call
    print(good_pair(arr, N))

# This code is contributed by jana_sayantan
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to return the count of all
// concatenated String with each vowel
// at least once
static int good_pair(String []str, int N)
{
    int countStr = 0;

    // Concatenating all possible
    // pairs of String
    for(int i = 0; i < N; i++)
    {
        for(int j = i + 1; j < N; j++) 
        {
            String res = str[i] + str[j];

            // Creating an array which checks,
            // the presence of each vowel
            int []vowel = new int[5];

            // Checking for each vowel by
            // traversing the concatenated
            // String
            for(int k = 0;
                    k < res.Length; k++) 
            {
                if (res[k] == 'a')
                    vowel[0] = 1;

                else if (res[k] == 'e')
                    vowel[1] = 1;

                else if (res[k] == 'i')
                    vowel[2] = 1;

                else if (res[k] == 'o')
                    vowel[3] = 1;

                else if (res[k] == 'u')
                    vowel[4] = 1;
            }

            // Checking if all the elements
            // are set in vowel[]
            int temp = 0;
            for(int ind = 0; ind < 5; ind++) 
            {
                if (vowel[ind] == 1)
                    temp++;
            }

            // Check if all vowels are
            // present or not
            if (temp == 5)
                countStr++;
        }
    }

    // Return the readonly count
    return countStr;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array of Strings
    String []arr = { "aaweiolkju", "oxdfgujkmi" };
    int N = arr.Length;

    // Function call
    Console.Write(good_pair(arr, N));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the count of all
// concatenated string with each vowel
// at least once
function good_pair(str, N)
{
    let countStr = 0;

    // Concatenating all possible
    // pairs of string
    for(let i = 0; i < N; i++)
    {
        for(let j = i + 1; j < N; j++) 
        {
            let res = str[i] + str[j];

            // Creating an array which checks,
            // the presence of each vowel
            let vowel = new Array(5);
            vowel.fill(0);

            // Checking for each vowel by
            // traversing the concatenated
            // string
            for(let k = 0; k < res.length; k++) 
            {
                if (res[k] == 'a')
                    vowel[0] = 1;

                else if (res[k] == 'e')
                    vowel[1] = 1;

                else if (res[k] == 'i')
                    vowel[2] = 1;

                else if (res[k] == 'o')
                    vowel[3] = 1;

                else if (res[k] == 'u')
                    vowel[4] = 1;
            }

            // Checking if all the elements
            // are set in vowel[]
            let temp = 0;
            for(let ind = 0; ind < 5; ind++)
            {
                if (vowel[ind] == 1)
                    temp++;
            }

            // Check if all vowels are
            // present or not
            if (temp == 5)
                countStr++;
        }
    }

    // Return the final count
    return countStr;
}

// Driver code

// Given array of strings
let arr = [ "aaweiolkju", "oxdfgujkmi" ];
let N = arr.length;

// Function Call
document.write(good_pair(arr, N));

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N<sup>4</sup>)*
**辅助空间:** *O(N)*

**高效方法:**优化上述方法的思路是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。以下是步骤:

*   创建长度为 32 的哈希**哈希[]** ，所有元素为 **0** 。
*   使用散列法，取一个变量**权重**并用 **2** 的[次幂对该变量执行](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)运算，同时遍历每个字符串，如下所示:

```
for 'a': Weight | 1,  
for 'e': Weight | 2,  
for 'i': Weight | 4,  
for 'o': Weight | 8,  
for 'u': Weight | 16
```

*   **权重**的值是一个哈希值，表示字符串包含的元音组合。
    **例如:**

```
"aeiouau": Weight = 31, as it has all the vowels and 
"oaiie": Weight = 15, as it has all the vowels except 'u'
```

*   将**哈希[]中由**表示的索引权重**增加 1** ，元素是以索引作为哈希值的字符串的计数。
*   因此，散列值的所有对都是索引 **(i，j)** ，这些索引将**按位“或”**作为 **31** 给出，这些对中至少有一次包含所有元音。让这样的字符串的计数为 *countStr* 。因此，计数由下式给出:
    **count str = hash[I]* hash[j]**
*   使用上一步中的公式添加每对的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of all
// concatenated string with each vowel
// at least once
int good_pairs(string str[], int N)
{

    // Creating a hash array with
    // initial value as 0
    int arr[32] = { 0 }, strCount = 0;

    // Traversing through each string
    // and getting hash value for each
    // of them
    for (int i = 0; i < N; i++) {

        // Initializing the weight
        // of each string
        int Weight = 0;

        // Find the hash value for
        // each string
        for (int j = 0;
             j < str[i].size(); j++) {
            switch (str[i][j]) {
            case 'a':
                Weight = Weight | 1;
                break;
            case 'e':
                Weight = Weight | 2;
                break;
            case 'i':
                Weight = Weight | 4;
                break;
            case 'o':
                Weight = Weight | 8;
                break;
            case 'u':
                Weight = Weight | 16;
                break;
            }
        }

        // Increasing the count
        // of the hash value
        arr[Weight]++;
    }

    // Getting all possible pairs
    // of indexes in hash array
    for (int i = 0; i < 32; i++) {

        for (int j = i + 1; j < 32; j++) {

            // Check if the pair which has
            // hash value 31 and
            // multiplying the count of
            // string and add it strCount
            if ((i | j) == 31)
                strCount += arr[i] * arr[j];
        }
    }

    // Corner case, for strings which
    // independently has all the vowels
    strCount += (arr[31] * (arr[31] - 1)) / 2;

    // Return there final count
    return strCount;
}

// Driver Code
int main()
{
    // Given array of strings
    string str[] = { "aaweiolkju", "oxdfgujkmi" };

    int N = sizeof(str) / sizeof(str[0]);

    // Function Call
    cout << good_pairs(str, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
class GFG{

// Function to return the count of all 
// concatenated string with each vowel 
// at least once 
public static int good_pairs(String[] str,
                             int N) 
{ 

    // Creating a hash array with 
    // initial value as 0
    int arr[] = new int[32];
    int strCount = 0; 

    // Traversing through each string 
    // and getting hash value for each 
    // of them 
    for(int i = 0; i < N; i++)
    { 

        // Initializing the weight 
        // of each string 
        int Weight = 0; 

        // Find the hash value for 
        // each string 
        for(int j = 0; 
                j < str[i].length(); j++)
        { 
            switch (str[i].charAt(j))
            {
                case 'a': 
                    Weight = Weight | 1; 
                    break; 
                case 'e': 
                    Weight = Weight | 2; 
                    break; 
                case 'i': 
                    Weight = Weight | 4; 
                    break; 
                case 'o': 
                    Weight = Weight | 8; 
                    break; 
                case 'u': 
                    Weight = Weight | 16; 
                    break; 
            } 
        } 

        // Increasing the count 
        // of the hash value 
        arr[Weight]++; 
    } 

    // Getting all possible pairs 
    // of indexes in hash array 
    for(int i = 0; i < 32; i++)
    { 
        for(int j = i + 1; j < 32; j++)
        { 

            // Check if the pair which has 
            // hash value 31 and 
            // multiplying the count of 
            // string and add it strCount 
            if ((i | j) == 31) 
                strCount += arr[i] * arr[j]; 
        } 
    } 

    // Corner case, for strings which 
    // independently has all the vowels 
    strCount += (arr[31] * (arr[31] - 1)) / 2; 

    // Return there final count 
    return strCount; 
} 

// Driver code
public static void main(String[] args)
{

    // Given array of strings 
    String str[] = { "aaweiolkju", "oxdfgujkmi" }; 

    int N = str.length; 

    // Function call 
    System.out.println(good_pairs(str, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach 

# Function to return the count of all 
# concatenated string with each vowel 
# at least once 
def good_pairs(Str, N):

    # Creating a hash array with 
    # initial value as 0 
    arr = [0 for i in range(32)]
    strCount = 0

    # Traversing through each string 
    # and getting hash value for each 
    # of them 
    for i in range(N):

        # Initializing the weight 
        # of each string 
        Weight = 0

        # Find the hash value for 
        # each string 
        for j in range(len(Str[i])):
            switcher = {
                'a': 1,
                'e': 2,
                'i': 4,
                'o': 8,
                'u': 16,
            }
            Weight = Weight | switcher.get(Str[i][j], 0)

        # Increasing the count 
        # of the hash value 
        arr[Weight] += 1

    # Getting all possible pairs 
    # of indexes in hash array 
    for i in range(32):
        for j in range(i + 1, 32):

            # Check if the pair which has 
            # hash value 31 and 
            # multiplying the count of 
            # string and add it strCount 
            if ((i | j) == 31):
                strCount += arr[i] * arr[j]

    # Corner case, for strings which 
    # independently has all the vowels 
    strCount += int((arr[31] * (arr[31] - 1)) / 2)

    # Return there final count 
    return strCount

# Driver Code 

# Given array of strings 
Str = [ "aaweiolkju", "oxdfgujkmi" ]
N = len(Str)

print(good_pairs(Str, N))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above approach 
using System;
class GFG{

// Function to return the count of all 
// concatenated string with each vowel 
// at least once 
public static int good_pairs(string[] str,
                             int N) 
{ 

    // Creating a hash array with 
    // initial value as 0
    int[] arr = new int[32];
    int strCount = 0; 

    // Traversing through each string 
    // and getting hash value for each 
    // of them 
    for(int i = 0; i < N; i++)
    { 

        // Initializing the weight 
        // of each string 
        int Weight = 0; 

        // Find the hash value for 
        // each string 
        for(int j = 0; 
                j < str[i].Length; j++)
        { 
            switch (str[i][j])
            {
                case 'a': 
                    Weight = Weight | 1; 
                    break; 
                case 'e': 
                    Weight = Weight | 2; 
                    break; 
                case 'i': 
                    Weight = Weight | 4; 
                    break; 
                case 'o': 
                    Weight = Weight | 8; 
                    break; 
                case 'u': 
                    Weight = Weight | 16; 
                    break; 
            } 
        } 

        // Increasing the count 
        // of the hash value 
        arr[Weight]++; 
    } 

    // Getting all possible pairs 
    // of indexes in hash array 
    for(int i = 0; i < 32; i++)
    { 
        for(int j = i + 1; j < 32; j++)
        { 

            // Check if the pair which has 
            // hash value 31 and 
            // multiplying the count of 
            // string and add it strCount 
            if ((i | j) == 31) 
                strCount += arr[i] * arr[j]; 
        } 
    } 

    // Corner case, for strings which 
    // independently has all the vowels 
    strCount += (arr[31] * (arr[31] - 1)) / 2; 

    // Return there final count 
    return strCount; 
} 

// Driver code
public static void Main(string[] args)
{

    // Given array of strings 
    string[] str = { "aaweiolkju", "oxdfgujkmi" }; 

    int N = str.Length; 

    // Function call 
    Console.Write(good_pairs(str, N));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to return the count of all
    // concatenated string with each vowel
    // at least once
    function good_pairs(str, N)
    {

        // Creating a hash array with
        // initial value as 0
        let arr = new Array(32);
        arr.fill(0);
        let strCount = 0;

        // Traversing through each string
        // and getting hash value for each
        // of them
        for(let i = 0; i < N; i++)
        {

            // Initializing the weight
            // of each string
            let Weight = 0;

            // Find the hash value for
            // each string
            for(let j = 0; j < str[i].length; j++)
            {
                switch (str[i][j])
                {
                    case 'a':
                        Weight = Weight | 1;
                        break;
                    case 'e':
                        Weight = Weight | 2;
                        break;
                    case 'i':
                        Weight = Weight | 4;
                        break;
                    case 'o':
                        Weight = Weight | 8;
                        break;
                    case 'u':
                        Weight = Weight | 16;
                        break;
                }
            }

            // Increasing the count
            // of the hash value
            arr[Weight]++;
        }

        // Getting all possible pairs
        // of indexes in hash array
        for(let i = 0; i < 32; i++)
        {
            for(let j = i + 1; j < 32; j++)
            {

                // Check if the pair which has
                // hash value 31 and
                // multiplying the count of
                // string and add it strCount
                if ((i | j) == 31)
                    strCount += arr[i] * arr[j];
            }
        }

        // Corner case, for strings which
        // independently has all the vowels
        strCount += parseInt((arr[31] * (arr[31] - 1)) / 2, 10);

        // Return there final count
        return strCount;
    }

    // Given array of strings
    let str = [ "aaweiolkju", "oxdfgujkmi" ];

    let N = str.length;

    // Function call
    document.write(good_pairs(str, N));

</script>
```

**Output:** 

```
1
```

**时间复杂度:*****O(N<sup>2</sup>)*** ****辅助空间:** *O(32)***