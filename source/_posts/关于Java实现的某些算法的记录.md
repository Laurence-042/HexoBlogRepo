---
title: 关于Java实现的某些算法的记录
date: 2018-07-09 22:54:08
tags: [Java,笔记,不定期更新]
preview: https://raw.githubusercontent.com/Laurence-042/Resources/master/jpg/other/java.jpg
---
做练习时看到的一些自认为对自己这种小白有不小启发性的算法，由于最近主要用Java，所以绝大部分都是Java语法。
<!--more-->
# 搜索算法
### 丑数
设计一个算法，找出只含素因子2，3，5 的第 n 小的数。  
符合条件的数如：1, 2, 3, 4, 5, 6, 8, 9, 10, 12...  
```java
// O(n) scan
class Solution {
    /**
     * @param n an integer
     * @return the nth prime number as description.
     */
    public int nthUglyNumber(int n) {
        List<Integer> uglys = new ArrayList<Integer>();
        uglys.add(1);
        
        int p2 = 0, p3 = 0, p5 = 0;
        // p2, p3 & p5 share the same queue: uglys

        for (int i = 1; i < n; i++) {
            int lastNumber = uglys.get(i - 1);
            while (uglys.get(p2) * 2 <= lastNumber) p2++;
            while (uglys.get(p3) * 3 <= lastNumber) p3++;
            while (uglys.get(p5) * 5 <= lastNumber) p5++;
            
            uglys.add(Math.min(
                Math.min(uglys.get(p2) * 2, uglys.get(p3) * 3),
                uglys.get(p5) * 5
            ));
        }

        return uglys.get(n - 1);
    }
};
```
依次生成，此处值得注意的是生成方式：使用因子进行累乘的方式。  

### 子集
输入一个集合，生成其所有的子集
```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    Arrays.sort(nums);
    backtrack(list, new ArrayList<>(), nums, 0);
    return list;
}
 
private void backtrack(List<List<Integer>> list , List<Integer> tempList, int [] nums, int start){
    list.add(new ArrayList<>(tempList));
    for(int i = start; i < nums.length; i++){
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        tempList.remove(tempList.size() - 1);
    }
}
```
比较基础的一个递归技巧，此处值得注意的是递归的应用方式。  
<!--more-->