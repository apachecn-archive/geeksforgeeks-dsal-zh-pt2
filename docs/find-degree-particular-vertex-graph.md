# 求图中特定顶点的度数

> 原文:[https://www . geesforgeks . org/find-degree-special-vertex-graph/](https://www.geeksforgeeks.org/find-degree-particular-vertex-graph/)

给定一个图 G(V，E)作为[邻接矩阵表示](https://www.geeksforgeeks.org/graph-and-its-representations/)和一个顶点，求图中顶点 V 的度。

**示例:**

```
0-----1
|\    |
|  \  |
|    \|
2-----3
Input : ver = 0
Output : 3

Input : ver = 1
Output : 2
```

算法:-

```
1\. Create the graphs adjacency matrix from src to des 
2\. For the given vertex then check if 
   a path from this vertices to other exists then
   increment the degree.
3\. Return degree 
```

下面是该方法的实现。

## C++

```
// CPP program to find degree of a vertex.
#include<iostream>
using namespace std;

// structure of a graph
struct graph     
{
    // vertices
    int v;         

    // edges
    int e;         

    // direction from src to des
    int **dir;     
};

// Returns degree of ver in given graph
int findDegree(struct graph *G, int ver)
{    
    // Traverse through row of ver and count
    // all connected cells (with value 1)
    int degree = 0;         
    for (int i=0; i<G->v; i++)     

        // if src to des is 1 the degree count
        if (G-> dir[ver][i] == 1) 
            degree++;             

    // below line is to account for self loop in graph
    // check sum of degrees in graph theorem
    if(G-> dir[ver][ver] == 1)
          degree++;
    return degree;         
}

struct graph *createGraph(int v,int e)
{   
    // G is a pointer of a graph
    struct graph *G = new graph; 

    G->v = v;
    G->e = e;

    // allocate memory
    G->dir = new int*[v];

    for (int i = 0;i < v;i++)
        G->dir[i] = new int[v];

    /*  0-----1
        | \   |
        |  \  |
        |   \ |
        2-----3     */

    //direction from 0
    G->dir[0][1]=1;
    G->dir[0][2]=1;
    G->dir[0][3]=1;

    //direction from 1
    G->dir[1][0]=1;
    G->dir[1][3]=1;

    //direction from 2
    G->dir[2][0]=1;
    G->dir[2][3]=1;

    //direction from 3
    G->dir[3][0]=1;
    G->dir[3][1]=1;
    G->dir[3][2]=1;

    return G;

}

// Driver code
int main()
{
    int vertices = 4;
    int edges = 5;
    struct graph *G = createGraph(vertices, edges);

    // loc is find the degree of 
    // particular vertex
    int ver = 0; 

    int degree = findDegree(G, ver);
    cout << degree << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find degree of a vertex.

class DegreeOfVertex 
{
    //Structure of Graph
    static class Graph
    {
        // vertices and edges
        int v, e;
        int[][] dir;

        //Graph Constructor
        Graph(int v, int e) {
            this.v = v;
            this.e = e;
            dir = new int[v][];
            for (int i = 0; i < v; i++)
                dir[i] = new int[v];
        }
    }
    static Graph createGraph(int v, int e) 
    {
        Graph G = new Graph(v, e);

     /* 0-----1
        | \   |
        |  \  |
        |   \ |
        2-----3 */

        //direction from 0
        G.dir[0][1] = 1;
        G.dir[0][2] = 1;
        G.dir[0][3] = 1;

        //direction from 1
        G.dir[1][0] = 1;
        G.dir[1][3] = 1;

        //direction from 2
        G.dir[2][0] = 1;
        G.dir[2][3] = 1;

        //direction from 3
        G.dir[3][0] = 1;
        G.dir[3][1] = 1;
        G.dir[3][2] = 1;

        return G;
    }

    static int findDegree(Graph G, int ver) 
    {
        int degree = 0;
        for (int i = 0; i < G.v; i++) {
            if (G.dir[ver][i] == 1)
                degree++;
        }

          // below line is to account for self loop in graph
        // check sum of degrees in graph theorem 
        if(G.dir[ver][ver] == 1) degree++;
        return degree;
    }

    // Driver code
    public static void main(String[] args)
    {
        int vertices = 4;
        int edges = 5;

        // Creating a Graph
        Graph G = createGraph(vertices, edges);

        int ver = 0;

        // Function calling
        int degree = findDegree(G, ver);
        System.out.println(degree);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find degree of a vertex.

# Structure of Graph
class Graph:

    # vertices and edges
    v = None
    e = None
    diri = []

    # Graph Constructor
    def __init__(self, v, e):
        self.v = v
        self.e = e
        self.diri = [[0 for i in range(v)] 
                        for j in range(v)]

def createGraph(v, e):
    G = Graph(v, e)

    # /* 0-----1
    # | \ |
    # | \ |
    # | \ |
    # 2-----3 */

    # direction from 0
    G.diri[0][1] = 1
    G.diri[0][2] = 1
    G.diri[0][3] = 1

    # direction from 1
    G.diri[1][0] = 1
    G.diri[1][3] = 1

    # direction from 2
    G.diri[2][0] = 1
    G.diri[2][3] = 1

    # direction from 3
    G.diri[3][0] = 1
    G.diri[3][1] = 1
    G.diri[3][2] = 1

    return G

def findDegree(G, ver):
    degree = 0
    for i in range(G.v):
        if G.diri[ver][i] == 1:
            degree += 1
    if G.diri[ver][ver] == 1: 
        degree += 1
    return degree

# Driver Code
if __name__ == "__main__":

    vertices = 4
    edges = 5

    # Creating a Graph
    G = createGraph(vertices, edges)

    ver = 0

    # Function calling
    degree = findDegree(G, ver)
    print(degree)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find degree of a vertex.
using System;

class GFG 
{
    // Structure of Graph
    public class Graph
    {
        // vertices and edges
        public int v, e;
        public int[,] dir;

        //Graph Constructor
        public Graph(int v, int e)
        {
            this.v = v;
            this.e = e;
            dir = new int[v,v];
        }
    }

    static Graph createGraph(int v, int e) 
    {
        Graph G = new Graph(v, e);

        /* 0-----1
            | \ |
            | \ |
            | \ |
            2-----3 */

        // direction from 0
        G.dir[0, 1] = 1;
        G.dir[0, 2] = 1;
        G.dir[0, 3] = 1;

        // direction from 1
        G.dir[1, 0] = 1;
        G.dir[1, 3] = 1;

        // direction from 2
        G.dir[2, 0] = 1;
        G.dir[2, 3] = 1;

        //direction from 3
        G.dir[3, 0] = 1;
        G.dir[3, 1] = 1;
        G.dir[3, 2] = 1;

        return G;
    }

    static int findDegree(Graph G, int ver) 
    {
        int degree = 0;
        for (int i = 0; i < G.v; i++) 
        {
            if (G.dir[ver,i] == 1)
                degree++;
        }
        return degree;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int vertices = 4;
        int edges = 5;

        // Creating a Graph
        Graph G = createGraph(vertices, edges);

        int ver = 0;

        // Function calling
        int degree = findDegree(G, ver);
        Console.WriteLine(degree);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find degree of a vertex.
class Graph
{
    constructor(v,e)
    {
        // Vertices
        this.v = v;

        // Edges
        this.e = e;

        // Direction from src to des
        this.dir = new Array(v);

        for(let i = 0; i < v; i++)
            this.dir[i] = new Array(v);
    }
}

function createGraph(v,e)
{
    let G = new Graph(v, e);

     /* 0-----1
        | \   |
        |  \  |
        |   \ |
        2-----3 */

        // Direction from 0
        G.dir[0][1] = 1;
        G.dir[0][2] = 1;
        G.dir[0][3] = 1;

        // Direction from 1
        G.dir[1][0] = 1;
        G.dir[1][3] = 1;

        // Direction from 2
        G.dir[2][0] = 1;
        G.dir[2][3] = 1;

        // Direction from 3
        G.dir[3][0] = 1;
        G.dir[3][1] = 1;
        G.dir[3][2] = 1;

        return G;
}

// Returns degree of ver in given graph
function findDegree(G, ver)
{

    // Traverse through row of ver and count
    // all connected cells (with value 1)
    let degree = 0;
    for(let i = 0; i < G.v; i++)
    {

        // If src to des is 1 the degree count
        if (G.dir[ver][i] == 1)
            degree++;
    }

    // Below line is to account for self 
    // loop in graph check sum of degrees
    // in graph theorem
    if (G.dir[ver][ver] == 1) 
        degree++;

    return degree;
}

// Driver code
let vertices = 4;
let edges = 5;

// Creating a Graph
let G = createGraph(vertices, edges);

// loc is find the degree of 
// particular vertex
let ver = 0;

// Function calling
let degree = findDegree(G, ver);
document.write(degree + "<br>");

// This code is contributed by rag2127

</script>
```

**Output**

```
3
```