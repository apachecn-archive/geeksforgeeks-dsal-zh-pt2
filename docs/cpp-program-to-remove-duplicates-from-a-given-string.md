# 从给定字符串中删除重复项的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-从给定字符串中删除重复项的程序/](https://www.geeksforgeeks.org/cpp-program-to-remove-duplicates-from-a-given-string/)

给定一个字符串 **S** ，任务是删除给定字符串中的所有重复项。
以下是删除字符串中重复项的不同方法。

**方法 1(简单)**

## C++

```
// CPP program to remove duplicate character
// from character array and print in sorted
// order
#include <bits/stdc++.h>
using namespace std;

char *removeDuplicate(char str[], int n)
{
   // Used as index in the modified string
   int index = 0;   

   // Traverse through all characters
   for (int i=0; i<n; i++) {

     // Check if str[i] is present before it  
     int j;  
     for (j=0; j<i; j++) 
        if (str[i] == str[j])
           break;

     // If not present, then add it to
     // result.
     if (j == i)
        str[index++] = str[i];
   }

   return str;
}

// Driver code
int main()
{
   char str[]= "geeksforgeeks";
   int n = sizeof(str) / sizeof(str[0]);
   cout << removeDuplicate(str, n);
   return 0;
}
```

**输出:**

```
geksfor
```

**时间复杂度:**O(n * n)
T3】辅助空间: O(1)
保持元素顺序与输入相同。

**方法 2(使用 BST)**
使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，实现二叉查找树的自平衡。

## C++

```
// CPP program to remove duplicate character
// from character array and print in sorted
// order
#include <bits/stdc++.h>
using namespace std;

char *removeDuplicate(char str[], int n)
{
    // create a set using string characters
    // excluding '�'
    set<char>s (str, str+n-1);

    // print content of the set
    int i = 0;
    for (auto x : s)
       str[i++] = x;
    str[i] = '�';

    return str;
}

// Driver code
int main()
{
   char str[]= "geeksforgeeks";
   int n = sizeof(str) / sizeof(str[0]);
   cout << removeDuplicate(str, n);
   return 0;
}
```

**输出:**

```
  efgkors
```

**时间复杂度**:O(n Log n)
T3】辅助空间 : O(n)

感谢阿尼维什·蒂瓦里 提出这种方法。

它不会保持元素的顺序与输入相同，而是按排序顺序打印它们。

**方法 3(使用排序)**
**算法:**

```
  1) Sort the elements.
  2) Now in a loop, remove duplicates by comparing the 
      current character with previous character.
  3)  Remove extra characters at the end of the resultant string.
```

**示例:**

```
Input string:  geeksforgeeks
1) Sort the characters
   eeeefggkkorss
2) Remove duplicates
    efgkorskkorss
3) Remove extra characters
     efgkors
```

请注意，此方法不保持输入字符串的原始顺序。例如，如果我们要删除 geeksforgeeks 的重复项，并保持字符的顺序不变，那么输出应该是 geksfor，但是上面的函数返回 efgkos。我们可以通过存储原始订单来修改此方法。

**实施:**

## C++

```
// C++ program to remove duplicates, the order of
// characters is not maintained in this program
#include<bits/stdc++.h>
using namespace std;

/* Function to remove duplicates in a sorted array */
char *removeDupsSorted(char *str)
{
    int res_ind = 1, ip_ind = 1;

    /* In place removal of duplicate characters*/
    while (*(str + ip_ind))
    {
        if (*(str + ip_ind) != *(str + ip_ind - 1))
        {
            *(str + res_ind) = *(str + ip_ind);
            res_ind++;
        }
        ip_ind++;
    }

    /* After above step string is efgkorskkorss.
       Removing extra kkorss after string*/
    *(str + res_ind) = '�';

    return str;
}

/* Function removes duplicate characters from the string
   This function work in-place and fills null characters
   in the extra space left */
char *removeDups(char *str)
{
   int n = strlen(str);

   // Sort the character array
   sort(str, str+n);

   // Remove duplicates from sorted
   return removeDupsSorted(str);
}

/* Driver program to test removeDups */
int main()
{
  char str[] = "geeksforgeeks";
  cout << removeDups(str);
  return 0;
}
```

**输出:**

```
efgkors
```

**时间复杂度:** O(n log n)如果我们用一些 n log n 排序算法来代替快速排序。

**辅助空间:** O(1)

**方法 4(使用散列法)**

**算法:**

