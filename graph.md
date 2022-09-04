## topological-sort
```
    def canFinish(self, n, prerequisites):
        G = [[] for i in range(n)]
        inDegree = [0] * n
        for j, i in prerequisites:
            G[i].append(j)
            inDegree[j] += 1
        bfs = [i for i in range(n) if inDegree[i] == 0]
        for i in bfs:
            for j in G[i]:
                inDegree[j] -= 1
                if inDegree[j] == 0:
                    bfs.append(j)
        return len(bfs) == n
```
