# 将编码的基本 64 字符串解码为 ASCII 字符串

> 原文:[https://www . geesforgeks . org/decode-encoded-base-64-string-ascii-string/](https://www.geeksforgeeks.org/decode-encoded-base-64-string-ascii-string/)

先决条件:[什么是 base64 编码以及我们为什么将字符串编码为 base64 格式](https://www.geeksforgeeks.org/encode-ascii-string-base-64-format/)
Base64 编码在通过网络传输位之前在发送节点执行，接收节点将该编码数据解码回原始 ASCII 字符串。
Base64 字符集为

```
// 64 characters
char_set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz0123456789+/" 
```

**例:**

```
Input : TUVO04= // (Encoded into base64 format)
Output : MENON  //  (Decoded back to ASCII string)

Input : Z2Vla3Nmb3JnZWVrcw==
Output : geeksforgeeks
```

**进场:**

1.  这里，编码字符串中的每个字符都被认为是由 6 位组成的。我们将一次从编码字符串中提取 4 个字符，即 4 * 6 = 24 位。对于每 4 个字符的编码字符串，我们将产生 3 个字符的原始字符串，每个 8 位，即 3 * 8 = 24 位。
2.  在 **char_set** 中找到它们各自的位置，并通过使用“|”OR 运算符存储位并将(LEFT–SHIFT)乘以 6 为另一个 6 位腾出空间，将其存储在变量 **(num)** 中。
    **注:**我们在编码器中使用了“=”来代替 2 个丢失的位，所以在解码器中我们必须颠倒这个过程。每当我们遇到“=”时，我们必须通过使用(右移)2 来删除**数**的 2 位。

3.  在我们将所有的位存储在 **num** 中之后，我们将通过使用带有 255(111111111)的&运算符以 8 为一组检索它们，这将存储 num 中的 8 位，这将是我们从 ASCII 字符串中得到的原始字符。

## C++

```
// C++ Program to decode a base64
// Encoded string back to ASCII string
#include <bits/stdc++.h>
using namespace std;
#define SIZE 100

/* char_set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz0123456789+/" */
char* base64Decoder(char encoded[], int len_str)
{
    char* decoded_string;

    decoded_string = (char*)malloc(sizeof(char) * SIZE);

    int i, j, k = 0;

    // stores the bitstream.
    int num = 0;

    // count_bits stores current
    // number of bits in num.
    int count_bits = 0;

    // selects 4 characters from
    // encoded string at a time.
    // find the position of each encoded
    // character in char_set and stores in num.
    for (i = 0; i < len_str; i += 4)
    {
        num = 0, count_bits = 0;
        for (j = 0; j < 4; j++)
        {

            // make space for 6 bits.
            if (encoded[i + j] != '=')
            {
                num = num << 6;
                count_bits += 6;
            }

            /* Finding the position of each encoded
            character in char_set
            and storing in "num", use OR
            '|' operator to store bits.*/

            // encoded[i + j] = 'E', 'E' - 'A' = 5
            // 'E' has 5th position in char_set.
            if (encoded[i + j] >= 'A' && encoded[i + j] <= 'Z')
                num = num | (encoded[i + j] - 'A');

            // encoded[i + j] = 'e', 'e' - 'a' = 5,
            // 5 + 26 = 31, 'e' has 31st position in char_set.
            else if (encoded[i + j] >= 'a' && encoded[i + j] <= 'z')
                num = num | (encoded[i + j] - 'a' + 26);

            // encoded[i + j] = '8', '8' - '0' = 8
            // 8 + 52 = 60, '8' has 60th position in char_set.
            else if (encoded[i + j] >= '0' && encoded[i + j] <= '9')
                num = num | (encoded[i + j] - '0' + 52);

            // '+' occurs in 62nd position in char_set.
            else if (encoded[i + j] == '+')
                num = num | 62;

            // '/' occurs in 63rd position in char_set.
            else if (encoded[i + j] == '/')
                num = num | 63;

            // ( str[i + j] == '=' ) remove 2 bits
            // to delete appended bits during encoding.
            else {
                num = num >> 2;
                count_bits -= 2;
            }
        }

        while (count_bits != 0)
        {
            count_bits -= 8;

            // 255 in binary is 11111111
            decoded_string[k++] = (num >> count_bits) & 255;
        }
    }

    // place NULL character to mark end of string.
    decoded_string[k] = '\0';

    return decoded_string;
}

// Driver code
int main()
{
    char encoded_string[] = "TUVOT04=";
    int len_str = sizeof(encoded_string) / sizeof(encoded_string[0]);

    // Do not count last NULL character.
    len_str -= 1;

    cout <<"Encoded string : " <<
            encoded_string << endl;
    cout <<"Decoded string : " <<
            base64Decoder(encoded_string, len_str) << endl;

    return 0;
}

// This code is contributed by
// shubhamsingh10
```

## C

```
// C Program to decode a base64
// Encoded string back to ASCII string

#include <stdio.h>
#include <stdlib.h>
#define SIZE 100

/* char_set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz0123456789+/" */

char* base64Decoder(char encoded[], int len_str)
{
    char* decoded_string;

    decoded_string = (char*)malloc(sizeof(char) * SIZE);

    int i, j, k = 0;

    // stores the bitstream.
    int num = 0;

    // count_bits stores current
    // number of bits in num.
    int count_bits = 0;

    // selects 4 characters from
    // encoded string at a time.
    // find the position of each encoded
    // character in char_set and stores in num.
    for (i = 0; i < len_str; i += 4) {
        num = 0, count_bits = 0;
        for (j = 0; j < 4; j++) {
            // make space for 6 bits.
            if (encoded[i + j] != '=') {
                num = num << 6;
                count_bits += 6;
            }

            /* Finding the position of each encoded
            character in char_set
            and storing in "num", use OR
            '|' operator to store bits.*/

            // encoded[i + j] = 'E', 'E' - 'A' = 5
            // 'E' has 5th position in char_set.
            if (encoded[i + j] >= 'A' && encoded[i + j] <= 'Z')
                num = num | (encoded[i + j] - 'A');

            // encoded[i + j] = 'e', 'e' - 'a' = 5,
            // 5 + 26 = 31, 'e' has 31st position in char_set.
            else if (encoded[i + j] >= 'a' && encoded[i + j] <= 'z')
                num = num | (encoded[i + j] - 'a' + 26);

            // encoded[i + j] = '8', '8' - '0' = 8
            // 8 + 52 = 60, '8' has 60th position in char_set.
            else if (encoded[i + j] >= '0' && encoded[i + j] <= '9')
                num = num | (encoded[i + j] - '0' + 52);

            // '+' occurs in 62nd position in char_set.
            else if (encoded[i + j] == '+')
                num = num | 62;

            // '/' occurs in 63rd position in char_set.
            else if (encoded[i + j] == '/')
                num = num | 63;

            // ( str[i + j] == '=' ) remove 2 bits
            // to delete appended bits during encoding.
            else {
                num = num >> 2;
                count_bits -= 2;
            }
        }

        while (count_bits != 0) {
            count_bits -= 8;

            // 255 in binary is 11111111
            decoded_string[k++] = (num >> count_bits) & 255;
        }
    }

    // place NULL character to mark end of string.
    decoded_string[k] = '\0';

    return decoded_string;
}

// Driver function
int main()
{
    char encoded_string[] = "TUVOT04=";
    int len_str = sizeof(encoded_string) / sizeof(encoded_string[0]);

    // Do not count last NULL character.
    len_str -= 1;

    printf("Encoded string : %s\n", encoded_string);
    printf("Decoded_string : %s\n", base64Decoder(encoded_string, len_str));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to decode a base64
// Encoded String back to ASCII String

class GFG
{
    static final int SIZE = 100;

/* char_set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz0123456789+/" */
static String base64Decoder(char encoded[], int len_str)
{
    char []decoded_String;

    decoded_String = new char[SIZE];

    int i, j, k = 0;

    // stores the bitstream.
    int num = 0;

    // count_bits stores current
    // number of bits in num.
    int count_bits = 0;

    // selects 4 characters from
    // encoded String at a time.
    // find the position of each encoded
    // character in char_set and stores in num.
    for (i = 0; i < len_str; i += 4)
    {
        num = 0; count_bits = 0;
        for (j = 0; j < 4; j++)
        {

            // make space for 6 bits.
            if (encoded[i + j] != '=')
            {
                num = num << 6;
                count_bits += 6;
            }

            /* Finding the position of each encoded
            character in char_set
            and storing in "num", use OR
            '|' operator to store bits.*/

            // encoded[i + j] = 'E', 'E' - 'A' = 5
            // 'E' has 5th position in char_set.
            if (encoded[i + j] >= 'A' && encoded[i + j] <= 'Z')
                num = num | (encoded[i + j] - 'A');

            // encoded[i + j] = 'e', 'e' - 'a' = 5,
            // 5 + 26 = 31, 'e' has 31st position in char_set.
            else if (encoded[i + j] >= 'a' && encoded[i + j] <= 'z')
                num = num | (encoded[i + j] - 'a' + 26);

            // encoded[i + j] = '8', '8' - '0' = 8
            // 8 + 52 = 60, '8' has 60th position in char_set.
            else if (encoded[i + j] >= '0' && encoded[i + j] <= '9')
                num = num | (encoded[i + j] - '0' + 52);

            // '+' occurs in 62nd position in char_set.
            else if (encoded[i + j] == '+')
                num = num | 62;

            // '/' occurs in 63rd position in char_set.
            else if (encoded[i + j] == '/')
                num = num | 63;

            // ( str[i + j] == '=' ) remove 2 bits
            // to delete appended bits during encoding.
            else
            {
                num = num >> 2;
                count_bits -= 2;
            }
        }

        while (count_bits != 0) {
            count_bits -= 8;

            // 255 in binary is 11111111
            decoded_String[k++] = (char)
                ((num >> count_bits) & 255);
        }
    }

    return String.valueOf(decoded_String);
}

// Driver code
public static void main(String[] args)
{
    char encoded_String[] = "TUVOT04=".toCharArray();
    int len_str = encoded_String.length;

    // Do not count last null character.
    len_str -= 1;

    System.out.printf("Encoded String : %s\n",
                       String.valueOf(encoded_String));
    System.out.printf("Decoded_String : %s\n",
                       base64Decoder(encoded_String, len_str));
}
}

// This code is contributed by 29AjayKumar
```

## C#

```
// C# Program to decode a base64
// Encoded String back to ASCII String
using System;

class GFG
{
    static readonly int SIZE = 100;

/* char_set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz0123456789+/" */
static String base64Decoder(char []encoded, int len_str)
{
    char []decoded_String;

    decoded_String = new char[SIZE];

    int i, j, k = 0;

    // stores the bitstream.
    int num = 0;

    // count_bits stores current
    // number of bits in num.
    int count_bits = 0;

    // selects 4 characters from
    // encoded String at a time.
    // find the position of each encoded
    // character in char_set and stores in num.
    for (i = 0; i < len_str; i += 4)
    {
        num = 0; count_bits = 0;
        for (j = 0; j < 4; j++)
        {

            // make space for 6 bits.
            if (encoded[i + j] != '=')
            {
                num = num << 6;
                count_bits += 6;
            }

            /* Finding the position of each encoded
            character in char_set
            and storing in "num", use OR
            '|' operator to store bits.*/

            // encoded[i + j] = 'E', 'E' - 'A' = 5
            // 'E' has 5th position in char_set.
            if (encoded[i + j] >= 'A' && encoded[i + j] <= 'Z')
                num = num | (encoded[i + j] - 'A');

            // encoded[i + j] = 'e', 'e' - 'a' = 5,
            // 5 + 26 = 31, 'e' has 31st position in char_set.
            else if (encoded[i + j] >= 'a' && encoded[i + j] <= 'z')
                num = num | (encoded[i + j] - 'a' + 26);

            // encoded[i + j] = '8', '8' - '0' = 8
            // 8 + 52 = 60, '8' has 60th position in char_set.
            else if (encoded[i + j] >= '0' && encoded[i + j] <= '9')
                num = num | (encoded[i + j] - '0' + 52);

            // '+' occurs in 62nd position in char_set.
            else if (encoded[i + j] == '+')
                num = num | 62;

            // '/' occurs in 63rd position in char_set.
            else if (encoded[i + j] == '/')
                num = num | 63;

            // ( str[i + j] == '=' ) remove 2 bits
            // to delete appended bits during encoding.
            else
            {
                num = num >> 2;
                count_bits -= 2;
            }
        }

        while (count_bits != 0)
        {
            count_bits -= 8;

            // 255 in binary is 11111111
            decoded_String[k++] = (char)
                ((num >> count_bits) & 255);
        }
    }

    return String.Join("",decoded_String);
}

// Driver code
public static void Main(String[] args)
{
    char []encoded_String = "TUVOT04=".ToCharArray();
    int len_str = encoded_String.Length;

    // Do not count last null character.
    len_str -= 1;

    Console.Write("Encoded String : {0}\n",
                    String.Join("",encoded_String));
    Console.Write("Decoded_String : {0}\n",
                    base64Decoder(encoded_String, len_str));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Program to decode a base64
// Encoded String back to ASCII String

let SIZE = 100;

/* char_set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ
abcdefghijklmnopqrstuvwxyz0123456789+/" */
function base64Decoder(encoded,len_str)
{
    let decoded_String;

    decoded_String = new Array(SIZE);

    let i, j, k = 0;

    // stores the bitstream.
    let num = 0;

    // count_bits stores current
    // number of bits in num.
    let count_bits = 0;

    // selects 4 characters from
    // encoded String at a time.
    // find the position of each encoded
    // character in char_set and stores in num.
    for (i = 0; i < len_str; i += 4)
    {
        num = 0; count_bits = 0;
        for (j = 0; j < 4; j++)
        {

            // make space for 6 bits.
            if (encoded[i + j] != '=')
            {
                num = num << 6;
                count_bits += 6;
            }

            /* Finding the position of each encoded
            character in char_set
            and storing in "num", use OR
            '|' operator to store bits.*/

            // encoded[i + j] = 'E', 'E' - 'A' = 5
            // 'E' has 5th position in char_set.
            if (encoded[i + j].charCodeAt(0) >=
            'A'.charCodeAt(0) && encoded[i + j].charCodeAt(0)
            <= 'Z'.charCodeAt(0))
            num = num | (encoded[i + j].charCodeAt(0) -
            'A'.charCodeAt(0));

            // encoded[i + j] = 'e', 'e' - 'a' = 5,
            // 5 + 26 = 31, 'e' has 31st position in char_set.
            else if (encoded[i + j].charCodeAt(0) >=
            'a'.charCodeAt(0) && encoded[i + j].charCodeAt(0) <=
            'z'.charCodeAt(0))
                num = num | (encoded[i + j].charCodeAt(0) -
                'a'.charCodeAt(0) + 26);

            // encoded[i + j] = '8', '8' - '0' = 8
            // 8 + 52 = 60, '8' has 60th position in char_set.
            else if (encoded[i + j].charCodeAt(0) >=
            '0'.charCodeAt(0) && encoded[i + j].charCodeAt(0) <=
            '9'.charCodeAt(0))
                num = num | (encoded[i + j].charCodeAt(0) -
                '0'.charCodeAt(0) + 52);

            // '+' occurs in 62nd position in char_set.
            else if (encoded[i + j] == '+')
                num = num | 62;

            // '/' occurs in 63rd position in char_set.
            else if (encoded[i + j] == '/')
                num = num | 63;

            // ( str[i + j] == '=' ) remove 2 bits
            // to delete appended bits during encoding.
            else
            {
                num = num >> 2;
                count_bits -= 2;
            }
        }

        while (count_bits != 0) {
            count_bits -= 8;

            // 255 in binary is 11111111
            decoded_String[k++] = String.fromCharCode
                ((num >> count_bits) & 255);
        }
    }

    return (decoded_String);
}

// Driver code
let encoded_String = "TUVOT04=".split("");
    let len_str = encoded_String.length;

    // Do not count last null character.
    len_str -= 1;

    document.write("Encoded String : " +
                       (encoded_String).join("")+"<br>");
    document.write("Decoded_String : "+
        base64Decoder(encoded_String, len_str).join("")+"<br>");

// This code is contributed by rag2127

</script>
```

**输出:**

```
Encoded string : TUVO04=
Decoded string : MENON
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)
本文由[**<u>Arshpreet Soodan</u>**](https://github.com/soodan)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。