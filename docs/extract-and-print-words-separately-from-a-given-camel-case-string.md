# 从给定的 Camel Case 字符串中分别提取和打印单词

> 原文:[https://www . geesforgeks . org/提取和打印单词-与给定的骆驼大小写字符串分开/](https://www.geeksforgeeks.org/extract-and-print-words-separately-from-a-given-camel-case-string/)

给定一个[**格式的字符串，我们需要提取字符串中存在的所有单词。**](https://en.wikipedia.org/wiki/Camel_case)

> **CamelCase 是一个或多个单词的序列，具有以下属性:**
> 
> 1.  **它是一个或多个由英文字母组成的单词的串联。**
> 2.  **第一个单词中的所有字母都是小写的。**
> 3.  **对于后面的每个单词，第一个字母是大写的，其余的字母是小写的。**

****示例:****

> ****输入:**str = " Geeks forgeeks "
> T3】输出:T5】极客
> 为
> 极客**
> 
>  ****输入:**str = " acomputerscienceportalforgeks "
> **输出:**
> A
> 计算机
> 科学
> 门户
> 为
> 极客**

****方法:**
一个简单的方法是遍历数组，通过查看每个单词的第一个字符来提取每个单词，因为它总是大写的。将所有提取的单词存储在一个新数组中并打印出来。**

## **C++**

```
// C++ program to print words
// from CamelCase String

#include <cstring>
#include <iostream>
using namespace std;

// Function to extract a word
char* mystrtok(char* str)
{
    static char* input = NULL;
    if (str != NULL) {
        input = str;
    }

    // Base case
    if (input == NULL)
        return NULL;

    // Array for storing tokens
    // +1 is for '\0'
    char* output = new char[strlen(input + 1)];

    int i = 0;

    // Storing the upper case character
    output[i] = input[i];

    i++;

    // Generating Tokens
    for (; input[i] != '\0'; i++) {
        if (!isupper(input[i]))
            output[i] = input[i];
        else {
            output[i] = '\0';
            input = input + i;
            return output;
        }
    }

    output[i] = '\0';
    input = NULL;
    return output;
}

// Function to extract words
void extractWords(char* s)
{

    // Extract 1st word and print it
    char* ptr = mystrtok(s);
    cout << ptr << endl;

    // Extract the remaining words
    while (ptr != NULL) {
        ptr = mystrtok(NULL);
        cout << ptr << endl;
    }
}

// Driver code
int main()
{

    char s[] = "GeeksForGeeks";
    extractWords(s);

    return 0;
}
```

****Output:**

```
Geeks
For
Geeks

```** 

****时间复杂度:**O(N)
T3】空间复杂度: O(N)，因为我们需要一个新的数组来存储输出。**