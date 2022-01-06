# 找到一个字符串中第一个重复的单词

> 原文:[https://www . geesforgeks . org/find-first-repeated-word-string/](https://www.geeksforgeeks.org/find-first-repeated-word-string/)

给定一个字符串，找到字符串中第一个重复的单词
示例:

```
Input : "Ravi had been saying that he had been there"
Output : had

Input : "Ravi had been saying that"
Output : No Repetition

Input : "he had had he"
Output : he
```

问题来源:[https://www . geesforgeks . org/Goldman-Sachs-面试-经验-设定-29-实习/](https://www.geeksforgeeks.org/goldman-sachs-interview-experience-set-29-internship/)

**简单方法:**从后面开始迭代，对于每个新单词，将其存储在无序映射中。对于每个出现不止一次的单词，更新 ans 为该单词，最后反转 ans 并打印出来。

## C++

```
// Cpp program to find first repeated word in a string
#include<bits/stdc++.h>
using namespace std;
void solve(string s)
{
    unordered_map<string,int> mp;  // to store occurences of word
    string t="",ans="";
    // traversing from back makes sure that we get the word which repeats first as ans
    for(int i=s.length()-1;i>=0;i--)
    {
        // if char present , then add that in temp word string t
        if(s[i]!=' ')
        {
            t+=s[i];

        }
        // if space is there then this word t needs to stored in map
        else
        {
            mp[t]++;
            // if that string t has occurred previously then it is a possible ans
            if(mp[t]>1)
               ans=t;
            // set t as empty for again new word  
            t="";

        }
    }

    // first word like "he" needs to be mapped
            mp[t]++;
            if(mp[t]>1)
               ans=t;

    if(ans!="")
    {
        // reverse ans string as it has characters in reverse order
        reverse(ans.begin(),ans.end());
        cout<<ans<<'\n';
    }
    else
    cout<<"No Repetition\n";
}
int main()
{
    string u="Ravi had been saying that he had been there";
    string v="Ravi had been saying that";
    string w="he had had he";
    solve(u);
    solve(v);
    solve(w);

    return 0;

}
```

**Output**

```
had
No Repetition
he
```