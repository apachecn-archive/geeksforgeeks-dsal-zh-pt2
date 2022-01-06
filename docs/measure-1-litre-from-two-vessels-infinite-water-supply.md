# 使用两个容器和无限供水测量 1 升

> 原文:[https://www . geeksforgeeks . org/measure-两船 1 升-无限供水/](https://www.geeksforgeeks.org/measure-1-litre-from-two-vessels-infinite-water-supply/)

有两个容量分别为“a”和“b”的容器。我们有无限的水源。给出一个有效的算法，在其中一个容器中精确地制造 1 升水。你可以在任何时间点从任何容器中抛出所有的水。假设‘a’和‘b’是[共线](http://en.wikipedia.org/wiki/Coprime_integers)。
步骤如下:
设 V1 为 a 容量船，V2 为 b 容量船，a 小于 b。
**1)** 在 V1 水量不为 1 的情况下做以下动作。
…。 **a)** 如果 V1 是空的，那么完全填满 V1
…。 **b)** 从 V1 向 V2 调水。如果 V2 变满，则保持 V1 的剩余水，清空 V2
**2)** 在步骤 1 中循环终止后，V1 将有 1 升。返回。
以下是上述算法的 C++实现。

## C++

```
/* Sample run of the Algo for V1 with capacity 3 and V2 with capacity 7
1\. Fill V1:                             V1 = 3, V2 = 0
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 3
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 6
3\. Transfer from V1 to V2, and empty V2: V1 = 2, V2 = 0
4\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 2
5\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 5
6\. Transfer from V1 to V2, and empty V2: V1 = 1, V2 = 0
7\. Stop as V1 now contains 1 litre.

Note that V2 was made empty in steps 3 and 6 because it became full */

#include <iostream>
using namespace std;

// A utility function to get GCD of two numbers
int gcd(int a, int b) { return b? gcd(b, a % b) : a; }

// Class to represent a Vessel
class Vessel
{
    // A vessel has capacity, and current amount of water in it
    int capacity, current;
public:
    // Constructor: initializes capacity as given, and current as 0
    Vessel(int capacity) { this->capacity = capacity; current = 0; }

    // The main function to fill one litre in this vessel. Capacity of V2
    // must be greater than this vessel and two capacities must be co-prime
    void makeOneLitre(Vessel &V2);

    // Fills vessel with given amount and returns the amount of water
    // transferred to it. If the vessel becomes full, then the vessel
    // is made empty.
    int transfer(int amount);
};

// The main function to fill one litre in this vessel. Capacity
// of V2 must be greater than this vessel and two capacities
// must be coprime
void Vessel:: makeOneLitre(Vessel &V2)
{
    // solution exists iff a and b are co-prime
    if (gcd(capacity, V2.capacity) != 1)
        return;

    while (current != 1)
    {
        // fill A (smaller vessel)
        if (current == 0)
            current = capacity;

        cout << "Vessel 1: " << current << " Vessel 2: "
            << V2.current << endl;

        // Transfer water from V1 to V2 and reduce current of V1 by
        // the amount equal to transferred water
        current = current - V2.transfer(current);
    }

    // Finally, there will be 1 litre in vessel 1
    cout << "Vessel 1: " << current << " Vessel 2: "
        << V2.current << endl;
}

// Fills vessel with given amount and returns the amount of water
// transferred to it. If the vessel becomes full, then the vessel
// is made empty
int Vessel::transfer(int amount)
{
    // If the vessel can accommodate the given amount
    if (current + amount < capacity)
    {
        current += amount;
        return amount;
    }

    // If the vessel cannot accommodate the given amount, then
    // store the amount of water transferred
    int transferred = capacity - current;

    // Since the vessel becomes full, make the vessel
    // empty so that it can be filled again
    current = 0;

    return transferred;
}

// Driver program to test above function
int main()
{
    int a = 3, b = 7; // a must be smaller than b

    // Create two vessels of capacities a and b
    Vessel V1(a), V2(b);

    // Get 1 litre in first vessel
    V1.makeOneLitre(V2);

    return 0;
}
```

## C#

