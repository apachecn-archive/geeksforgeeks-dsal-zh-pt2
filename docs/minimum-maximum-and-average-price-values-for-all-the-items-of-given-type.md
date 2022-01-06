# 给定类型所有项目的最低、最高和平均价格值

> 原文:[https://www . geesforgeks . org/给定类型所有物品的最低-最高-平均价格值/](https://www.geeksforgeeks.org/minimum-maximum-and-average-price-values-for-all-the-items-of-given-type/)

给定一个字符串数组**项目[]** 和一个整数数组**价格[]** ，其中**价格【I】**是从 **i <sup>th</sup>** 商店购买的**项目【I】**的价格。任务是找到所有采购项目的最低、最高和平均价格值。

**示例:**

> **输入:**项[] = {“玩具”、“笔”、“笔记本”、“笔”}，价格[] = {2，1，3，2}
> **输出:**
> 项 Min Max Average
> 笔 1 2 1.5
> 玩具 2 2 2.0
> 笔记本 3 3.0
> 
> **输入:**项[] = {“车”、“车”}，价格[] = {20000，30000 }；
> **产量:**
> 单品最低最高均价
> 车 20000 30000 25000.0

**方法:**创建一个[哈希表](https://www.geeksforgeeks.org/java-util-hashmap-in-java/)，其中项目的名称将是一个字符串，值将是一个对象，该对象将为每个项目存储四种类型的值，即

1.  **分钟:**存储当前类型项目的最小值。
2.  **最大值:**存储当前类型项目的最大值。
3.  **合计:**当前类型的合计项目。
4.  **总和:**当前类型项目价格的总和。

现在，对于 Hashmap 中存储的每个项目，最低和最高价格都存储在 value 对象中，平均值可以计算为**总和/总和**。

以下是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG {

    // To store an item
    static class Item {

        // To store the minimum and the
        // maximum price for the item
        int min, max;

        // To store the total number of items
        // of the current type and the
        // total cost of buying them
        int total, sum;

        // Initializing an element
        Item(int price)
        {
            min = price;
            max = price;
            total = 1;
            this.sum = price;
        }
    }

    // Function to find the minimum, the maximum
    // and the average price for every item
    static void findPrices(String item[], int price[], int n)
    {

        // To store the distinct items
        HashMap<String, Item> map = new HashMap<>();

        // For every item
        for (int i = 0; i < n; i++) {

            // If the current item has aready been
            // purchased earlier from a different shop
            if (map.containsKey(item[i])) {

                // Get the item
                Item currItem = map.get(item[i]);

                // Update its minimum and maximum price so far
                currItem.min = Math.min(currItem.min, price[i]);
                currItem.max = Math.max(currItem.max, price[i]);

                // Increment the total count of the current item
                currItem.total++;

                // Add the current price to the sum
                currItem.sum += price[i];
            }
            else {

                // The item has been purchased for the first time
                Item currItem = new Item(price[i]);
                map.put(item[i], currItem);
            }
        }

        // Print all the items with their
        // minimum, maximum and average prices
        System.out.println("Item Min Max Average");
        for (Map.Entry<String, Item> ob : map.entrySet()) {
            String key = ob.getKey();
            Item currItem = ob.getValue();
            System.out.println(key + " " + currItem.min
                               + " " + currItem.max + " "
                               + ((float)currItem.sum / (float)currItem.total));
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String item[] = { "toy", "pen", "notebook", "pen" };
        int n = item.length;
        int price[] = { 2, 1, 3, 2 };

        findPrices(item, price, n);
    }
}
```

## C#

```
// C# implementation of the approach 
using System;         
using System.Collections.Generic;

class GFG 
{

    // To store an item
    public class Item
    {

        // To store the minimum and the
        // maximum price for the item
        public int min, max;

        // To store the total number of items
        // of the current type and the
        // total cost of buying them
        public int total, sum;

        // Initializing an element
        public Item(int price)
        {
            min = price;
            max = price;
            total = 1;
            this.sum = price;
        }
    }

    // Function to find the minimum, the maximum
    // and the average price for every item
    static void findPrices(String []item, 
                              int []price, int n)
    {

        // To store the distinct items
        Dictionary<String,
                   Item> map = new Dictionary<String,
                                              Item>();

        // For every item
        for (int i = 0; i < n; i++)
        {

            // If the current item has aready been
            // purchased earlier from a different shop
            if (map.ContainsKey(item[i]))
            {

                // Get the item
                Item currItem = map[item[i]];

                // Update its minimum and
                // maximum price so far
                currItem.min = Math.Min(currItem.min,
                                           price[i]);
                currItem.max = Math.Max(currItem.max, 
                                           price[i]);

                // Increment the total count of 
                // the current item
                currItem.total++;

                // Add the current price to the sum
                currItem.sum += price[i];
            }
            else 
            {

                // The item has been purchased
                // for the first time
                Item currItem = new Item(price[i]);
                map.Add(item[i], currItem);
            }
        }

        // Print all the items with their
        // minimum, maximum and average prices
        Console.WriteLine("Item Min Max Average");
        foreach(KeyValuePair<String, Item> ob in map)
        {
            String key = ob.Key;
            Item currItem = ob.Value;
            Console.WriteLine(key + " " + currItem.min + 
                                    " " + currItem.max + 
                                    " " + ((float)currItem.sum /
                                           (float)currItem.total));
        }
    }

    // Driver code
    public static void Main(String []args)
    {
        String []item = { "toy", "pen", "notebook", "pen" };
        int n = item.Length;
        int []price = { 2, 1, 3, 2 };

        findPrices(item, price, n);
    }
}

// This code is contributed by 29AjayKumar
```

**Output:**

```
Item Min Max Average
pen 1 2 1.5
toy 2 2 2.0
notebook 3 3 3.0

```