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
