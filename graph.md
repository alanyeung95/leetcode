## network-delay-time/dijkstras-algorithm
```
    def networkDelayTime(self, times, N, K):
        q, t, adj = [(0, K)], {}, collections.defaultdict(list)
        for u, v, w in times:
            adj[u].append((v, w))

        while q:
            time, node = heapq.heappop(q)
            if node not in t:
                t[node] = time
                for v, w in adj[node]:
                    heapq.heappush(q, (time + w, v))
        return max(t.values()) if len(t) == N else -1
```


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