```
1: Initialize:
    str  =  "test string" /* input string */
    ip_ind =  0          /* index to  keep track of location of next
                             character in input string */
    res_ind  =  0         /* index to  keep track of location of
                            next character in the resultant string */
    bin_hash[0..255] = {0,0, ….} /* Binary hash to see if character is 
                                        already processed or not */
2: Do following for each character *(str + ip_ind) in input string:
              (a) if bin_hash is not set for *(str + ip_ind) then
                   // if program sees the character *(str + ip_ind) first time
                         (i)  Set bin_hash for *(str + ip_ind)
                         (ii)  Move *(str  + ip_ind) to the resultant string.
                              This is done in-place.
                         (iii) res_ind++
              (b) ip_ind++
  /* String obtained after this step is "te stringing" */
3: Remove extra characters at the end of the resultant string.
  /*  String obtained after this step is "te string" */
```

**实施:**

## C++

```
#include <bits/stdc++.h>
using namespace std; 
# define NO_OF_CHARS 256 
# define bool int 

/* Function removes duplicate characters from the string 
This function work in-place and fills null characters 
in the extra space left */
char *removeDups(char str[]) 
{ 
    bool bin_hash[NO_OF_CHARS] = {0}; 
    int ip_ind = 0, res_ind = 0; 
    char temp; 

    /* In place removal of duplicate characters*/
    while (*(str + ip_ind)) 
    { 
        temp = *(str + ip_ind); 
        if (bin_hash[temp] == 0) 
        { 
            bin_hash[temp] = 1; 
            *(str + res_ind) = *(str + ip_ind); 
            res_ind++; 
        } 
        ip_ind++; 
    } 

    /* After above step string is stringiittg. 
        Removing extra iittg after string*/
    *(str+res_ind) = '�'; 

    return str; 
} 

/* Driver code */
int main() 
{ 
    char str[] = "geeksforgeeks"; 
    cout << removeDups(str); 
    return 0; 
} 

// This code is contributed by rathbhupendra
```

**输出:**

```
geksfor
```

**时间复杂度:** O(n)

**要点:**

*   方法 2 没有将字符保持为原始字符串，但是方法 4 保持了。
*   假设输入字符串中可能的字符数是 256。应该相应地改变字符数。
*   calloc()代替 malloc()用于计数数组(count)的内存分配，以将分配的内存初始化为“”。也可以使用 malloc()后跟 memset()。
*   如果给定数组中整数的范围，上述算法也适用于整数数组输入。一个示例问题是，假设输入数组只包含 1000 到 1100 之间的整数，则找出输入数组中出现的最大数字

**方法 5** (使用**索引 Of()** 方法):
T5】先决条件:T7】Java**索引 Of()** 方法

## C++

```
// C++ program to create a unique string
#include <bits/stdc++.h>
using namespace std;

// Function to make the string unique
string unique(string s)
{
    string str;
    int len = s.length();

    // loop to traverse the string and
    // check for repeating chars using
    // IndexOf() method in Java
    for(int i = 0; i < len; i++)
    {

        // character at i'th index of s
        char c = s[i];

        // If c is present in str, it returns
        // the index of c, else it returns npos
        auto found = str.find(c);
        if (found == std::string::npos) 
        {

            // Adding c to str if npos is returned
            str += c;
        }
    }
    return str;
}

// Driver code
int main()
{

    // Input string with repeating chars
    string s = "geeksforgeeks";

    cout << unique(s) << endl;
}

// This code is contributed by nirajgusain5
```

**输出:**

```
geksfor
```

感谢 [**debjitdbb**](https://auth.geeksforgeeks.org/user/debjitdbb/articles) 提出这个方法。

**方法 6** (使用**无序 _ 映射 STL** 方法):
**先决条件:** [无序 _ 映射 STL C++方法](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)

## C++

```
// C++ program to create a unique string using unordered_map

/* access time in unordered_map on is O(1) generally if no collisions occur 
and therefore it helps us check if an element exists in a string in O(1) 
time complexity with constant space. */

#include <bits/stdc++.h> 
using namespace std; 
char* removeDuplicates(char *s,int n){
  unordered_map<char,int> exists;
  int index = 0; 
  for(int i=0;i<n;i++){
    if(exists[s[i]]==0)
    {
      s[index++] = s[i];
      exists[s[i]]++;
    }
  }
  return s;
}

//driver code
int main(){
  char s[] = "geeksforgeeks";
  int n = sizeof(s)/sizeof(s[0]);
  cout<<removeDuplicates(s,n)<<endl;
  return 0;
}
```

**输出:**

```
geksfor
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
谢谢，**艾伦·詹姆斯·维诺伊**提出这个方法。

更多详情请参考[从给定字符串](https://www.geeksforgeeks.org/remove-duplicates-from-a-given-string/)中删除重复项的完整文章！