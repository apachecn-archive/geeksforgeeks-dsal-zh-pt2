# 找出每个字符在给定字符串数组中的位置的频率

> 原文:[https://www . geesforgeks . org/find-给定字符串数组中每个字符的位置频率/](https://www.geeksforgeeks.org/find-frequency-of-each-character-with-positions-in-given-array-of-strings/)

给定一个由**N**T6 字符串组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)、 **arr[]** ，其中字符串的每个字符都是小写英文字母，任务是存储和打印每个字符串中每个不同字符的出现。

**示例:**

> **输入:**arr[]= {“geeks forgeeks”、“gfg”}
> **输出:**出现次数:e = [1 2] [1 3] [1 10] [1 11]
> 出现次数:f = [1 6] [2 2]
> 出现次数:g =[1 1 1][1 9][2 1][2 3]
> 出现次数:k = [1 4] [1 12]
> 出现次数:o = [1 7]
> 出现次数:r
> 
> **输入:**arr[]= {“ABC”、“ab”}
> **输出:**出现次数:a = [1 1] [2 1]
> 出现次数:b = [1 2] [2 2]
> 出现次数:c = [1 3]

**方法:**使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)和[矢量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)数据结构可以解决上述问题。按照以下步骤解决问题:

*   初始化一个[映射< char，向量<对< int，int>>>](https://www.geeksforgeeks.org/map-of-vectors-in-c-stl-with-examples/)say**MP**来存储一个字符在向量对中的出现，其中每个对将数组中字符串的索引存储为第一个元素，将字符串中字符的位置存储为第二个元素。
*   使用变量 **i** 遍历向量 **arr** ，并执行以下步骤:
    *   [使用变量 **j** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**arr【I】**的字符，并在每次迭代中推进向量**MP【arr【I】【j】中的对 **{i+1，j+1}** 。**
*   最后，完成以上步骤后，通过遍历地图 **mp** 打印每个字符的出现次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print every occurrence
// of every characters in every string
void printOccurrences(vector<string> arr, int N)
{
    map<char, vector<pair<int, int> > > mp;

    // Iterate over the vector arr[]
    for (int i = 0; i < N; i++) {
        // Traverse the string arr[i]
        for (int j = 0; j < arr[i].length(); j++) {

            // Push the pair of{i+1, j+1}
            // in mp[arr[i][j]]
            mp[arr[i][j]].push_back(
                make_pair(i + 1, j + 1));
        }
    }
    // Print the occurrences of every
    // character
    for (auto it : mp) {
        cout << "Occurrences of: " << it.first << " = ";
        for (int j = 0; j < (it.second).size(); j++) {
            cout << "[" << (it.second)[j].first << " "
                 << (it.second)[j].second << "] ";
        }
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Input
    vector<string> arr = { "geeksforgeeks", "gfg" };
    int N = arr.size();
    // Function call
    printOccurrences(arr, N);
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print every occurrence
# of every characters in every string
def printOccurrences(arr, N):

    mp = [[] for i in range(26)]

    # Iterate over the vector arr[]
    for i in range(N):

        # Traverse the string arr[i]
        for j in range(len(arr[i])):

            # Push the pair of{i+1, j+1}
            # in mp[arr[i][j]]
            mp[ord(arr[i][j]) - ord('a')].append(
                           (i + 1, j + 1))

    # print(mp)

    # Print the occurrences of every
    # character
    for i in range(26):
        if len(mp[i]) == 0:
            continue

        print("Occurrences of:", chr(i +
              ord('a')), "=", end = " ")
        for j in mp[i]:
            print("[" + str(j[0]) + " " +
                        str(j[1]) + "] ", end = "")
        print()

# Driver Code
if __name__ == '__main__':

    # Input
    arr= [ "geeksforgeeks", "gfg" ]
    N  = len(arr)

    # Function call
    printOccurrences(arr, N)

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print every occurrence
// of every characters in every string
function printOccurrences(arr, N) {
  let mp = new Map();

  // Iterate over the vector arr[]
  for (let i = 0; i < N; i++) {
    // Traverse the string arr[i]
    for (let j = 0; j < arr[i].length; j++) {
      // Push the pair of{i+1, j+1}
      // in mp[arr[i][j]]
      if (mp.has(arr[i][j])) {
        let temp = mp.get(arr[i][j]);
        temp.push([i + 1, j + 1]);

        mp.set(arr[i][j], temp);
      } else {
        mp.set(arr[i][j], [[i + 1, j + 1]]);
      }
    }
  }
  // Print the occurrences of every
  // character
  for (let it of new Map([...mp.entries()].sort())) {
    document.write("Occurrences of: " + it[0] + " = ");
    for (let j = 0; j < it[1].length; j++) {
      document.write(" [" + it[1][j][0] + " " + it[1][j][1] + "] ");
    }
    document.write("<br>");
  }
}

// Driver Code

// Input
let arr = ["geeksforgeeks", "gfg"];
let N = arr.length;
// Function call
printOccurrences(arr, N);

</script>
```

**Output**

```
Occurrences of: e = [1 2] [1 3] [1 10] [1 11] 
Occurrences of: f = [1 6] [2 2] 
Occurrences of: g = [1 1] [1 9] [2 1] [2 3] 
Occurrences of: k = [1 4] [1 12] 
Occurrences of: o = [1 7] 
Occurrences of: r = [1 8] 
Occurrences of: s = [1 5] [1 13] 

```

***时间复杂度:** O(N*M)，其中 M 是最长字符串的长度。*
***辅助空间:** O(N*M)*