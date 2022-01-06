# 使用 StringStream

查找两个日期之间的天数

> 原文:[https://www . geeksforgeeks . org/find-两个日期之间的天数-使用-stringstream/](https://www.geeksforgeeks.org/finding-number-of-days-between-two-dates-using-stringstream/)

给定代表两个日期的两个字符串 **str1** 和 **str2** ，任务是计算给定两个日期之间的天数。鉴于给出的日期在 1971 年之后。

**示例:**

> **输入:**str 1 =“2020-01-29”，str 2 =“2020-01-30”
> **输出:** 1
> **说明:**
> 1 月 29 日<sup>至 1 月 30 日<sup>之间的天数为 1。</sup></sup>
> 
> **输入:**str 1 =“1971-06-29”，str 2 =“2019-06-23”
> T3】输出: 17526

**方法:**想法是将两个日期转换成各自的秒。由于一天有 86，400 秒，两天之间的天数可以通过用 86，400 除秒差来计算。

下面是上述方法的实现:

```
// C++ implementation of the above approach
#include <iostream>
#include <sstream>
#include <string>
using namespace std;

// Function to find the number of days
// between given two dates
int daysBetweenDates(string date1, string date2)
{
    stringstream ss(date1 + "-" + date2);
    int year, month, day;
    char hyphen;

    // Parse the first date into seconds
    ss >> year >> hyphen >> month >> hyphen >> day;
    struct tm starttm = { 0, 0, 0, day,
                          month - 1, year - 1900 };
    time_t start = mktime(&starttm);

    // Parse the second date into seconds
    ss >> hyphen >> year >> hyphen
        >> month >> hyphen >> day;
    struct tm endtm = { 0, 0, 0, day,
                        month - 1, year - 1900 };
    time_t end = mktime(&endtm);

    // Find out the difference and divide it
    // by 86400 to get the number of days
    return abs(end - start) / 86400;
}

// Driver code
int main()
{
    string str1 = "2019-09-12";
    string str2 = "2020-08-04";
    cout << daysBetweenDates(str1, str2);
    return 0;
}
```

**Output:**

```
327

```