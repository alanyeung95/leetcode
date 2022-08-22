## meeting rooms
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
