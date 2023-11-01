## Mimimum Height Trees
[310 Mimimum Height Trees](https://leetcode.com/problems/minimum-height-trees/description/)

## Description

A tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.

Given a tree of n nodes labelled from 0 to n - 1, and an array of n - 1 edges where edges[i] = [ai, bi] indicates that there is an undirected edge between the two nodes ai and bi in the tree, you can choose any node of the tree as the root. When you select a node x as the root, the result tree has height h. Among all possible rooted trees, those with minimum height (i.e. min(h))  are called minimum height trees (MHTs).

Return a list of all MHTs' root labels. You can return the answer in any order.

The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

## Code

```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        # get the longest path and we can get the middle points
        if n == 1:
            return [0]
        elif n == 2:
            return [0,1]
        tree = [set() for i in range(n)]
        for edge in edges:
            tree[edge[0]].add(edge[1])
            tree[edge[1]].add(edge[0])
        nodes = [i for i in range(n)]

        # delete those have
        while n > 2: 
            cut_nodes = []
            for node in nodes:
                if len(tree[node]) == 1:
                    # not leaf
                    cut_nodes.append(node)     
                    n = n - 1
            for node in cut_nodes:
                tree[tree[node].pop()].remove(node)

            nodes = set(nodes) - set(cut_nodes)            
        return nodes

```

## Best 

```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if n <= 2:
            return [i for i in range(n)]
        
        neighbours = [set() for _ in range(n)]
        for a, b in edges:
            neighbours[a].add(b)
            neighbours[b].add(a)
        
        leaves = []
        for node in range(n):
            if len(neighbours[node]) == 1:
                leaves.append(node)
        
        remaining_nodes = n
        while remaining_nodes > 2:
            remaining_nodes -= len(leaves)
            new_leaves = []
            while leaves:
                leaf = leaves.pop()
                neighbour = neighbours[leaf].pop()
                neighbours[neighbour].remove(leaf)
                if len(neighbours[neighbour]) == 1:
                    new_leaves.append(neighbour)
            
            leaves = new_leaves
        
        return leaves

```

## Analysis
- Time complexity : O(N^2) -- Worst Case: a line
- Space complexity: O(N) -- Not sure
- Note: The two version use the same idea, that is: find the leafs(only connecting to one another node) and delete them, repete the progress until there are only 1 or 2 nodes. The latter combines some loop operations to accelerate. It's easy to run out of time for this question (in the worst case). 

**WHY**: because to get Mimimum Height Trees, the top must be in the middle of the longest path in this tree. 