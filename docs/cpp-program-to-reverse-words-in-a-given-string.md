# 给定字符串中倒排单词的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-程序-给定字符串中的反向单词/](https://www.geeksforgeeks.org/cpp-program-to-reverse-words-in-a-given-string/)

示例:让输入字符串为“我非常喜欢这个程序”。该函数应该将字符串更改为“非常像我这样的程序”

![reverse-words](img/369767928f21e752cfabf4c1b77a30e2.png)

**示例**:

> **输入** : s =【极客问答练习代码】
> **输出** : s =【代码练习问答极客】
> 
> **输入** : s =“擅长编码需要大量练习”
> **输出** : s =“擅长编码需要大量练习”

**算法**:

*   最初，逐个反转给定字符串的单个单词，对于上面的示例，反转单个单词后，字符串应该是“i ekil siht margorp yrev hcum”。
*   [从头到尾反转整个字符串](https://www.geeksforgeeks.org/write-a-program-to-reverse-an-array-or-string/)得到想要的输出“非常像我这个程序”在上例中。

下面是上述方法的实现:

## C++

```
// C++ program to reverse a string
#include <bits/stdc++.h>
using namespace std;

// Function to reverse words
void reverseWords(string s)
{    
    // Temporary vector to store all words
    vector<string> tmp;
    string str = "";
    for (int i = 0; i < s.length(); i++) 
    {        
        // Check if we encounter space 
        // push word(str) to vector
        // and make str NULL
        if (s[i] == ' ') 
        {
            tmp.push_back(str);
            str = "";
        }

        // Else add character to 
        // str to form current word
        else
            str += s[i];
    }

    // Last word remaining,add it to vector
    tmp.push_back(str);

    // Now print from last to first in vector
    int i;
    for (i = tmp.size() - 1; i > 0; i--)
        cout << tmp[i] << " ";
    // Last word remaining,print it
    cout << tmp[0] << endl;
}

// Driver Code
int main()
{
    string s = 
    "i like this program very much";
    reverseWords(s);
    return 0;
}
```

**输出:**

```
much very program this like i
```

上面的代码没有处理字符串以空格开头的情况。下面的版本处理这种特殊情况，在中间有多个空格的情况下，不会对反函数进行不必要的调用。感谢 rka143 提供这个版本。

## C++

```
// C++ program to implement
// the above approach
void reverseWords(char* s)
{
  char* word_begin = NULL;

  // temp is for word boundary 
  char* temp = s;

  // STEP 1 of the above algorithm 
  while (*temp) 
  {
    /*This condition is to make sure that 
      the string start with valid character 
      (not space) only*/
    if ((word_begin == NULL) && 
        (*temp != ' ')) 
    {
      word_begin = temp;
    }
    if (word_begin && 
       ((*(temp + 1) == ' ') ||
       (*(temp + 1) == ''))) 
    {
      reverse(word_begin, temp);
      word_begin = NULL;
    }
    temp++;

  // End of while 
  } 

  // STEP 2 of the above algorithm 
  reverse(s, temp - 1);
}

// This code is contributed by rutvik_56.
```

**时间复杂度:** O(n)

**另一种方法:**

我们可以通过以相反的方式拆分和保存字符串来完成上述任务。

下面是上述方法的实现:

## C++

```
// C++ program to reverse a string
// s = input()
#include <bits/stdc++.h>
using namespace std;

// Driver code
int main()
{
    string s[] = {"i", "like", "this", 
                  "program", "very", "much"};

    string ans = "";
    for (int i = 5; i >= 0; i--) 
    {
        ans += s[i] + " ";
    }
    cout << 
    ("Reversed String:") << endl;
    cout << 
    (ans.substr(0, ans.length() - 1)) << 
     endl;

    return 0;
}
// This code is contributed by divyeshrabadiya07.
```

**输出:**

```
Reversed String:
much very program this like i
```

**时间复杂度:** O(n)

**不使用任何额外空间:**
以上任务也可以从中间开始拆分直接对换字符串来完成。由于涉及直接交换，因此占用的空间也更少。

下面是上述方法的实现:

## C++

```
// C++ code to reverse a string
#include <bits/stdc++.h>
using namespace std;

// Reverse the string
string RevString(string s[], int l)
{    
    // Check if number of words is even
    if (l % 2 == 0)
    {        
        // Find the middle word
        int j = l / 2;

        // Starting from the middle
        // start swapping words at 
        // jth position and l-1-j position
        while (j <= l - 1)
        {
            string temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    // Check if number of words is odd
    else
    {        
        // Find the middle word
        int j = (l / 2) + 1;

        // Starting from the middle start
        // swapping the words at jth 
        // position and l-1-j position
        while (j <= l - 1) 
        {
            string temp;
            temp = s[l - j - 1];
            s[l - j - 1] = s[j];
            s[j] = temp;
            j += 1;
        }
    }

    string S = s[0];

    // Return the reversed sentence
    for(int i = 1; i < 9; i++)
    {
        S = S + " " + s[i];
    }
    return S;
}

// Driver code
int main()
{
    string s = "getting good at coding "
               "needs a lot of practice";

    string words[] = {"getting", "good", "at", 
                      "coding", "needs", "a", 
                      "lot", "of", "practice"};

    cout << RevString(words, 9) << endl;
    return 0;
}

// This code is contributed by divyesh072019
```

**输出:**

```
practice of lot a needs coding at good getting
```

**另一个直观的恒空间解**:遍历字符串，镜像字符串中的每个单词，然后，在最后，镜像整个字符串。

下面的 C++代码可以处理多个连续的空格。

## C++

```
// C++ program to implement
// the above approach
#include <algorithm>
#include <iostream>
#include <string>
 using namespace std;

string reverse_words(string s)
{
    int left = 0, i = 0, n = s.size();

    while (s[i] == ' ')
        i++;

    left = i;

    while (i < n)
    {
        if (i + 1 == n || 
            s[i] == ' ')
        {
            int j = i - 1;
            if (i + 1 == n)
                j++;

            while (left < j)
                swap(s[left++], s[j--]);

            left = i + 1;
        }
        if (s[left] == ' ' && i > left)
            left = i;

        i++;
    }
    reverse(s.begin(), s.end());
    return s;
}

// Driver code
int main()
{ 
    string str = 
    "Be a game changer the world is already full of players"; 
    str = reverse_words(str); 
    cout << str;   
    return 0;
}
// This code is contributed by Gatea David
```

**输出:**

```
players of full already is world the changer game a Be
```

更多详情请参考[给定字符串](https://www.geeksforgeeks.org/reverse-words-in-a-given-string/)倒字整篇文章！