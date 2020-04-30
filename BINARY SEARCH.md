## Dichotomy

69. Sqrt(x)

Implement `int sqrt(int x)`.

Compute and return the square root of *x*, where *x* is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

```c++
int mySqrt(int x) {
        if(x <= 1){
            return x;
        }
        int l = 0;
        int r = x;
        while(l <= r){
            int mid = l + (r - l) / 2;
            if(x/mid==mid){
                return mid;
            }
            else if(x/mid>mid){
                l = mid + 1;
            }
            else{
                r = mid -1; 
            }
        }
        return r;
    }

```



744. Find Smallest Letter Greater Than Target<font color = red> (hard to think of the answer)</font>

Given a list of sorted characters `letters` containing only lowercase letters, and given a target letter `target`, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is `target = 'z'` and `letters = ['a', 'b']`, the answer is `'a'`.

**Examples:**

```
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

```c++
char nextGreatestLetter(vector\<char>& letters, char target) {
        int len = letters.size();
        int l = 0;
        int r = len - 1;
        while(l<=r){
            int mid = l + (r-l)/2;
            if(letters[mid]<=target){
                l = mid + 1;
            }
            else {
                r = mid - 1;
            }
        }
        char res = l==len?letters[0]:letters[l];
        return res;
    }
```



278. First Bad Version

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which will return whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example:**

```
Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version. 
```



```c++
bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int l = 0;
        int r = n;
        while(l<=r){
            int m = l + (r-l)/2;
            if(isBadVersion(m) == false&&isBadVersion(m+1)==true){
                return  m+1;
            }
            else if(isBadVersion(m) == false){
                l = m + 1;
            }
            else{
                r = m - 1;
            }
        }
       return n; 
     }   
};
```

540. Single Element in a Sorted Array

     <font color = red> find pattern before and after the single number!!</font>

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once. Find this single element that appears only once. 

**Example 1:**

```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Example 2:**

```
Input: [3,3,7,7,10,11,11]
Output: 10
```

```c++
int singleNonDuplicate(vector<int>& nums) {
        int l = 0;
        int r = nums.size()-1;
        while(l<r){
            int m = l + (r - l)/2;
            if (m%2==1){
                m = m - 1;//make m alsways be even
            }
            if (nums[m] == nums[m+1]){
                l = m + 2;
            }
            else{
                r = m;
            }
        }
        return nums[l];
    }
```

153. Find Minimum in Rotated Sorted Array

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e.,  `[0,1,2,4,5,6,7]` might become  `[4,5,6,7,0,1,2]`).

Find the minimum element.

You may assume no duplicate exists in the array.

**Example 1:**

```
Input: [3,4,5,1,2] 
Output: 1
```

**Example 2:**

```
Input: [4,5,6,7,0,1,2]
Output: 0
```

 ```c++
int findMin(vector<int>& nums) {
  int l = 0;
  int r = nums.size()-1;
  while(l<r){
    int m = l + (r - l)/2;
    if(nums[m]>nums[r]){
      l = m + 1; 
    }
    else{
      r = m;
    }
  }
  return nums[l];
}

 ```

34. Find First and Last Position of Element in Sorted Array

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

```c++
class Solution {
public:
    int findfirst(vector<int>& nums,int target){
        int l = 0;
        int r = nums.size();//注意这里的r，为了[2,2],2这类情况
        while(l<r){
            int m = l + (r - l)/2;
            if(nums[m]<target){
                l = m + 1;
            }
            else{
                r = m;
            }
        }
        return l;
    }
    vector<int> searchRange(vector<int>& nums, int target) {
        int first = findfirst(nums,target);
        int last = findfirst(nums,target+1);
        vector<int> res;
        if(first == nums.size()||nums[first]!=target){
            res.push_back(-1);
            res.push_back(-1);
            return res;
        }
        res.push_back(first);
        res.push_back(last-1);
        return res;
    }
};
```

