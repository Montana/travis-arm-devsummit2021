# devsummit2021
DevSummit 2021 .travis.yml 

I've made a `.travis.yml` file specifically for ARM DevSummit 2021, specifically showing how a BFS builds on each architecture, `arm64` and `arm64-graviton`.

The BFS I created: 

```python
import collections

# Breadth-First search by Montana Mendy

def shortest_distance(grid):
    if not grid or not grid[0]:
        return -1

    matrix = [[[0,0] for i in range(len(grid[0]))] for j in range(len(grid))]

    count = 0    # count how many building we have visited
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == 1:
                bfs(grid, matrix, i, j, count)
                count += 1

    res = float('inf')
    for i in range(len(matrix)):
        for j in range(len(matrix[0])):
            if matrix[i][j][1]==count:
                res = min(res, matrix[i][j][0])

    return res if res!=float('inf') else -1

def bfs(grid, matrix, i, j, count):
    q = [(i, j, 0)]
    while q:
        i, j, step = q.pop(0)
        for k, l in [(i-1,j), (i+1,j), (i,j-1), (i,j+1)]:
            # only the position be visited by count times will append to queue
            if 0<=k<len(grid) and 0<=l<len(grid[0]) and \
                    matrix[k][l][1]==count and grid[k][l]==0:
                matrix[k][l][0] += step+1
                matrix[k][l][1] = count+1
                q.append((k, l, step+1))
 ```
