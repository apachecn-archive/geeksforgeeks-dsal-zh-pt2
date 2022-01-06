# 根据给定的规则解密字符串

> 原文:[https://www . geeksforgeeks . org/decrypt-a-string-根据给定规则/](https://www.geeksforgeeks.org/decrypt-a-string-according-to-given-rules/)

给定加密字符串 **str** ，当加密规则如下时，任务是解密给定字符串:

1.  从原始字符串的第一个字符开始。
2.  在每一个奇怪的步骤中，附加下一个字符。
3.  到目前为止，在每一个偶数步中，在加密字符串前添加下一个字符。

> 例如，如果 str = "geeks "那么加密的字符串将是，
> g->ge->ege->egek->segek

**示例:**

> **输入:** str = "segosegekfrek"
> **输出:** geeksforgeeks
> **输入:** str = "vrstie"
> **输出:**力争

**方法:**给定的加密字符串的步骤可以按照相反的顺序进行，以获得原始字符串。获得原始字符串有两个条件:

*   **如果字符串长度为奇数**，在奇数步骤中，在结果字符串中从后面添加字符，否则从前面添加。
*   **如果字符串是偶数长度**，在奇数步从前面添加字符，在偶数步从后面添加字符。

这样得到的结果字符串的反码是加密的原始字符串。
以下是上述方法的实现:

## C++

```
// C++ program to decrypt the original string
#include <bits/stdc++.h>
using namespace std;

// Function to return the original string
// after decryption
string decrypt(string s, int l)
{
    // Stores the decrypted string
    string ans = "";

    // If length is odd
    if (l % 2) {

        // Step counter
        int cnt = 0;

        // Starting and ending index
        int indl = 0, indr = l - 1;

        // Iterate till all characters
        // are decrypted
        while (ans.size() != l) {

            // Even step
            if (cnt % 2 == 0)
                ans += s[indl++];

            // Odd step
            else
                ans += s[indr--];

            cnt++;
        }
    }

    // If length is even
    else {

        // Step counter
        int cnt = 0;

        // Starting and ending index
        int indl = 0, indr = l - 1;
        while (ans.size() != l) {

            // Even step
            if (cnt % 2 == 0)
                ans += s[indr--];

            // Odd step
            else
                ans += s[indl++];

            cnt++;
        }
    }

    // Reverse the decrypted string
    reverse(ans.begin(), ans.end());

    return ans;
}

// Driver Code
int main()
{
    string s = "segosegekfrek";
    int l = s.length();
    cout << decrypt(s, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to decrypt the original string
import java.io.*;
import java.util.*;

class GFG
{

  // Function to return the original string
  // after decryption
  public static String decrypt(String s, int l)
  {

    // Stores the decrypted string
    String ans = "";

    // If length is odd
    if (l % 2 == 1)
    {

      // Step counter
      int cnt = 0;

      // Starting and ending index
      int indl = 0, indr = l - 1;

      // Iterate till all characters
      // are decrypted
      while (ans.length() != l)
      {

        // Even step
        if (cnt % 2 == 0)
          ans += s.charAt(indl++);

        // Odd step
        else
          ans += s.charAt(indr--);
        cnt++;
      }
    }

    // If length is even
    else
    {

      // Step counter
      int cnt = 0;

      // Starting and ending index
      int indl = 0, indr = l - 1;
      while (ans.length() != l)
      {

        // Even step
        if (cnt % 2 == 0)
          ans += s.charAt(indr--);

        // Odd step
        else
          ans += s.charAt(indl++);

        cnt++;
      }
    }

    // Reverse the decrypted string
    StringBuffer sbr = new StringBuffer(ans);
    sbr.reverse();
    return sbr.toString();
  }

  // Driver code
  public static void main (String[] args)
  {
    String s = "segosegekfrek";
    int l = s.length();
    System.out.println(decrypt(s, l));
  }
}

// This Code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program to decrypt
# the original string

# Function to return the
# original string after
# decryption
def decrypt(s, l):

    # Stores the decrypted
    # string
    ans = ""

    # If length is odd
    if (l % 2):

        # Step counter
        cnt = 0

        # Starting and ending
        # index
        indl = 0
        indr = l - 1

        # Iterate till all
        # characters are decrypted
        while (len(ans) != l):

            # Even step
            if (cnt % 2 == 0):
                ans += s[indl]
                indl += 1

            # Odd step
            else:
                ans += s[indr]
                indr -= 1

            cnt += 1

    # If length is even
    else:

        # Step counter
        cnt = 0

        # Starting and ending
        # index
        indl = 0
        indr = l - 1
        while (len(ans) != l):

            # Even step
            if (cnt % 2 == 0):
                ans += s[indr]
                indr -= 1

            # Odd step
            else:
                ans += s[indl]
                indl += 1

            cnt += 1

    # Reverse the decrypted
    # string
    string = list(ans)
    string.reverse()
    ans = ''.join(string)

    return ans

# Driver Code
if __name__ == "__main__":

    s = "segosegekfrek"
    l = len(s)
    print(decrypt(s, l))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to decrypt the original string
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

  // Function to return the original string
  // after decryption
  static string decrypt(string s, int l)
  {

    // Stores the decrypted string
    string ans = "";

    // If length is odd
    if (l % 2 == 1)
    {

      // Step counter
      int cnt = 0;

      // Starting and ending index
      int indl = 0, indr = l - 1;

      // Iterate till all characters
      // are decrypted
      while (ans.Length != l)
      {

        // Even step
        if (cnt % 2 == 0)
          ans += s[indl++];

        // Odd step
        else
          ans += s[indr--];
        cnt++;
      }
    }

    // If length is even
    else
    {

      // Step counter
      int cnt = 0;

      // Starting and ending index
      int indl = 0, indr = l - 1;
      while (ans.Length != l)
      {

        // Even step
        if (cnt % 2 == 0)
          ans += s[indr--];

        // Odd step
        else
          ans += s[indl++];

        cnt++;
      }
    }

    // Reverse the decrypted string
    //Array.Reverse(ans);
    char[] sbr = ans.ToCharArray();
    Array.Reverse(sbr);

    return new string(sbr);
  }

  // Driver code
  public static void Main ()
  {
    string s = "segosegekfrek";
    int l = s.Length;
    Console.Write(decrypt(s, l));
  }
}

// This Code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program to decrypt the original string

    // Function to return the original string
    // after decryption
      function decrypt( s , l) {

        // Stores the decrypted string
        var ans = "";

        // If length is odd
        if (l % 2 == 1) {

            // Step counter
            var cnt = 0;

            // Starting and ending index
            var indl = 0, indr = l - 1;

            // Iterate till all characters
            // are decrypted
            while (ans.length != l) {

                // Even step
                if (cnt % 2 == 0)
                    ans += s.charAt(indl++);

                // Odd step
                else
                    ans += s.charAt(indr--);
                cnt++;
            }
        }

        // If length is even
        else {

            // Step counter
            var cnt = 0;

            // Starting and ending index
            var indl = 0, indr = l - 1;
            while (ans.length != l) {

                // Even step
                if (cnt % 2 == 0)
                    ans += s.charAt(indr--);

                // Odd step
                else
                    ans += s.charAt(indl++);

                cnt++;
            }
        }

        // Reverse the decrypted string

        return ans.split('').reverse().join('');
    }

    // Driver code

        var s = "segosegekfrek";
        var l = s.length;
        document.write(decrypt(s, l));

// This code is contributed by todaysgaurav

</script>
```

**Output**

```
geeksforgeeks
```

下面是 Python 的实现。

## 蟒蛇 3

```
#Python 3 Code for encrypting a string according to given rules
#Function for encryption
def encrypted_string(strg):
    EncryptedString = [strg[0]]
    for t in range(1,len(strg)):
        if (t%2 == 1):
            EncryptedString.append(strg[t]) #At odd position, append the next character
        else:
            EncryptedString.insert(0,strg[t]) #At Even position, prepend the next character
    #print the resultant string
    return (''.join(EncryptedString))

#Python 3 Code for decrypting a string (Answer to the actual question)
def decrypted_string(strg):
    #CHeck the divisibility of length of string by 2
    if (len(strg)%2!=0):
        DecryptedString = [strg[0]]
        for t in range(1,len(strg)):
            DecryptedString.append(strg[-1*t]) #First add the characters from the back
            DecryptedString.append(strg[t]) #from the front
        DecryptedString = DecryptedString[:len(strg)][::-1] #Reverse the final string to get output
        return (''.join(DecryptedString))
    else:
        reverse_strg = strg[::-1] #In case of even length, reverse the given string first
        DecryptedString=[reverse_strg[0]]

        #Looping over the reversed string
        for t in range(1,len(reverse_strg)):
            DecryptedString.append(reverse_strg[-1*t]) #First add the characters from the back
            DecryptedString.append(reverse_strg[t]) #and then from the front
        DecryptedString = DecryptedString[:len(reverse_strg)][::-1]
        return (''.join(DecryptedString))

#Testing the algorithm with Driver Code
if __name__== '__main__':

    print (encrypted_string('geeks'))
    print (encrypted_string('geeksforgeeks'))
    print (encrypted_string('strive'))
    print (encrypted_string('vikaschitturi'))
    print (encrypted_string('padmachitturi'))
    print (encrypted_string('hackerrank'))
    print (encrypted_string('hackerearth'))
    print (encrypted_string('codechef'))
    print (encrypted_string('IamVikas'))
    print (encrypted_string('HelloHowareyou'))
    print (encrypted_string('whatareyoudoing'))

    print(decrypted_string('segek'))
    print(decrypted_string('segosegekfrek'))
    print(decrypted_string('vrstie'))
    print(decrypted_string('iuthskviacitr'))
    print(decrypted_string('iuthadpamcitr'))
    print(decrypted_string('nrechakrak'))
    print(decrypted_string('hreechakrat'))
    print(decrypted_string(encrypted_string('IamVikas')))
    print(decrypted_string(encrypted_string('HelloHowareyou')))
    print(decrypted_string(encrypted_string('whatareyoudoing')))
```

**Output**

```
segek
segosegekfrek
vrstie
iuthskviacitr
iuthadpamcitr
nrechakrak
hreechakrat
ecdcoehf
aimIaVks
oeaoolHelHwryu
gidoeaawhtryuon
geeks
geeksforgeeks
strive
vikaschitturi
padmachitturi
hackerrank
hackerearth
IamVikas
HelloHowareyou
whatareyoudoing
```

**方法:**使用 2 个指针

## 蟒蛇 3

```
def decrypt(encrypted_string):
    i = 0
    n = len(encrypted_string)
    j = n-1
    decrypted_string = ''
    if n % 2 == 1:
        while i < j:
            decrypted_string = encrypted_string[i] + decrypted_string
            decrypted_string = encrypted_string[j] + decrypted_string
            i += 1
            j -= 1
        decrypted_string = encrypted_string[i] + decrypted_string
    else:
        while i < j:
            decrypted_string = encrypted_string[j] + decrypted_string
            decrypted_string = encrypted_string[i] + decrypted_string
            i += 1
            j -= 1
    return decrypted_string

# Testing sample inputs
if __name__ == '__main__':
    print(decrypt('segosegekfrek')) # should print geeksforgeeks
    print(decrypt('vrstie')) # should print strive
    print(decrypt('segek')) # should print geeks
```

**Output**

```
geeksforgeeks
strive
geeks
```