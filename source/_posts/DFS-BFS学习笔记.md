---
title: 'DFS,BFS学习笔记'
date: 2018-07-22 11:18:21
tags: [Java,笔记]
preview: 
---
基础的对图进行搜索的两种算法，自己敲一遍之后发现其实挺简单的，思路也很直观，但依然佩服想出来这个的家伙
<!--more-->
*本文是这个鶸在看完[@卡巴拉的树](https://www.jianshu.com/p/70952b51f0c8)的[图的基本算法（BFS和DFS）](https://www.jianshu.com/p/70952b51f0c8)后写出来的，那篇文章讲的很明了但代码注释不足（其实正文讲明白了也没多大写注释的必要），而且用的是C++，因此这个鶸就在练习性的用Java敲了一遍后顺便补上了注释写成了本文*  

## BFS：广度优先搜索算法
简单来说就是“哎呀我眼镜掉了”然后开始满地摸眼镜的过程。  
先把身边的地方摸个遍顺便记下稍远处还没摸到的地方，身边摸不到的话再去刚刚记下的远处没摸到的地方继续摸，直到摸到为止。  
注释很详细，就不多赘述了，上代码！  
```Java
package com.Laurence_042.BFS;

import java.util.LinkedList;
import java.util.Queue;

public class Demo {
    // 先定义一个代表邻接矩阵的二维数组，忘记||不知道邻接矩阵的先去学离散数学再敲代码
    public static final int[][] MAZE = new int[][] { { 0, 1, 1, 0, 0 }, { 0, 0, 1, 1, 0 }, { 0, 1, 1, 1, 0 },
            { 1, 0, 0, 0, 0 }, { 0, 0, 1, 1, 0 } };
    // 再定义一个标记“已访问过的节点”的boolean数组
    boolean[] visited = new boolean[5];

    //没错，这玩意去掉注释才13条语句，而且还是算上里面的两条System.out.println()的结果
    private void BFS(int start) {
        /*
         * 顺便提前说一下Queue（队列）是个啥， Queue可以被看作一个水管，水从一边进从另一边出。
         * 也就是说，先加入的元素会先被取出来，和Stack（栈）正好相反。 
         * 元素出来的一侧叫做“头”，进去的一侧叫做“尾”。
         * 在Java里可以用offer()方法向尾部加入元素，用poll()方法从头部取出元素。
         * 注意：元素被“取出”代表着它从Queue脱离了，不再存在于Queue中
         */
        // 先定义一个Queue
        Queue<Integer> queue = new LinkedList<>();

        // 先将搜索起点加进Queue里
        queue.offer(start);
        System.out.println("offer:" + start);

        // 只要Queue未空，就代表从起点进行的搜索还未完成
        while (!queue.isEmpty()) {
            // 在这个循环中，start变量代表”正在被访问的节点
            // 现在取出并访问start
            start = queue.poll();
            System.out.println("poll:" + start);
            // 记下“start这个节点已经被访问过了”
            visited[start] = true;
            // do some thing
            // 这里的方法是访问节点是所需要执行的操作，毕竟想搜索什么东西肯定是准备要对它做点啥的对吧（笑）
            visit(start, queue, visited);

            for (int j = 0; j < MAZE[start].length; j++) {
                // 将与“当前正在被访问的节点”邻接的所有未访问过的节点加到Queue中，
                // 准备以新的节点作为“当前正在被访问的节点”进行下一轮操作
                if (MAZE[start][j] == 1 && !visited[j]) {
                    queue.offer(j);
                    System.out.println("offer:" + j);
                    visited[j] = true;
                }
            }
        }
    }

    // 这是个演示方法，实际使用时把这个方法的内容替换为任意想对节点进行的操作即可
    private void visit(int node, Queue<Integer> queue, boolean[] visited) {
        System.out.println("-----------------------------------");
        System.out.println("visiting node: " + node);
        System.out.print("now queue: {");
        for (int i = 0; i < queue.size(); i++) {
            System.out.print(queue.toArray()[i]);
            if (i < queue.size() - 1)
                System.out.print(",");
            else
                System.out.println("}");
        }
        System.out.print("now visited: {");
        for (int i = 0; i < visited.length; i++) {
            System.out.print(visited[i]);
            if (i < visited.length - 1)
                System.out.print(",");
            else
                System.out.println("}");
        }
        System.out.println("-----------------------------------");
    }

    public static void main(String[] args) {
        Demo demo = new Demo();
        for (int i = 0; i < 5; i++) {
            if (demo.visited[i])
                continue;
            System.out.println("node "+i+" isn't visited, new BFS from node "+i);
            demo.BFS(i);
        }

    }

}
```
运行结果：
```
node 0 isn't visited, new BFS from node 0
offer:0
poll:0
-----------------------------------
visiting node: 0
now queue: {now visited: {true,false,false,false,false}
-----------------------------------
offer:1
offer:2
poll:1
-----------------------------------
visiting node: 1
now queue: {2}
now visited: {true,true,true,false,false}
-----------------------------------
offer:3
poll:2
-----------------------------------
visiting node: 2
now queue: {3}
now visited: {true,true,true,true,false}
-----------------------------------
poll:3
-----------------------------------
visiting node: 3
now queue: {now visited: {true,true,true,true,false}
-----------------------------------
node 4 isn't visited, new BFS from node 4
offer:4
poll:4
-----------------------------------
visiting node: 4
now queue: {now visited: {true,true,true,true,true}
-----------------------------------
```

## DFS：深度优先搜索算法
相对而言，深度优先的想法稍微不那么浅显了，嗯，没错，只是“稍微”不那么浅显而已，还是挺浅显的。  
话说，你知道“二叉树”吗？用那个数据结构存储的数据查找起来还是挺快的，利用它的变种“红黑树”还能进一步提高查找事件的稳定性，不过这都是题外话了。我想说的是，“二叉树”的遍历算法和DFS有异曲同工之妙。简言之就是下面的思想：  
> 1.我知道只有一个元素，或两个元素，甚至三个元素的时候该怎么做
> 2.这个问题的集合里有一堆的元素（比如遍历某个有向图里所有节点），我被搞糊涂了，不知道该怎么做
> 3.这个问题集合里的元素貌似可以进行相似的分割（比如有向图里所有节点可分为“当前节点”和“剩下的它旁边的节点”
> 4.那就对作为起始的随便一个“这个元素”执行某个方法，这样的话这个节点就被搞定了，剩下的节点就是下一次执行方法要处理的了（比如（访问当前结点，并对周围节点执行（访问当前结点，并对周围节点执行（访问当前结点，并对周围节点执行（······（**whoops！**）······）））））
> 5.这样下去总能再最深处（一堆括号的最内层）出现1.处的情况（没错就是那个 **whoops！**），也就是······这个问题可解了！然后这个“最内层的括号”就可以被打开，“次外层的括号”就变成了“最内层的括号”！这时候你只要继续下去，当最外层的括号也被解开的时候，问题解决了！
```Java
package com.Laurence_042.DFS;

public class Demo {
    // 先定义一个代表邻接矩阵的二维数组，忘记||不知道邻接矩阵的先去学离散数学再敲代码
    public static final int[][] MAZE = new int[][] { { 0, 1, 1, 0, 0 }, { 0, 0, 1, 1, 0 }, { 0, 1, 1, 1, 0 },
            { 1, 0, 0, 0, 0 }, { 0, 0, 1, 1, 0 } };
    // 再定义一个标记“已访问过的节点”的boolean数组
    boolean[] visited = new boolean[5];

    /*
     * 没错，这个算法更短，才5条语句（笑）
     * 这是个典型的递归思想：
     * 如果我只有一个节点，访问完这个节点就全部访问完了。
     * 如果这个节点旁边还有节点，就"访问完这个节点"后再对旁边的节点依次"访问完这个节点"，
     * 这样一直往深的访问总有到头的时候，这时候只要执行"如果我只有一个节点"时候的操作就万事大吉了
     * 
     * 简言之，大事化小，小事化了。不过除了递归的时候外，我平时都超烦这句话的（苦笑）
     */
    private void DFS(int start) {
        visited[start]=true;
        visit(start, visited);
        for (int i = 0; i < MAZE.length; i++) {
            if (MAZE[start][i] == 1 && !visited[i])
                DFS(i);
        }
    }

    // 这是个演示方法，实际使用时把这个方法的内容替换为任意想对节点进行的操作即可
    private void visit(int node, boolean[] visited) {
        System.out.println("-----------------------------------");
        System.out.println("visiting node: " + node);
        System.out.print("now visited: {");
        for (int i = 0; i < visited.length; i++) {
            System.out.print(visited[i]);
            if (i < visited.length - 1)
                System.out.print(",");
            else
                System.out.println("}");
        }
        System.out.println("-----------------------------------");
    }

    public static void main(String[] args) {
        Demo demo = new Demo();
        for (int i = 0; i < 5; i++) {
            if (demo.visited[i])
                continue;
            System.out.println("node " + i + " isn't visited, new DFS from node " + i);
            demo.DFS(i);
        }

    }

}
```
运行结果：
```
node 0 isn't visited, new DFS from node 0
-----------------------------------
visiting node: 0
now visited: {true,false,false,false,false}
-----------------------------------
-----------------------------------
visiting node: 1
now visited: {true,true,false,false,false}
-----------------------------------
-----------------------------------
visiting node: 2
now visited: {true,true,true,false,false}
-----------------------------------
-----------------------------------
visiting node: 3
now visited: {true,true,true,true,false}
-----------------------------------
node 4 isn't visited, new DFS from node 4
-----------------------------------
visiting node: 4
now visited: {true,true,true,true,true}
-----------------------------------
```
So······这个才5条语句，这么好写而且输出结果没啥问题，为啥不只用DFS还要学BFS呢?  
Well,这个是递归，有向图越大，它到达“最内层”花的时间就越长，更麻烦的是，随着调用层数的增加，调用外层时消耗掉内存无法被释放，因此当有向图大到一定程度时，这个算法会花大量时间占满内存而最后一个解都弄不出来并随着一句“内存满了”而异常终止。
那为啥不只学BFS呢？  
拜托，你如果只是解个自行车的追及问题（小范围问题）还有必要用相对论的时空相对性（保险但麻烦的算法）嘛？（笑）
<!--more-->