```
/* Sample run of the Algo for V1 with capacity 3 and V2 with capacity 7
1\. Fill V1:                             V1 = 3, V2 = 0
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 3
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 6
3\. Transfer from V1 to V2, and empty V2: V1 = 2, V2 = 0
4\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 2
5\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 5
6\. Transfer from V1 to V2, and empty V2: V1 = 1, V2 = 0
7\. Stop as V1 now contains 1 litre.

Note that V2 was made empty in steps 3 and 6 because it became full */

using System;

class GFG
{

    // A utility function to get GCD of two numbers
    static int gcd(int a, int b)
    {
        return b > 0 ? gcd(b, a % b) : a;
    }

    // Class to represent a Vessel
    class Vessel
    {

        // A vessel has capacity, and
        // current amount of water in it
        int capacity, current;

        // Constructor: initializes capacity
        // as given, and current as 0
        public Vessel(int capacity)
        {
            this.capacity = capacity;
            current = 0;
        }

        // The main function to fill one litre
        // in this vessel. Capacity of V2 must be
        // greater than this vessel and two capacities
        // must be coprime
        public void makeOneLitre(Vessel V2)
        {
            // solution exists iff a and b are co-prime
            if (gcd(capacity, V2.capacity) != 1)
                return;

            while (current != 1)
            {
                // fill A (smaller vessel)
                if (current == 0)
                    current = capacity;

                Console.Write("Vessel 1: " + current +
                            " Vessel 2: " + V2.current + "\n");

                // Transfer water from V1 to V2 and
                // reduce current of V1 by
                // the amount equal to transferred water
                current = current - V2.transfer(current);
            }

            // Finally, there will be 1 litre in vessel 1
            Console.Write("Vessel 1: " + current +
                        " Vessel 2: " + V2.current + "\n");
        }

        // Fills vessel with given amount and
        // returns the amount of water
        // transferred to it. If the vessel
        // becomes full, then the vessel
        // is made empty
        int transfer(int amount)
        {
            // If the vessel can accommodate the given amount
            if (current + amount < capacity)
            {
                current += amount;
                return amount;
            }

            // If the vessel cannot accommodate
            // the given amount, then store
            // the amount of water transferred
            int transferred = capacity - current;

            // Since the vessel becomes full, make the vessel
            // empty so that it can be filled again
            current = 0;

            return transferred;
        }
    }

    // Driver program to test above function
    public static void Main(String[] args)
    {
        int a = 3, b = 7; // a must be smaller than b

        // Create two vessels of capacities a and b
        Vessel V1 = new Vessel(a);
        Vessel V2 = new Vessel(b);

        // Get 1 litre in first vessel
        V1.makeOneLitre(V2);
    }
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Sample run of the Algo for V1 with capacity 3 and V2 with capacity 7
1\. Fill V1:                             V1 = 3, V2 = 0
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 3
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 6
3\. Transfer from V1 to V2, and empty V2: V1 = 2, V2 = 0
4\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 2
5\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 5
6\. Transfer from V1 to V2, and empty V2: V1 = 1, V2 = 0
7\. Stop as V1 now contains 1 litre.

Note that V2 was made empty in steps 3 and 6 because it became full */

class GFG
{

    // A utility function to get GCD of two numbers
    static int gcd(int a, int b)
    {
        return b > 0 ? gcd(b, a % b) : a;
    }

    // Class to represent a Vessel
    static class Vessel
    {

        // A vessel has capacity, and
        // current amount of water in it
        int capacity, current;

        // Constructor: initializes capacity
        // as given, and current as 0
        public Vessel(int capacity)
        {
            this.capacity = capacity;
            current = 0;
        }

        // The main function to fill one litre
        // in this vessel. Capacity of V2 must be
        // greater than this vessel and two capacities
        // must be coprime
        void makeOneLitre(Vessel V2)
        {
            // solution exists iff a and b are co-prime
            if (gcd(capacity, V2.capacity) != 1)
                return;

            while (current != 1)
            {
                // fill A (smaller vessel)
                if (current == 0)
                    current = capacity;

                System.out.print("Vessel 1: " + current +
                            " Vessel 2: " + V2.current + "\n");

                // Transfer water from V1 to V2 and
                // reduce current of V1 by
                // the amount equal to transferred water
                current = current - V2.transfer(current);
            }

            // Finally, there will be 1 litre in vessel 1
            System.out.print("Vessel 1: " + current +
                        " Vessel 2: " + V2.current + "\n");
        }

        // Fills vessel with given amount and
        // returns the amount of water
        // transferred to it. If the vessel
        // becomes full, then the vessel
        // is made empty
        int transfer(int amount)
        {
            // If the vessel can accommodate the given amount
            if (current + amount < capacity)
            {
                current += amount;
                return amount;
            }

            // If the vessel cannot accommodate
            // the given amount, then store
            // the amount of water transferred
            int transferred = capacity - current;

            // Since the vessel becomes full, make the vessel
            // empty so that it can be filled again
            current = 0;

            return transferred;
        }
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int a = 3, b = 7; // a must be smaller than b

        // Create two vessels of capacities a and b
        Vessel V1 = new Vessel(a);
        Vessel V2 = new Vessel(b);

        // Get 1 litre in first vessel
        V1.makeOneLitre(V2);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
/* Sample run of the Algo for V1 with capacity 3 and V2 with capacity 7
1\. Fill V1:                             V1 = 3, V2 = 0
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 3
2\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 6
3\. Transfer from V1 to V2, and empty V2: V1 = 2, V2 = 0
4\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 2
5\. Transfer from V1 to V2, and fill V1: V1 = 3, V2 = 5
6\. Transfer from V1 to V2, and empty V2: V1 = 1, V2 = 0
7\. Stop as V1 now contains 1 litre.

Note that V2 was made empty in steps 3 and 6 because it became full */

    // A utility function to get GCD of two numbers
    function gcd(a,b)
    {
        return b > 0 ? gcd(b, a % b) : a;
    }

 // Class to represent a Vessel   
class Vessel
{
    // Constructor: initializes capacity
        // as given, and current as 0
    constructor(capacity)
    {
        this.capacity = capacity;
        this.current = 0;
    }

    // The main function to fill one litre
        // in this vessel. Capacity of V2 must be
        // greater than this vessel and two capacities
        // must be coprime
    makeOneLitre(V2)
    {
        // solution exists iff a and b are co-prime
            if (gcd(this.capacity, V2.capacity) != 1)
                return;

            while (this.current != 1)
            {
                // fill A (smaller vessel)
                if (this.current == 0)
                    this.current = this.capacity;

                document.write("Vessel 1: " + this.current +
                            " Vessel 2: " + V2.current + "<br>");

                // Transfer water from V1 to V2 and
                // reduce current of V1 by
                // the amount equal to transferred water
                this.current = this.current - V2.transfer(this.current);
            }

            // Finally, there will be 1 litre in vessel 1
            document.write("Vessel 1: " + this.current +
                        " Vessel 2: " + V2.current + "<br>");
    }

    // Fills vessel with given amount and
        // returns the amount of water
        // transferred to it. If the vessel
        // becomes full, then the vessel
        // is made empty
    transfer(amount)
    {
        // If the vessel can accommodate the given amount
            if (this.current + amount < this.capacity)
            {
                this.current += amount;
                return amount;
            }

            // If the vessel cannot accommodate
            // the given amount, then store
            // the amount of water transferred
            let transferred = this.capacity - this.current;

            // Since the vessel becomes full, make the vessel
            // empty so that it can be filled again
            this.current = 0;

            return transferred;
    }
}

// Driver program to test above function
let a = 3, b = 7; // a must be smaller than b

// Create two vessels of capacities a and b
let V1 = new Vessel(a);
let V2 = new Vessel(b);

// Get 1 litre in first vessel
V1.makeOneLitre(V2);

// This code is contributed by rag2127
</script>
```

