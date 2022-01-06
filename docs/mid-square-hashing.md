# 中方形散列

> 原文:[https://www.geeksforgeeks.org/mid-square-hashing/](https://www.geeksforgeeks.org/mid-square-hashing/)

中方形哈希是一种生成唯一密钥的哈希技术。在这种技术中，种子值被取平方。然后，从中间提取一些数字。这些提取的数字形成一个数字，作为新的种子。如果采用足够大的种子值，这种技术可以生成具有高度随机性的密钥。然而，它有一个局限性。由于种子是平方的，如果取一个 6 位数，那么平方将有 12 位数。这超出了 int 数据类型的范围。所以，溢出一定要处理好。如果溢出，使用长整型数据类型，如果溢出仍然发生，则使用[字符串作为乘法](https://www.geeksforgeeks.org/multiply-large-numbers-represented-as-strings/)。在中方形哈希中发生冲突的几率很低，而不是过时。因此，在可能的情况下，如果发生冲突，将使用一些[哈希映射](https://www.geeksforgeeks.org/hashing-data-structure/)来处理。

**例**:

> 假设取一个 4 位数的种子。seed = 4765
> 因此，seed 的平方是= 4765 * 4765 = 22705225
> 现在，从这个 8 位数中，提取任意四位数字(比如中间的四位)。
> 所以，新的种子值变成 seed = 7052
> 现在，这个新种子的平方是= 7052 * 7052 = 49730704
> 再次，提取相同的 4 位数集合。
> 于是，新的种子值变成 seed = 7307
> 。
> 。
> 。
> 。
> 该过程重复的次数与需要一把钥匙的次数一样多。

中间平方技术从一个数字的平方中取一定数量的数字。提取的这个数字是一个伪随机数，可以用作哈希的密钥。

**算法:**

1.  选择种子值。这是一个重要的步骤，因为对于相同的种子值，生成相同的随机数序列。
2.  取种子值的平方，用平方中出现的特定位数更新种子。**注**:位数越大，随机性越大。
3.  归还钥匙。

下面是上述算法的实现:

```
// C++ program to illustrate the
// mid-square hashing technique
#include <ctime>
#include <iostream>

using namespace std;

// Returns a seed value based on current system time.
long long int newTime()
{

    // Acquiring number of seconds
    // passed from Jan 1, 1970.
    time_t t = time(NULL);

    // Converting the time to year, month,
    // day, hour, minute, and second.
    struct tm* tm = localtime(&t);
    long long int x;

    // Applying a certain logic to get
    // required number of digits. It may vary.
    x = (tm->tm_hour) * 10000000 + (tm->tm_min) * 100000
        + (tm->tm_sec) * 1000 + (tm->tm_mday) * 10 + (tm->tm_year);

    // Return the calculated number.
    return x;
}

// Returns a random 8-digit key.
long int getKey()
{

    // Taking the key from system time. 
    // returns a  8-digit seed value.
    static long long int key = newTime();

    // Squaring the key.
    key = key * key;

    // Extracting required number of digits ( here, 8 ).
    if (key < 1000000000000000) {
        key = key / 10000;
        key = key % 100000000;
    }
    else {
        key = key / 10000;
        key = key % 100000000;
    }

    // Returning the key value.
    return key;
}

// Driver Code
int main()
{
    // get the first key
    std::cout << getKey() << endl;

    // get the second key
    std::cout << getKey() << endl;
    return 0;
}
```

**Output:**

```
56002270
25424515

```

**注意:**输出会根据日期和时间变化。