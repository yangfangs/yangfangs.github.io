---
layout: post
title: 顶点覆盖（vertex cover）
categories: Algorithm
description: 顶点覆盖问题
keywords: 算法，图，顶点，
---

# 顶点覆盖（Vertex cover）
　　在图论的数学学科中，图的顶点覆盖（有时是节点覆盖）是一组顶点的集合，使得图的每个边缘至少与集合中的一个顶点相连接。
找到最小顶点覆盖的问题是计算机科学中的经典优化问题，也是NP-hard最优问题近似算法的一个典型例子。

![vertex cover](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0a/Couverture_de_sommets.svg/220px-Couverture_de_sommets.svg.png)

> 图来自于wiki


## 顶点覆盖问题（vertex cover problem）
顶点覆盖问题是在给定的无向图中找出顶点覆盖的最小值，尽管我们不能够在多项式时间里找出一个图G中最优的顶点覆盖，
但是我们可以有效的找出一个顶点覆盖的近似最优解。

例如：给定图G和正整数K

问题: G是否有顶点覆盖的大小至多为K?

## 问题解决

对于这类问题没有很精确的算法来解决，只有一些近似的算法解决这类问题。
2-approximation就是其中一种近似算法来解决这类问题，能找到至多不会超过最优顶点覆盖的2倍的顶点覆盖的集合，算法时间复杂度 O(E+V)。

## 2-approximation近似算法

```
1 C = {}
2 E' = G.E
3 while E != {};
4   let (u,v) be an arbitrary edge of E'
5   C = C U {u,v}
6   remove from E' every edge incident on either u or v
7 return C
```

* 其中C为Vertex cover，G为图，E'为图的一个拷贝，(u,v)为边。

## java实现

```java
import java.util.Iterator;
import java.util.LinkedList;

class Graph
{
    private int V;
    private LinkedList<Integer> adj[];
    //构造函数
    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];     
        
        for (int i=0; i<v; ++i)
            adj[i] = new LinkedList();
    }
    //用邻接表来表示图
    void addEdge(int v, int w)
    {
        adj[v].add(w);
        adj[w].add(v);
    }
    void printVertexCover()
    {
        //初始化所有点都没有被遍历
        boolean visited[] = new boolean[V];
        for (int i=0; i<V; i++)
            visited[i] = false;
        Iterator<Integer> i;
        //遍历所有的点
        for (int u=0; u<V; u++)
        {
            if (visited[u] == false)
            {
                //遍历与当前节点相链接的点
                i = adj[u].iterator();
                while (i.hasNext())
                {
                    int v = i.next();
                    //对已经访问的点进行标记
                    if (visited[v] == false){
                        visited[v] = true;
                        visited[u] = true;
                        break;
                    }
                }
            }
        }
        //顶点覆盖的结果C
        for (int j=0; j<V; j++)
            if (visited[j])
                System.out.print(j+" ");
        System.out.println();
        for (boolean v: visited)
            System.out.print(v+" ");
        System.out.println();
        //邻接表
        for (LinkedList<Integer> str: adj)
            System.out.println(str);
    }
    
    public static void main(String args[])
    {
        Graph g = new Graph(7);
        g.addEdge(0, 1);
        g.addEdge(1, 2);
        g.addEdge(2, 3);
        g.addEdge(2, 4);
        g.addEdge(4, 5);
        g.addEdge(3, 5);
        g.addEdge(3, 4);
        g.addEdge(3, 6); 
        
        g.printVertexCover();
    }
}

```

##run

```
0 1 2 3 4 5 
true true true true true true false 
[1]
[0, 2]
[1, 3, 4]
[2, 5, 4, 6]
[2, 5, 3]
[4, 3]
[3]
```

## 参考：

* [GeeksforGeeks](http://www.geeksforgeeks.org/vertex-cover-problem-set-1-introduction-approximate-algorithm-2/)

* [Wiki Vertex cover](https://en.wikipedia.org/wiki/Vertex_cover)

* [ClRS book](https://www.flipkart.com/introduction-algorithms-english-3rd/p/itmdwxyrafdburzg?pid=9788120340077&affid=sandeepgfg)

* [PPT](http://www.cs.vassar.edu/~walter/cs241index/lectures/PDF/approx.pdf)