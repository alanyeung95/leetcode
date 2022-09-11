## graph-valid-tree
### ans
ref: https://algomonster.medium.com/leetcode-261-graph-valid-tree-f27c212c1db1
```
    def validTree(self, n: int, edges: List[List[int]]) -> bool:
        from collections import defaultdict
        graph = defaultdict(list)
        
        # build the graph
        for src, dest in edges:
            graph[src].append(dest)
            graph[dest].append(src)
            
        visited = set()
        def dfs(root, parent): # returns true if graph has no cycle
            visited.add(root)
            for node in graph[root]:
                if node == parent: # trivial cycle, skip
                    continue
                if node in visited:
                    return False
            
                if not dfs(node, root):
                    return False
            return True
        
        return dfs(0, -1) and len(visited) == n
```

## boundary-of-binary-tree
### ans
https://www.geeksforgeeks.org/boundary-traversal-of-binary-tree/#:~:text=The%20left%20boundary%20is%20defined,left%20boundary%20or%20right%20boundary.

## alien-dictionary
### ans
```
# DFS solution.
class Solution(object):
    def alienOrder(self, words):
        """
        :type words: List[str]
        :rtype: str
        """
        # Find ancestors of each node by DFS.
        nodes, ancestors = set(), {}
        for i in range(len(words)):
            for c in words[i]:
                nodes.add(c)
        for node in nodes:
            ancestors[node] = []
        for i in range(1, len(words)):
            if (len(words[i-1]) > len(words[i]) and
                    words[i-1][:len(words[i])] == words[i]):
                return ""
            self.findEdges(words[i - 1], words[i], ancestors)

        # Output topological order by DFS.
        result = []
        visited = {}
        for node in nodes:
            if self.topSortDFS(node, node, ancestors, visited, result):
                return ""

        return "".join(result)

    # Construct the graph.
    def findEdges(self, word1, word2, ancestors):
        min_len = min(len(word1), len(word2))
        for i in range(min_len):
            if word1[i] != word2[i]:
                ancestors[word2[i]].append(word1[i])
                # one character is enough, the ordering behind are meaningless
                break

    # Topological sort, return whether there is a cycle.
    def topSortDFS(self, root, node, ancestors, visited, result):
        if node not in visited:
            visited[node] = root
            for ancestor in ancestors[node]:
                if self.topSortDFS(root, ancestor, ancestors, visited, result):
                    return True
            result.append(node)
        elif visited[node] == root:
            # Visited from the same root in the DFS path.
            # So it is cyclic.
            return True
        return False

instance = Solution()
print(instance.alienOrder([
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]))
```

## two-sum-less-than-k
### ans
https://wentao-shao.gitbook.io/leetcode/two-pointers/1099.two-sum-less-than-k

## path-with-maximum-minimum-value
### ans
https://www.junhaow.com/lc/problems/heap/1102_path-with-maximum-minimum-value.html

## design-tic-tac-toe
### ans
https://aaronice.gitbook.io/lintcode/data_structure/design-tic-tac-toe

## design-search-autocomplete-system

### ans
https://aaronice.gitbook.io/lintcode/data_structure/design-search-autocomplete-system

## minimum-cost-to-connect-sticks
```
You have some sticks with positive integer lengths.

You can connect any two sticks of lengths X and Y into one stick by paying a cost of X + Y.  You perform this action until there is one stick remaining.

Return the minimum cost of connecting all the given sticks into one stick in this way.

Example 1:

Input: sticks = [2,4,3]
Output: 14
Example 2:

Input: sticks = [1,8,3,5]
Output: 30
```
### ans
```
def minCost(arr):
    # Create a priority queue out of the
    # given list
    heapq.heapify(arr)
 
    # Initialize result
    res = 0
 
    # While size of priority queue
    # is more than 1
    while(len(arr) > 1):
 
        # Extract shortest two ropes from arr
        first = heapq.heappop(arr)
        second = heapq.heappop(arr)
 
        # Connect the ropes: update result
        # and insert the new rope to arr
        res += first + second
        heapq.heappush(arr, first + second)
 
    return res
```

## meeting-rooms
```
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), determine if a person could attend all meetings.

Example 1:

Input: [[0,30],[5,10],[15,20]]
Output: false
Example 2:

Input: [[7,10],[2,4]]
Output: true
```

### ans
```
class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b){return a[0] < b[0];});
        for (int i = 1; i < intervals.size(); ++i) {
            if (intervals[i][0] < intervals[i - 1][1]) {
                return false;
            }
        }
        return true;
    }
};
```

## meeting-rooms-ii
```
Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

Example 1:

Input: 
[[0, 30],[5, 10],[15, 20]]

Output: 2
Example 2:

Input: [[7,10],[2,4]]
Output: 1
```
### ans
ref: https://www.cnblogs.com/grandyang/p/5244720.html
```
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        map<int, int> m;
        for (auto a : intervals) {
            ++m[a[0]];
            --m[a[1]];
        }
        int rooms = 0, res = 0;
        for (auto it : m) {
            res = max(res, rooms += it.second);
        }
        return res;
    }
};
```
```
class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b){ return a[0] < b[0]; });
        priority_queue<int, vector<int>, greater<int>> q;
        for (auto interval : intervals) {
            if (!q.empty() && q.top() <= interval[0]) q.pop();
            q.push(interval[1]);
        }
        return q.size();
    }
};
```

## reverse-words-in-a-string-ii
```
Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

For example,
Given s = "the sky is blue",
return "blue is sky the".

Could you do it in-place without allocating extra space?
```
### ans
```
   void reverseWords(vector<char>& s) {
      reverse(s.begin(), s.end());
      int j = 0;
      int n = s.size();
      for(int i = 0; i < n; i++){
         if(s[i] == ' '){
            reverse(s.begin() + j, s.begin() + i);
            j = i + 1;
         }
      }
      reverse(s.begin() + j, s.begin() + n);
   }
```
