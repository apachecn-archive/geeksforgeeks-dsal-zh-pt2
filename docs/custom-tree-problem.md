# 自定义树问题

> 原文:[https://www.geeksforgeeks.org/custom-tree-problem/](https://www.geeksforgeeks.org/custom-tree-problem/)

给你一组链接，例如

```
a ---> b
b ---> c
b ---> d
a ---> e 
```

打印当具有相同字符作为起点和终点的每对链接连接在一起时将形成的树。你必须保持保真度 w.r.t .节点的高度，即距根高度为 n 的节点应打印在同一行或同一列。对于上面给出的一组链接，树打印应该是–

```
-->a
   |-->b
   |   |-->c
   |   |-->d
   |-->e
```

请注意，这些链接不需要形成单一的树；它们可以形成，嗯，一片森林。请考虑以下链接

```
a ---> b
a ---> g
b ---> c
c ---> d
d ---> e
c ---> f
z ---> y
y ---> x
x ---> w
```

输出将跟随森林。

```
-->a
   |-->b
   |   |-->c
   |   |   |-->d
   |   |   |   |-->e
   |   |   |-->f
   |-->g

-->z
   |-->y
   |   |-->x
   |   |   |-->w

```

您可以假设给定的链接只能形成一棵树或树的森林，并且链接之间没有重复。

**解决方案:**思路是维护两个数组，一个数组用于树节点，另一个数组用于树本身(我们称这个数组为林)。节点数组的一个元素包含对应于相应字符的树节点对象。林数组的一个元素包含对应于树的相应根的树对象。

显而易见，关键的部分是在这里创建森林，一旦创建了森林，以所需的格式打印出来就很简单了。要创建林，请使用以下过程–

```
Do following for each input link,
1\. If start of link is not present in node array
     Create TreeNode objects for start character
     Add entries of start in both arrays. 
2\. If end of link is not present in node array
     Create TreeNode objects for start character
     Add entry of end in node array.
3\. If end of link is present in node array.
     If end of link is present in forest array, then remove it
     from there.
4\. Add an edge (in tree) between start and end nodes of link.

```

应该清楚的是，该过程在节点数量和链路数量上以线性时间运行——它只通过链路一次。就字母大小而言，它还需要线性空间。

下面是上述算法的 Java 实现。在下面的实现中，假设字符只是从“a”到“z”的小写字符。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to create a custom tree from a given set of links.

// The main class that represents tree and has main method
public class Tree {

    private TreeNode root;

    /* Returns an array of trees from links input. Links are assumed to 
       be Strings of the form "<s> <e>" where <s> and <e> are starting
       and ending points for the link. The returned array is of size 26
       and has non-null values at indexes corresponding to roots of trees
       in output */
    public Tree[] buildFromLinks(String [] links) {

        // Create two arrays for nodes and forest
        TreeNode[] nodes = new TreeNode[26];  
        Tree[] forest = new Tree[26];          

        // Process each link 
        for (String link : links) {

            // Find the two ends of current link
            String[] ends = link.split(" ");
            int start = (int) (ends[0].charAt(0) - 'a'); // Start node
            int end   = (int) (ends[1].charAt(0) - 'a'); // End node             

            // If start of link not seen before, add it two both arrays
            if (nodes[start] == null) 
            {                
                nodes[start] = new TreeNode((char) (start + 'a'));   

                // Note that it may be removed later when this character is
                // last character of a link. For example, let we first see
                // a--->b, then c--->a.  We first add 'a' to array of trees
                // and when we see link c--->a, we remove it from trees array.
                forest[start] = new Tree(nodes[start]);                                            
            } 

            // If end of link is not seen before, add it to the nodes array
            if (nodes[end] == null)                             
                nodes[end] = new TreeNode((char) (end + 'a'));                                 

            // If end of link is seen before, remove it from forest if 
            // it exists there.
            else forest[end] = null; 

            // Establish Parent-Child Relationship between Start and End
            nodes[start].addChild(nodes[end], end);
        }        
        return forest;
    }

    // Constructor 
    public Tree(TreeNode root) { this.root = root;  }  

    public static void printForest(String[] links)
    {
        Tree t = new Tree(new TreeNode('\0'));
        for (Tree t1 : t.buildFromLinks(links)) {
           if (t1 != null)  
           {  
              t1.root.printTreeIdented("");
              System.out.println("");
           }  
        }
    }        

    // Driver method to test
    public static void main(String[] args) {
        String [] links1 = {"a b", "b c", "b d", "a e"};
        System.out.println("------------ Forest 1 ----------------");
        printForest(links1);       

        String [] links2 = {"a b", "a g", "b c", "c d", "d e", "c f",
                            "z y", "y x", "x w"};
        System.out.println("------------ Forest 2 ----------------");
        printForest(links2);      
    }
}

// Class to represent a tree node
class TreeNode {    
    TreeNode []children;
    char c;

    // Adds a child 'n' to this node
    public void addChild(TreeNode n, int index) { this.children[index] = n;}  

    // Constructor
    public TreeNode(char c) { this.c = c;  this.children = new TreeNode[26];}

    // Recursive method to print indented tree rooted with this node.
    public void printTreeIdented(String indent) {        
            System.out.println(indent + "-->" + c);
            for (TreeNode child : children) {
              if (child != null)  
                child.printTreeIdented(indent + "   |");
            }        
    }    
}
```

## C#

```
// C# program to create a custom tree 
// from a given set of links.
using System;

// The main class that represents tree 
// and has main method
class Tree
{
    public TreeNode root;

    /* Returns an array of trees from links input.  
    Links are assumed to be Strings of the form 
    "<s> <e>" where <s> and <e> are starting and 
    ending points for the link. The returned array is
    of size 26 and has non-null values at indexes 
    corresponding to roots of trees in output */
    public Tree[] buildFromLinks(String [] links) 
    {

        // Create two arrays for nodes and forest
        TreeNode[] nodes = new TreeNode[26]; 
        Tree[] forest = new Tree[26];         

        // Process each link 
        foreach (String link in links) 
        {
            char []sep = {' ',' '};

            // Find the two ends of current link
            String[] ends = link.Split(sep);
            int start = (int) (ends[0][0] - 'a'); // Start node
            int end = (int) (ends[1][0] - 'a'); // End node             

            // If start of link not seen before, 
            // add it two both arrays
            if (nodes[start] == null) 
            {             
                nodes[start] = new TreeNode((char) (start + 'a')); 

                // Note that it may be removed later when 
                // this character is last character of a link. 
                // For example, let we first see a--->b, 
                // then c--->a. We first add 'a' to array 
                // of trees and when we see link c--->a,
                // we remove it from trees array.
                forest[start] = new Tree(nodes[start]);                                         
            } 

            // If end of link is not seen before, 
            // add it to the nodes array
            if (nodes[end] == null)                             
                nodes[end] = new TreeNode((char) (end + 'a'));                                 

            // If end of link is seen before, 
            // remove it from forest if it exists there.
            else forest[end] = null; 

            // Establish Parent-Child Relationship
            // between Start and End
            nodes[start].addChild(nodes[end], end);
        }     
        return forest;
    }

    // Constructor 
    public Tree(TreeNode root) { this.root = root; } 

    public static void printForest(String[] links)
    {
        Tree t = new Tree(new TreeNode('\0'));
        foreach (Tree t1 in t.buildFromLinks(links)) 
        {
            if (t1 != null) 
            { 
                t1.root.printTreeIdented("");
                Console.WriteLine("");
            } 
        }
    }     

    // Driver Code
    public static void Main(String[] args) {
        String [] links1 = {"a b", "b c", "b d", "a e"};
        Console.WriteLine("------------ Forest 1 ----------------");
        printForest(links1);     

        String [] links2 = {"a b", "a g", "b c", "c d", "d e",
                            "c f", "z y", "y x", "x w"};
        Console.WriteLine("------------ Forest 2 ----------------");
        printForest(links2);     
    }
}

// Class to represent a tree node
public class TreeNode 
{ 
    TreeNode []children;
    char c;

    // Adds a child 'n' to this node
    public void addChild(TreeNode n, int index) 
    { 
        this.children[index] = n;
    } 

    // Constructor
    public TreeNode(char c)
    { 
        this.c = c; this.children = new TreeNode[26];
    }

    // Recursive method to print indented tree
    // rooted with this node.
    public void printTreeIdented(String indent) 
    {     
        Console.WriteLine(indent + "-->" + c);
        foreach (TreeNode child in children)
        {
            if (child != null) 
                child.printTreeIdented(indent + " |");
        }     
    } 
}

// This code is contributed by Rajput-Ji
```

**Output:**

```
------------ Forest 1 ----------------
-->a
   |-->b
   |   |-->c
   |   |-->d
   |-->e

------------ Forest 2 ----------------
-->a
   |-->b
   |   |-->c
   |   |   |-->d
   |   |   |   |-->e
   |   |   |-->f
   |-->g

-->z
   |-->y
   |   |-->x
   |   |   |-->w
```

**练习:**
在上面的实现中，假设输入链接的端点来自仅 26 个字符的集合。扩展端点为任意长度字符串的实现。

本文由 **Ciphe** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论