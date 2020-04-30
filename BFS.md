## BFS

##### 1091. Shortest Path in Binary Matrix

In an N by N square grid, each cell is either empty (0) or blocked (1).

A *clear path from top-left to bottom-right* has length `k` if and only if it is composed of cells `C_1, C_2, ..., C_k` such that:

- Adjacent cells `C_i` and `C_{i+1}` are connected 8-directionally (ie., they are different and share an edge or corner)
- `C_1` is at location `(0, 0)` (ie. has value `grid[0][0]`)
- `C_k` is at location `(N-1, N-1)` (ie. has value `grid[N-1][N-1]`)
- If `C_i` is located at `(r, c)`, then `grid[r][c]` is empty (ie. `grid[r][c] == 0`).

Return the length of the shortest such clear path from top-left to bottom-right. If such a path does not exist, return -1.

 

**Example 1:**

```c++
Input: [[0,1],[1,0]]


Output: 2
```

**Example 2:**

```
Input: [[0,0,0],[1,1,0],[1,1,0]]


Output: 4
```

```c++
class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
      std::queue<pair<int,int>> q;
      int steps = 0;
      q.push(make_pair(0,0));
        while(q.size()!=0){
            queue<pair<int,int>> q1;
            steps++;
            while(q.size()!=0){
            pair<int,int> p;
            p=q.front();
            q.pop();
            if(grid[p.first][p.second]==0){
                grid[p.first][p.second]=1;
                if(p.first==grid.size()-1&&p.second==grid.size()-1){
                    return steps;
                }
                else{
                    for(int i=-1;i<=1;i++){
                        for(int j=-1;j<=1;j++){
                            if(i==0&&j==0){continue;}
                            int first = p.first + i;
                            int second = p.second + j;
                            	if(first>=0&&second>=0&&first<grid.size()&&second<grid.size()&&grid[first][second]==0)                                              {
                                q1.push(make_pair(first,second));
                            } 
                        }
                    }
                }
            }
            }
            swap(q,q1);
        }
        return -1;
    }
};
```

##### 279. Perfect Squares

Given a positive integer *n*, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to *n*.

**Example 1:**

```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

**Example 2:**

```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

```c++
class Solution {
public:
     vector<int> squarelist(int n){
        vector<int> squares;
        for(int i=1;i*i<=n;i++){
            squares.push_back(i*i);
        }
        return squares;
    }
    int numSquares(int n) {
        vector<int> squares=squarelist(n);
        queue<int> q,q1;
        q.push(n);
        int num=0;
        while(q.size()!=0){
            num++;
            int size = q.size();
            while(size!=0){
                size--;
                int c = q.front();
                q.pop();
                for(int i=0;i<squares.size();i++){
                    int next=c-squares[i];
                    if(next<0) {break;}
                    if(next==0){return num;}
                    q1.push(next);
                }
            }
            swap(q,q1);
        }
        return num;
    }
};
```

##### 127. Word Ladder<font color = red> (time limit exceed)</font>

Given two words (*beginWord* and *endWord*), and a dictionary's word list, find the length of shortest transformation sequence from *beginWord* to *endWord*, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that *beginWord* is *not* a transformed word.

**Note:**

- Return 0 if there is no such transformation sequence.
- All words have the same length.
- All words contain only lowercase alphabetic characters.
- You may assume no duplicates in the word list.
- You may assume *beginWord* and *endWord* are non-empty and are not the same.

**Example 1:**

```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**

```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

```c++
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> dict(wordList.begin(), wordList.end()), head, tail, *phead, *ptail;
        if (dict.find(endWord) == dict.end()) {
            return 0;
        }
        head.insert(beginWord);
        tail.insert(endWord);
        int ladder = 2;
        while (!head.empty() && !tail.empty()) {
            if (head.size() < tail.size()) {
                phead = &head;
                ptail = &tail;
            } else {
                phead = &tail;
                ptail = &head;
            }
            unordered_set<string> temp;
            for (auto it = phead -> begin(); it != phead -> end(); it++) {    
                string word = *it;
                for (int i = 0; i < word.size(); i++) {
                    char t = word[i];
                    for (int j = 0; j < 26; j++) {
                        word[i] = 'a' + j;
                        if (ptail -> find(word) != ptail -> end()) {
                            return ladder;
                        }
                        if (dict.find(word) != dict.end()) {
                            temp.insert(word);
                            dict.erase(word);
                        }
                    }
                    word[i] = t;
                }
            }
            ladder++;
            std::swap(*phead,temp);
        }
        return 0;
    }
};
```

```c++
class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> dict(wordList.begin(),wordList.end());
        queue<string> q;
        q.push(beginWord);
        int steps = 1;
        while(q.size()!=0){
            steps++;
            int size = q.size();
            queue<string> q1;
            while(size--){
                string s = q.front();
                q.pop();
                dict.erase(s);
                int len = s.size();
                for(int i =0;i<len;i++){
                    for(int j=0;j<26;j++){
                        char c = s[i];
                        s[i]='a'+j;
                        if(dict.find(s)!=dict.end()){
                            if(s==endWord){return steps;}
                            q1.push(s);
                        }
                        s[i]=c;
                    }
                }
            }
            q=q1;
        }
        return 0;
    }
};
```

