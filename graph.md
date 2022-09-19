## topological-sort
```
    def canFinishBFS(self, n, prerequisites):
        G = [[] for i in range(n)]
        inDegree = [0] * n

        for i, j in prerequisites:
            # [1, 0] means 1 depends on 0
            # so 1 -> 0
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
