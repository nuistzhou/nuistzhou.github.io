---
layout:     post
title:      "Number of Islands"
subtitle:   " \"Algorithms\""
date:       2020-05-12 22:00:00
author:     "Ping"
header-img: "img/post-bg-leetcode.jpg"
catalog: true
tags:
    - Technology
    - Algorithm
    - Leetcode
---

## Description
Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

__Example 1__:

```
Input:
11110
11010
11000
00000

Output: 1
```

__Example 2__:
```
Input:
11000
11000
00100
00011

Output: 3
```


## Approach 1 

A recursive way of checking every element and its four neighbors of the grid to see if it is '1' and mark as '0' if so.

```python
class Solution:
    def isValid(self, grid, x, y):
        if x < 0 or y < 0 or x >= len(grid) or y >= len(grid[0]):
            return False
        return True
    
    def dfs(self, grid, x, y):
        grid[x][y] = "0"
        neighbour_vec = [(0, -1), (0, 1), (-1, 0), (1, 0)]
        for neighbour in neighbour_vec:
            neigh_x = x + neighbour[0]
            neigh_y = y + neighbour[1]
            if self.isValid(grid, neigh_x, neigh_y) and grid[neigh_x][neigh_y] == "1":
                self.dfs(grid, neigh_x, neigh_y)
        
    def numIslands(self, grid: List[List[str]]) -> int:
        count = 0
        if not grid:
            return 0
        x_dim = len(grid[0])
        y_dim = len(grid)
        for i in range(y_dim):
            for j in range(x_dim):
                if grid[i][j] == "1":
                    self.dfs(grid, i, j)
                    count += 1
        return count
```
