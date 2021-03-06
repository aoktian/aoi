## 前提假设

**本文讨论的AOI，场景中的游戏对象均有碰撞。**

**因此，不存在所有游戏对象重叠在一起的情况。**


## 讨论内容

本文主要讨论以下AOI算法：
  - 基于Tile的灯塔算法
  - 基于QuadTree算法


并按以下方面来比较算法优劣：
  - 占用内存
  - Add操作
  - Leave操作
  - Move操作
  - AOI操作

## 基础算法对比

算法          | 占用内存  | Add | Leave | Move | AOI | 说明
--------------|----------|-----|-------|------|-----|------
Tile算法      | O(W*H) | O(1)   | O(1) | O(T) | O(T)<br> | 2维数组。<br>第1维表达所有Tile；<br>第2维表达每个Tile上的游戏对象列表
QuadTree算法  | O(N)     | O(logN) | O(1) | 通常O(L)；<br>跨边界O(logN)+O(L) | O(logN) + O(L) | 四叉树。<br>叶子节点上有游戏对象列表；<br>叶子节点游戏对象超过指定数量限制，则分裂子节点<br>叶子节点有游戏对象Leave，可能触发4兄弟节点合并<br>节点边界上的游戏对象放在父节点上<br>AOI从Root节点开始做广度遍历

其中：
- N为游戏对象数量。
- W为地图宽
- H为地图长
- T为Tile上能容纳的游戏对象数量
- L为叶子节点区域能容纳的游戏对象数量

有上可以看出：
  - Tile算法优势在于CPU消耗低，缺点是内存占用大
  - QuadTree算法优势在于内存占用低，缺点是CPU消耗大

总体而言，QuadTree算法占优势，特别是人数少，且地图很大的情况。
