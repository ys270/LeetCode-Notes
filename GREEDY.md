455. assign cookies

Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie. Each child i has a greed factor gi, which is the minimum size of a cookie that the child will be content with; and each cookie j has a size sj. If sj >= gi, we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

**Note:**
You may assume the greed factor is always positive.
You cannot assign more than one cookie to one child.

**Example 1:**

```
Input: [1,2,3], [1,1]

Output: 1

Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.
```



**Example 2:**

```
Input: [1,2], [1,2,3]

Output: 2

Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
```

```c++
int findContentChildren(vector<int>& g, vector<int>& s) {
     std::sort(g.begin(),g.end());
     std::sort(s.begin(),s.end());
     int count = 0;
     vector<int>::iterator it1 = g.begin();
     vector<int>::iterator it2 = s.begin();
     while(it1!=g.end()&&it2!=s.end()){
        if (*it1>*it2){
            ++it2;
        }
         else{
             ++it1;
             ++it2;
             count++;
         }
     }
        return count;
    }
```



435.non-overlapping intervals

Given a collection of intervals, find the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

**Example 1:**

```
Input: [[1,2],[2,3],[3,4],[1,3]]
Output: 1
Explanation: [1,3] can be removed and the rest of intervals are non-overlapping.
```

**Example 2:**

```
Input: [[1,2],[1,2],[1,2]]
Output: 2
Explanation: You need to remove two [1,2] to make the rest of intervals non-overlapping.
```

```c++
bool wayToSort(vector\<int> a, vector\<int> b){
        return a[1]<b[1];
    }
class Solution {
public:  
    int eraseOverlapIntervals(vector<vector\<int>>& intervals) {
        if(intervals.size()==0){return 0;}
        std::sort(intervals.begin(),intervals.end(),wayToSort);
        int count = 1;
        int end = intervals\[0][1];
        for(int i =0;i<intervals.size();i++){
            if(intervals\[i][0]<end){
                continue;
            }
            end = intervals\[i][1];
            count++;
        }
        return intervals.size()-count;
    }
};
```

452.minimum number of arrows to burst balloons(very similar to above)

There are a number of spherical balloons spread in two-dimensional space. For each balloon, provided input is the start and end coordinates of the horizontal diameter. Since it's horizontal, y-coordinates don't matter and hence the x-coordinates of start and end of the diameter suffice. Start is always smaller than end. There will be at most 104 balloons.

An arrow can be shot up exactly vertically from different points along the x-axis. A balloon with xstart and xend bursts by an arrow shot at x if xstart ≤ x ≤ xend. There is no limit to the number of arrows that can be shot. An arrow once shot keeps travelling up infinitely. The problem is to find the minimum number of arrows that must be shot to burst all balloons.

**Example:**

```
Input:
[[10,16], [2,8], [1,6], [7,12]]

Output:
2

Explanation:
One way is to shoot one arrow for example at x = 6 (bursting the balloons [2,8] and [1,6]) and another arrow at x = 11 (bursting the other two balloons).
```

```c++
bool sortMethod(vector\<int> a, vector\<int> b){
    return a[1]<b[1]?true:false;
}
class Solution {
public:
    int findMinArrowShots(vector<vector\<int>>& points) {
        if (points.size()==0){
            return 0;
        }
        std::sort(points.begin(),points.end(),sortMethod);
        int end = points[0][1];
        int count = 1;
        for(int i = 0;i<points.size();i++){
            if(points[i][0]<=end){
                continue;
            }
            end = points[i][1];
            count++;
        }
        return count;
    }
};
```

406.queue reconstruction by height (vector insert 用法)

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers `(h, k)`, where `h` is the height of the person and `k` is the number of people in front of this person who have a height greater than or equal to `h`. Write an algorithm to reconstruct the queue.

**Note:**
The number of people is less than 1,100. 

**Example**

```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

```c++
bool sortMethod(vector\<int> &a,vector\<int> &b){
    if (a[0]>b[0]){
        return true;
    }
    else if(a[0]==b[0]){
        if(a[1]<=b[1]){
            return true;
        }
    }
    return false;
}

class Solution {
public:
    vector<vector\<int>> reconstructQueue(vector<vector\<int>>& people) {
    std::sort(people.begin(),people.end(),sortMethod); 
    vector<vector\<int>> res;
    for(int i = 0;i<people.size();i++){
        <font color = red size = 3 >res.insert(res.begin()+people\[i][1],people[i]);</font>
         }
    return res;
     }  
};
```

121.best time to buy and sell stock

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**Example 2:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

```c++
int maxProfit(vector\<int>& prices) {
        int min_price = INT_MAX;
        int max_profit = 0;
        for(int i = 0;i<prices.size();i++){
            min_price = prices[i]<min_price?prices[i]:min_price;
            max_profit = (prices[i]-min_price)>max_profit?(prices[i]-min_price):max_profit;
        }
        return max_profit;
    }
