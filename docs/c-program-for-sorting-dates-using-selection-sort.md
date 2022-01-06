# 使用选择排序对日期进行排序的 C++程序

> 原文:[https://www . geesforgeks . org/c-排序程序-日期-使用-选择-排序/](https://www.geeksforgeeks.org/c-program-for-sorting-dates-using-selection-sort/)

```
// C++ program for sorting dates using selectio0n sort
#include<bits/stdc++.h>
using namespace std;
struct date
{
    int day;
    int month;
    int year;
};

int main()
{
    struct date input[5];
    for(int i=0; i<5; i++)
    {
        cin>>input[i].day;
        cin>>input[i].month;
        cin>>input[i].year;

    }
    for (int i=0; i<4; i++)
    {
        for (int j=i+1; j<5; j++)
        {
            if (input[i].year > input[j].year)
            {
                struct date temp = input[i];
                input[i] = input[j];
                input[j] = temp;
            }
            else if (input[i].year == input[j].year && input[i].month > input[j].month)
            {
                struct date temp = input[i];
                input[i] = input[j];
                input[j] = temp;
            }
            else if (input[i].year == input[j].year && input[i].month == input[j].month && input[i].day > input[j].day)
            {
                struct date temp = input[i];
                input[i] = input[j];
                input[j] = temp;
            }

        }
    }

    for(int i=0; i<5; i++)
    {
        cout<<input[i].day<<" "<<input[i].month<<" "<<input[i].year;
        cout<<endl;
    }
}
```

本节目由 Dinesh T.P.D .提供。如果您发现任何不正确的地方，或者您想分享关于上述主题的更多信息，请写评论