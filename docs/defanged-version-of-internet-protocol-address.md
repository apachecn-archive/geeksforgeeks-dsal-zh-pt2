# 互联网协议地址的默认版本

> 原文:[https://www . geesforgeks . org/default-version-of-internet-protocol-address/](https://www.geeksforgeeks.org/defanged-version-of-internet-protocol-address/)

给定一个有效的(IPv4) [互联网协议地址](https://www.geeksforgeeks.org/introduction-of-classful-ip-addressing/) **S** ，任务是找到该 IP 地址的默认版本。
被替换为“[。]".
**示例:**

> **输入:**S = " 1 . 1 . 1 . 1 "
> T3】输出: 1[。]1[.]1[.]1
> **输入:** S = "255.100.50.0"
> **输出:** 255[。]100[.]50[.]0

**方法:**想法是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并将字符串的每个字符追加到最终答案字符串中，除非当前字符为“”，然后追加**”【。】**进入最终答案串。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// defanged version of the IP address

#include <bits/stdc++.h>

using namespace std;

// Function to generate a
// defanged version of IP address.
string GeberateDefangIP(string str)
{
    string defangIP = "";

    // Loop to iterate over the
    // characters of the string
    for (char c : str)
        (c == '.') ? defangIP += "[.]" :
                     defangIP += c;
    return defangIP;
}

// Driven Code
int main()
{
    string str = "255.100.50.0";
    cout << GeberateDefangIP(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// defanged version of the IP address
class GFG{

// Function to generate a defanged 
// version of IP address.
static String GeberateDefangIP(String str)
{
    String defangIP = "";

    // Loop to iterate over the
    // characters of the string
    for(int i = 0; i < str.length(); i++)
    {
       char c = str.charAt(i);
       if(c == '.')
       {
           defangIP += "[.]";
       }
       else
       {
           defangIP += c;
       }
    }
    return defangIP;
}

// Driver Code
public static void main(String[] args)
{
    String str = "255.100.50.0";

    System.out.println(GeberateDefangIP(str));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation to find the
# defanged version of the IP address

# Function to generate a
# defanged version of IP address.
def GeberateDefangIP(str):

    defangIP = "";

    # Loop to iterate over the
    # characters of the string
    for c in str:
        if(c == '.'):
            defangIP += "[.]"
        else:
             defangIP += c;
    return defangIP;

# Driver Code
str = "255.100.50.0";
print(GeberateDefangIP(str));

# This code is contributed by Nidhi_biet
```

## C#

```
// C# implementation to find the
// defanged version of the IP address
using System;
class GFG{

// Function to generate a defanged
// version of IP address.
static String GeberateDefangIP(string str)
{
    string defangIP = "";

    // Loop to iterate over the
    // characters of the string
    for(int i = 0; i < str.Length; i++)
    {
    char c = str[i];
    if(c == '.')
    {
        defangIP += "[.]";
    }
    else
    {
        defangIP += c;
    }
    }
    return defangIP;
}

// Driver Code
public static void Main()
{
    string str = "255.100.50.0";

    Console.Write(GeberateDefangIP(str));
}
}

// This code is contributed by Code_mech
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// defanged version of the IP address

// Function to generate a
// defanged version of IP address.
function GeberateDefangIP(str)
{
    var defangIP = "";

    // Loop to iterate over the
    // characters of the string
    str.split('').forEach(function(letter) {
        (letter == '.') ? defangIP += "[.]" :
                     defangIP += letter; })

    return defangIP;
}

// Driven Code
var str = "255.100.50.0";
document.write( GeberateDefangIP(str));

</script>
```

**Output:** 

```
255[.]100[.]50[.]0
```