```



122. Best Time to Buy and Sell Stock II

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
```

**Example 2:**

```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

```c++
int maxProfit(vector\<int>& prices) {
        if(prices.size()==0){return 0;}
        int max_profit = 0;
        for(int i = 0; i < prices.size()-1; i++){
            if(prices[i]<prices[i+1]){
                   max_profit += prices[i+1] - prices[i];
            }
        }
        return max_profit;
    }
```





392. Is Subsequence

Given a string **s** and a string **t**, check if **s** is subsequence of **t**.

You may assume that there is only lower case English letters in both **s** and **t**. **t** is potentially a very long (length ~= 500,000) string, and **s** is a short string (<=100).

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ace"` is a subsequence of `"abcde"` while `"aec"` is not).

**Example 1:**
**s** = `"abc"`, **t** = `"ahbgdc"`

Return `true`.

**Example 2:**
**s** = `"axc"`, **t** = `"ahbgdc"`

Return `false`.

```c++
 bool isSubsequence(string s, string t) {
        int pos = -1;
       for(int i = 0;i<s.size();i++){
           <font color = red size = 3>pos = t.find(s[i],pos+1);</font>
           if(pos == string::npos){
               return false;
           }
       }
        return true;
    }

```



665. Non-decreasing Array

Given an array with `n` integers, your task is to check if it could become non-decreasing by modifying **at most** `1` element.

We define an array is non-decreasing if `array[i] <= array[i + 1]` holds for every `i` (1 <= i < n).

**Example 1:**

```
Input: [4,2,3]
Output: True
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
```



**Example 2:**

```
Input: [4,2,1]
Output: False
Explanation: You can't get a non-decreasing array by modify at most one element.
```

<font color = red>when encounter nums[i]>nums[i+1], should we change nums[i] or change nums[i+1]: utilize greedy. If change nums[i] is feasible, change it to be smaller, if not(constraint by nums[i-1]), change nums[i+1] to be bigger.</font>

```c++
bool checkPossibility(vector\<int>& nums) {
        int count = 0;
        for(int i = 0;i < nums.size() - 1;i++){
            if(nums[i]>nums[i+1]){
                count++;
                if(count==1){
                    if(i!=0 && nums[i-1]>nums[i+1]){
                        nums[i+1] = nums[i];
                    }
                    nums[i] = nums[i+1];
                }
                else{
                    return false;
                }
            }
        }
        return true;
    }
```



53. Maximum Subarray

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

<font color = red size = 3> when presum < 0, restart it from 0.</font>

int maxSubArray(vector\<int>& nums) {
        int max = nums[0];
        int presum = 0;
        for(int i = 0;i<nums.size();i++){
            presum = presum > 0 ? presum + nums[i] : nums[i];
            max = max > presum? max : presum;
        }
        return max;
    }

<font color = red>Divide and Conquer:</font>

```c++
class Solution {
public:
    
    int divideandconquer(vector<int>&nums, int left, int right)
    {            
        //conquer 
        if (left==right)
        {
            return nums.at(left);
        }
        
        int mid = (left + right) / 2;
        
        // divide
        int leftMax = divideandconquer(nums, left, mid);
        
        int rightMax = divideandconquer(nums, mid+1, right);
               
        // merge
        int ml= -1e6,  mr = -1e6;
        
        for (int i=mid+1, sum=0;i<=right;i++)
        {
            sum += nums.at(i);
            
            if (sum > mr) mr = sum;
        }
        
        for (int i=mid, sum=0;i>=left;i--)
        {
            sum += nums.at(i);
            
            if (sum > ml) ml = sum;
        }
        
        int crossMax = ml + mr;
        
        int maximum = max(max(leftMax, rightMax), crossMax);

        return maximum;
    }
    
    int maxSubArray(vector<int>& nums) {
        
        return divideandconquer(nums, 0, nums.size()-1);
        
    }
};
```

763. Partition Labels  <font color = red> (pay attention !!!)</font>

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example 1:**

```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

```c++
vector\<int> partitionLabels(string S) {
        int lastchar[26]={0};
        for(int i =0;i<S.size();i++){
            lastchar[S[i]-'a'] = i;    
        }
        int maxend = 0;
        int start = 0;
        vector\<int> res;
        for(int j = start;j<S.size();j++){
            maxend = maxend>lastchar[S[j]-'a']?maxend:lastchar[S[j]-'a'];
            if(maxend==j){
                res.push_back(j-start+1);
                start = j+1;
            }
        }
        return res;
    }
```