**输出:**

```
Vessel 1: 3   Vessel 2: 0
Vessel 1: 3   Vessel 2: 3
Vessel 1: 3   Vessel 2: 6
Vessel 1: 2   Vessel 2: 0
Vessel 1: 3   Vessel 2: 2
Vessel 1: 3   Vessel 2: 5
Vessel 1: 1   Vessel 2: 0
```

**这是如何工作的？**
为了证明算法有效，我们需要证明在 while 循环中经过一定次数的迭代后，我们将在 V1 得到 1 升。
假设‘a’是 V1 号的容量，而‘b’是 V2 号的容量。由于我们不断将水从 V1 转移到 V2，直到 V2 变满，当 V2 第一次变满时，我们将在 V1 拥有“a–b(mod a)”水。一旦 V2 变满，它就会被清空。当 V2 第二次满水时，我们将在 V1 有“a–2b(mod a)”水。我们重复上述步骤，在 V2 号船装满和清空 n 次后，在 V1 获得 a–nb(mod a)水。我们需要证明‘a–nb(mod a)’的值对于有限整数‘n’将是 1。为了证明这一点，让我们考虑互质数的下列性质。
对于任意两个[互质整数](http://en.wikipedia.org/wiki/Coprime_integers)“a”和“b”，整数“b”具有以“a”为模的[乘法逆](http://en.wikipedia.org/wiki/Modular_multiplicative_inverse)。换句话说，存在一个整数‘y’，比如‘b * y≡1(mod)a’(见第三点[此处](http://en.wikipedia.org/wiki/Coprime_integers#Properties))。经过'(a–1)* y '次迭代，我们在 V1 将有' a –[(a-1)*y * b(mod a)]'水，这个表达式的值是' a –[(a–1)* 1]mod a '即 1。所以算法收敛了，我们在 V1 得到了 1 升。
本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish?fref=ts)编写。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。