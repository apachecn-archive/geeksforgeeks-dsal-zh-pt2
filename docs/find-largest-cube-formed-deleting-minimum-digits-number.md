# 找出从一个数字中删除最小数字形成的最大立方体

> 原文:[https://www . geesforgeks . org/find-最大-立方体-格式-删除-最小位数-数字/](https://www.geeksforgeeks.org/find-largest-cube-formed-deleting-minimum-digits-number/)

给定一个数字 n，任务是找到最大的完美立方体，它可以通过从数字中删除最小的数字(可能是 0)来形成。
如果 X = Y <sup>3</sup> 对于某些 Y
T4【例:
X 被称为完美立方体

```
Input : 4125
Output : 125
Explanation
125 = 53. We can form 125 by deleting digit 4 from 4125

Input : 876
Output :8
Explanation
8 = 23. We can form 8 by deleting digits 7 and 6 from 876
```

我们可以生成从 1 到 N 的所有数字的立方体 <sup>1/3</sup> (我们不认为 0 是 0 就不认为是完美的立方体)。我们从最大到最小迭代立方体。
现在如果我们看给我们的数字 n，那么我们知道这个数字只包含 log(n) + 1 个数字，因此如果我们以后把这个数字 n 当作一个字符串，我们可以有效地处理这个问题。
当迭代完美立方体时，我们检查当它被表示为字符串时，完美立方体是否是数字 n 的子序列。如果是这种情况，那么将数字 n 更改为当前完美立方体所需的删除是:

```
No of deleted digits = No of digits in number n - 
                       Number of digits in current 
                                      perfect cube
```

因为我们想要最大的立方体数，所以我们以相反的顺序遍历预处理立方体的数组。

## C++

```
/* C++ code to implement maximum perfect cube
   formed after deleting  minimum digits */
#include <bits/stdc++.h>
using namespace std;

// Returns vector of Pre Processed perfect cubes
vector<string> preProcess(long long int n)
{
    vector<string> preProcessedCubes;
    for (int i = 1; i * i * i <= n; i++) {
        long long int iThCube = i * i * i;

        // convert the cube to string and push into
        // preProcessedCubes vector
        string cubeString = to_string(iThCube);
        preProcessedCubes.push_back(cubeString);
    }
    return preProcessedCubes;
}

/* Utility function for findLargestCube().
   Returns the Largest cube number that can be formed */
string findLargestCubeUtil(string num,
                    vector<string> preProcessedCubes)
{
    // reverse the preProcessed cubes so that we
    // have the largest cube in the beginning
    // of the vector
    reverse(preProcessedCubes.begin(), preProcessedCubes.end());

    int totalCubes = preProcessedCubes.size();

    // iterate over all cubes
    for (int i = 0; i < totalCubes; i++) {
        string currCube = preProcessedCubes[i];

        int digitsInCube = currCube.length();
        int index = 0;
        int digitsInNumber = num.length();
        for (int j = 0; j < digitsInNumber; j++) {

            // check if the current digit of the cube
            // matches with that of the number num
            if (num[j] == currCube[index])
                index++;

            if (digitsInCube == index)                
                return currCube;           
        }
    }

    // if control reaches here, the its
    // not possible  to form a perfect cube
    return "Not Possible";
}

// wrapper for findLargestCubeUtil()
void findLargestCube(long long int n)
{
    // pre process perfect cubes
    vector<string> preProcessedCubes = preProcess(n);

    // convert number n to string
    string num = to_string(n);

    string ans = findLargestCubeUtil(num, preProcessedCubes);

    cout << "Largest Cube that can be formed from "
         << n << " is " << ans << endl;
}

// Driver Code
int main()
{
    long long int n;
    n = 4125;
    findLargestCube(n);

    n = 876;
    findLargestCube(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java code to implement maximum perfect cube
formed after deleting minimum digits */
import java.util.*;
class GFG
{

    // Returns vector of Pre Processed perfect cubes
    static Vector<String> preProcess(int n)
    {
        Vector<String> preProcessedCubes = new Vector<>();
        for (int i = 1; i * i * i <= n; i++)
        {
            int iThCube = i * i * i;

            // convert the cube to String and push into
            // preProcessedCubes vector
            String cubeString = String.valueOf(iThCube);
            preProcessedCubes.add(cubeString);
        }
        return preProcessedCubes;
    }

    /* Utility function for findLargestCube().
    Returns the Largest cube number that can be formed */
    static String findLargestCubeUtil(String num,
            Vector<String> preProcessedCubes)
    {
        // reverse the preProcessed cubes so that we
        // have the largest cube in the beginning
        // of the vector
        Collections.reverse(preProcessedCubes);

        int totalCubes = preProcessedCubes.size();

        // iterate over all cubes
        for (int i = 0; i < totalCubes; i++)
        {
            String currCube = preProcessedCubes.get(i);

            int digitsInCube = currCube.length();
            int index = 0;
            int digitsInNumber = num.length();
            for (int j = 0; j < digitsInNumber; j++)
            {

                // check if the current digit of the cube
                // matches with that of the number num
                if (num.charAt(j) == currCube.charAt(index))
                {
                    index++;
                }

                if (digitsInCube == index)
                {
                    return currCube;
                }
            }
        }

        // if control reaches here, the its
        // not possible to form a perfect cube
        return "Not Possible";
    }

    // wrapper for findLargestCubeUtil()
    static void findLargestCube(int n)
    {
        // pre process perfect cubes
        Vector<String> preProcessedCubes = preProcess(n);

        // convert number n to String
        String num = String.valueOf(n);

        String ans = findLargestCubeUtil(num, preProcessedCubes);

        System.out.println("Largest Cube that can be formed from "
                + n + " is " + ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n;
        n = 4125;
        findLargestCube(n);

        n = 876;
        findLargestCube(n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 code to implement maximum perfect
# cube formed after deleting minimum digits
import math as mt

# Returns vector of Pre Processed
# perfect cubes
def preProcess(n):

    preProcessedCubes = list()
    for i in range(1, mt.ceil(n**(1\. / 3.))):
        iThCube = i**3

        # convert the cube to string and
        # push into preProcessedCubes vector
        cubeString = str(iThCube)
        preProcessedCubes.append(cubeString)

    return preProcessedCubes

# Utility function for findLargestCube().
# Returns the Largest cube number that
# can be formed
def findLargestCubeUtil(num,preProcessedCubes):

    # reverse the preProcessed cubes so
    # that we have the largest cube in
    # the beginning of the vector
    preProcessedCubes = preProcessedCubes[::-1]

    totalCubes = len(preProcessedCubes)

    # iterate over all cubes
    for i in range(totalCubes):
        currCube = preProcessedCubes[i]

        digitsInCube = len(currCube)
        index = 0
        digitsInNumber = len(num)
        for j in range(digitsInNumber):

            # check if the current digit of the cube
            # matches with that of the number num
            if (num[j] == currCube[index]):
                index += 1

            if (digitsInCube == index):            
                return currCube        

    # if control reaches here, the its
    # not possible to form a perfect cube
    return "Not Possible"

# wrapper for findLargestCubeUtil()
def findLargestCube(n):

    # pre process perfect cubes
    preProcessedCubes = preProcess(n)

    num = str(n)

    ans = findLargestCubeUtil(num, preProcessedCubes)

    print("Largest Cube that can be formed from",
                                    n, "is", ans)

# Driver Code
n = 4125
findLargestCube(n)

n = 876
findLargestCube(n)

# This code is contributed
# by mohit kumar 29
```

## C#

```
/* C# code to implement maximum perfect cube
formed after deleting minimum digits */
using System;
using System.Collections.Generic;

class GFG
{

    // Returns vector of Pre Processed perfect cubes
    static List<String> preProcess(int n)
    {
        List<String> preProcessedCubes = new List<String>();
        for (int i = 1; i * i * i <= n; i++)
        {
            int iThCube = i * i * i;

            // convert the cube to String and push into
            // preProcessedCubes vector
            String cubeString = String.Join("",iThCube);
            preProcessedCubes.Add(cubeString);
        }
        return preProcessedCubes;
    }

    /* Utility function for findLargestCube().
    Returns the Largest cube number that can be formed */
    static String findLargestCubeUtil(String num,
            List<String> preProcessedCubes)
    {
        // reverse the preProcessed cubes so that we
        // have the largest cube in the beginning
        // of the vector
        preProcessedCubes.Reverse();

        int totalCubes = preProcessedCubes.Count;

        // iterate over all cubes
        for (int i = 0; i < totalCubes; i++)
        {
            String currCube = preProcessedCubes[i];

            int digitsInCube = currCube.Length;
            int index = 0;
            int digitsInNumber = num.Length;
            for (int j = 0; j < digitsInNumber; j++)
            {

                // check if the current digit of the cube
                // matches with that of the number num
                if (num[j] == currCube[index])
                {
                    index++;
                }

                if (digitsInCube == index)
                {
                    return currCube;
                }
            }
        }

        // if control reaches here, the its
        // not possible to form a perfect cube
        return "Not Possible";
    }

    // wrapper for findLargestCubeUtil()
    static void findLargestCube(int n)
    {
        // pre process perfect cubes
        List<String> preProcessedCubes = preProcess(n);

        // convert number n to String
        String num = String.Join("",n);

        String ans = findLargestCubeUtil(num, preProcessedCubes);

        Console.WriteLine("Largest Cube that can be formed from "
                + n + " is " + ans);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n;
        n = 4125;
        findLargestCube(n);

        n = 876;
        findLargestCube(n);
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to implement maximum perfect
// cube formed after deleting minimum digits

// Returns vector of Pre Processed
// perfect cubes
function preProcess($n)
{

    $preProcessedCubes = array();
    for ($i = 1; $i * $i * $i < $n; $i++)
    {
        $iThCube = $i * $i * $i;

        // convert the cube to string and
        // push into preProcessedCubes vector
        $cubeString = strval($iThCube);
        array_push($preProcessedCubes,$cubeString);
    }
    return $preProcessedCubes;
}

// Utility function for findLargestCube().
// Returns the Largest cube number that
// can be formed
function findLargestCubeUtil($num,$preProcessedCubes)
{
    // reverse the preProcessed cubes so
    // that we have the largest cube in
    // the beginning of the vector
    $preProcessedCubes = array_reverse($preProcessedCubes);

    $totalCubes = count($preProcessedCubes);

    // iterate over all cubes
    for($i = 0; $i < $totalCubes; $i++)
    {
        $currCube = $preProcessedCubes[$i];

        $digitsInCube = strlen($currCube);
        $index = 0;
        $digitsInNumber = strlen($num);
        for ($j = 0; $j < $digitsInNumber; $j++)
        {

            // check if the current digit of the cube
            // matches with that of the number num
            if ($num[$j] == $currCube[$index])
                $index += 1;

            if ($digitsInCube == $index)            
                return $currCube;    
        }
    }
    // if control reaches here, the its
    // not possible to form a perfect cube
    return "Not Possible";
}

// wrapper for findLargestCubeUtil()
function findLargestCube($n)
{

    // pre process perfect cubes
    $preProcessedCubes = preProcess($n);

    $num = strval($n);

    $ans = findLargestCubeUtil($num, $preProcessedCubes);

    print("Largest Cube that can be formed from ".$n." is ".$ans."\n");
}

// Driver Code
$n = 4125;
findLargestCube($n);

$n = 876;
findLargestCube($n)

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
/* Javascript code to implement maximum perfect cube
formed after deleting minimum digits */

    // Returns vector of Pre Processed perfect cubes
    function preProcess(n)
    {
        let preProcessedCubes =[];
        for (let i = 1; i * i * i <= n; i++)
        {
            let iThCube = i * i * i;

            // convert the cube to String and push into
            // preProcessedCubes vector
            let cubeString = (iThCube).toString();
            preProcessedCubes.push(cubeString);
        }
        return preProcessedCubes;
    }

    /* Utility function for findLargestCube().
    Returns the Largest cube number that can be formed */
    function findLargestCubeUtil(num,preProcessedCubes)
    {

        // reverse the preProcessed cubes so that we
        // have the largest cube in the beginning
        // of the vector
        (preProcessedCubes).reverse();

        let totalCubes = preProcessedCubes.length;

        // iterate over all cubes
        for (let i = 0; i < totalCubes; i++)
        {
            let currCube = preProcessedCubes[i];

            let digitsInCube = currCube.length;
            let index = 0;
            let digitsInNumber = num.length;
            for (let j = 0; j < digitsInNumber; j++)
            {

                // check if the current digit of the cube
                // matches with that of the number num
                if (num[j] == currCube[index])
                {
                    index++;
                }

                if (digitsInCube == index)
                {
                    return currCube;
                }
            }
        }

        // if control reaches here, the its
        // not possible to form a perfect cube
        return "Not Possible";
    }

    // wrapper for findLargestCubeUtil()
    function findLargestCube(n)
    {

        // pre process perfect cubes
        let preProcessedCubes = preProcess(n);

        // convert number n to String
        let num = (n).toString();

        let ans = findLargestCubeUtil(num, preProcessedCubes);

        document.write("Largest Cube that can be formed from "
                + n + " is " + ans+"<br>");
    }

    // Driver Code
    let n;
    n = 4125;
    findLargestCube(n);

    n = 876;
    findLargestCube(n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
Largest Cube that can be formed from 4125 is 125
Largest Cube that can be formed from 876 is 8
```

上述算法的时间复杂度为 O(N <sup>1/3</sup> log(N) log(N)是因为 N 中的位数是 Log(N) + 1。