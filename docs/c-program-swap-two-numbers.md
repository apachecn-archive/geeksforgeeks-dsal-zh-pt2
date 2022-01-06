# 交换两个号码的程序

> 原文:[https://www.geeksforgeeks.org/c-program-swap-two-numbers/](https://www.geeksforgeeks.org/c-program-swap-two-numbers/)

给定两个数字，编写一个 C 程序来交换给定的数字。

```
Input : x = 10, y = 20;
Output : x = 20, y = 10

Input : x = 200, y = 100
Output : x = 100, y = 200

```

![](https://media.geeksforgeeks.org/wp-content/cdn-uploads/CommonArticleDesign16.png)

想法很简单

1.  将 x 赋给一个临时变量:temp = x
2.  将 y 指定给 x : x = y
3.  将温度分配给 y : y =温度

让我们用一个例子来理解。

> x = 100，y = 200
> 
> 第 1 行后:温度= x
> 温度= 100
> 
> 第 2 行后:x = y
> x = 200
> 
> 第 3 行后:y =温度
> y = 100

```
// C program to swap two variables
#include <stdio.h>

int main()
{
    int x, y;
    printf("Enter Value of x ");
    scanf("%d", &x);
    printf("\nEnter Value of y ");
    scanf("%d", &y);

    int temp = x;
    x = y;
    y = temp;

    printf("\nAfter Swapping: x = %d, y = %d", x, y);
    return 0;
}
```

输出:

```
Enter Value of x 12

Enter Value of y 14

After Swapping: x = 14, y = 12 
```

**如何编写函数进行交换？**
既然我们希望 main 的局部变量被 swap 函数修改，我们就必须使用 C 中的[指针来修改它们。](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)

```
// C program to swap two variables using a 
// user defined swap()
#include <stdio.h>

// This function swaps values pointed by xp and yp
void swap(int *xp, int *yp)
{
    int temp = *xp;
    *xp = *yp;
    *yp = temp;
}

int main()
{
    int x, y;
    printf("Enter Value of x ");
    scanf("%d", &x);
    printf("\nEnter Value of y ");
    scanf("%d", &y);
    swap(&x, &y);
    printf("\nAfter Swapping: x = %d, y = %d", x, y);
    return 0;
}
```

输出:

```
Enter Value of x 12

Enter Value of y 14

After Swapping: x = 14, y = 12 
```

**用 C++怎么做？**
在 C++中，我们可以用[引用](https://www.geeksforgeeks.org/references-in-c/)也可以。

```
// C++ program to swap two variables using a 
// user defined swap()
#include <stdio.h>

// This function swaps values referred by 
// x and y,
void swap(int &x, int &y)
{
    int temp = x;
    x = y;
    y = temp;
}

int main()
{
    int x, y;
    printf("Enter Value of x ");
    scanf("%d", &x);
    printf("\nEnter Value of y ");
    scanf("%d", &y);
    swap(x, y);
    printf("\nAfter Swapping: x = %d, y = %d", x, y);
    return 0;
}
```

输出:

```
Enter Value of x 12

Enter Value of y 14

After Swapping: x = 14, y = 12 
```

**有库函数吗？**
我们可以用 [C++库互换功能](https://www.geeksforgeeks.org/swap-in-cpp/)也可以。

```
// C++ program to swap two variables using a 
// user defined swap()
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int x, y;
    printf("Enter Value of x ");
    scanf("%d", &x);
    printf("\nEnter Value of y ");
    scanf("%d", &y);
    swap(x, y);
    printf("\nAfter Swapping: x = %d, y = %d", x, y);
    return 0;
}
```

输出:

```
Enter Value of x 12

Enter Value of y 14

After Swapping: x = 14, y = 12 
```

 **[不使用临时变量怎么互换？](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)**