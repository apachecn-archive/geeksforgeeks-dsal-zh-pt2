# 将一个文本文件的内容附加到另一个文本文件的程序

> 原文:[https://www . geesforgeks . org/c-program-to-append-content-of-one-text-file-to-other/](https://www.geeksforgeeks.org/c-program-to-append-content-of-one-text-file-to-another/)

**先决条件:** [文件处理在 C](https://www.geeksforgeeks.org/basics-file-handling-c/)

给定源文件和目标文本文件，任务是将内容从源文件追加到目标文件，然后显示目标文件的内容。
**例:**

```
Input: 

file1.text
This is line one in file1
Hello World.
file2.text
This is line one in file2
Programming is fun.

Output: 

This is line one in file2
Programming is fun.
This is line one in file1
Hello World.

```

**进场:**

1.  用“a+”(追加并读取)选项打开**文件 1.txt** 、**文件 2.txt** ，不删除文件之前的内容。如果文件不存在，它们将被创建。
2.  向目标文件显式写入换行符(" \n ")，以增强可读性。
3.  将内容从源文件写入目标文件。
4.  将 file2.txt 中的内容显示到控制台(stdout)。

## C

```
// C program to append the contents of
// source file to the destination file
// including header files
#include <stdio.h>

// Function that appends the contents
void appendFiles(char source[],
                 char destination[])
{
    // declaring file pointers
    FILE *fp1, *fp2;

    // opening files
    fp1 = fopen(source, "a+");
    fp2 = fopen(destination, "a+");

    // If file is not found then return.
    if (!fp1 && !fp2) {
        printf("Unable to open/"
               "detect file(s)\n");
        return;
    }

    char buf[100];

    // explicitly writing "\n"
    // to the destination file
    // so to enhance readability.
    fprintf(fp2, "\n");

    // writing the contents of
    // source file to destination file.
    while (!feof(fp1)) {
        fgets(buf, sizeof(buf), fp1);
        fprintf(fp2, "%s", buf);
    }

    rewind(fp2);

    // printing contents of
    // destination file to stdout.
    while (!feof(fp2)) {
        fgets(buf, sizeof(buf), fp2);
        printf("%s", buf);
    }
}

// Driver Code
int main()
{
    char source[] = "file1.txt",
         destination[] = "file2.txt";

    // calling Function with file names.
    appendFiles(source, destination);

    return 0;
}
```

**输出:**

以下是上述程序的输出:

[![](img/8073b8a4b090e24d3006c375eb14e1e4.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20200626095425/File-handling-Output.png)

**时间复杂度:O(N)**
**辅助空间复杂度:O(1)**