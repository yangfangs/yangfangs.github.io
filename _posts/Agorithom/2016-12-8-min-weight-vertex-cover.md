---
layout: post
title: 带权重的顶点覆盖（最小全权重集合）
categories: Algorithm
description: 顶点覆盖问题
keywords: 算法，图，顶点，权重，最小值
---


# 带权重的顶点覆盖问题

在没有权重的图里面顶点覆盖问题，只考虑每个边至少与一个顶点覆盖的点相连，但对有权重的顶点覆盖问题是找出带顶点权重和的最小值。

如图:

![HelloWord](/images/posts/agorithom/min-vertex-cover.svg)

* 最优选取点的集合为{b,c,d,e,f} 其中cost=5 而覆盖近似算法则选取点为{a,e} cost =101，并不是我们想要的。

## 近似算法理论
> [Bar-Yehuda R, Even S. A local-ratio theorem for approximating the weighted vertex cover problem[J]. North-Holland Mathematics Studies, 1985, 109: 27-45.][2]

> [Bar-Yehuda R, Even S. A linear-time approximation algorithm for the weighted vertex cover problem[J]. Journal of Algorithms, 1981, 2(2): 198-203.][1]

##Min-Vertex-Cover算法如下:

```
In Put G(V.E), w.
1 C = {}
2 For every (u,v)∈E;
3   let w'= Min{w(x)|x∈(u,v)}
    For every x ∈ (u,v) do w(x) = w(x)-w'
4 C = {x|w(x)=0}
5 return C
```

* 其中C为Vertex cover，G为图，w为每个点的权重，E'为图的一个拷贝，(u,v)为边。

##java实现

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

class Graph
{
    private int V;
    private LinkedList<Integer> adj[];
    private Map<Integer, Integer> wt = new HashMap<Integer, Integer>();
    private int W;
    //构造函数
    Graph(int v)
    {
        V = v;
        adj = new LinkedList[v];     
        
        for (int i=0; i<v; ++i)
            adj[i] = new LinkedList();
    }
    
    void addWeight(int v, int w)
    {
        wt.put(v, w);
    }
    public int getWeight(int value)
    {
        int weight = wt.get(value);
        return weight;
    }
    
    void addEdge(int v, int w)
    {
        adj[v].add(w);
        adj[w].add(v);
    }

    //取图中的所有，边返回一个list
    public List getEdge()
    {
        List<Integer> list1 = new ArrayList<Integer>();
        List<List<Integer>> outList = new ArrayList<List<Integer>>();
        for (int i=0;i<V; i++){
            for(Integer substr: adj[i]){
                if (!list1.contains(substr)){
                    List<Integer> list2 = new ArrayList<Integer>();
                    list2.add(i);
                    list2.add(substr);

                    outList.add(list2);
                }
                list1.add(i);
                
            }
                
        }
        return outList;
    }
    //实现最小Cost的覆盖近似算法
    public List minVexterCover(Graph g)
    {
        List everyEdge = g.getEdge();
        Map weight = wt;
        List<Integer> outlist= new ArrayList<Integer>();
        
        for (int i=0;i<everyEdge.size();i++){
             
            int min;
            int a = ((List<Integer>) everyEdge.get(i)).get(0);
            int wa = wt.get(a);
            int b = ((List<Integer>) everyEdge.get(i)).get(1);
            int wb = wt.get(b);
            if (wa > wb){
                min = wb;
            }else{
                min = wa;
            }
            wa -= min;
            wb -= min;
            weight.put(a, wa);
            weight.put(b, wb);
        }
        Set<Integer> set = weight.keySet();
        for (int i:set){
            int value = (int) weight.get(i);
            if (value == 0){
                outlist.add(i);
            }else{
                
            }
        }
        
        return outlist;
            
    }
    public static void main(String args[])
    {
        Graph g = new Graph(6);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(0, 3);
        g.addEdge(0, 4);
        g.addEdge(0, 5);
        g.addWeight(0, 100);
        g.addWeight(1, 1);
        g.addWeight(2, 1);
        g.addWeight(3, 1);
        g.addWeight(4, 1);
        g.addWeight(5, 0);
        List minCover = g.minVexterCover(g);
        System.out.println(minCover);
    }
}

```
## 输出结果

```
[1, 2, 3, 4, 5]
```

参考:

[引用1][1]

[引用2][2]


[1]:http://www.cs.technion.ac.il/~reuven/PDF/vc_lp.pdf
[2]: http://www.cs.technion.ac.il/~reuven/PDF/vc_lr.pdf