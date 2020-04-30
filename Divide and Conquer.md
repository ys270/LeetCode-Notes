## Divide and Conquer

241. Different Ways to Add Parentheses

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are `+`, `-` and `*`.

**Example 1:**

```
Input: "2-1-1"
Output: [0, 2]
Explanation: 
((2-1)-1) = 0 
(2-(1-1)) = 2
```

**Example 2:**

```
Input: "2*3-4*5"
Output: [-34, -14, -10, -10, 10]
Explanation: 
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```

```c++
class Solution {
public:
   vector<int> diffWaysToCompute(string input){
       vector<int> res;
       for(int i =0;i<input.size();i++){
            if(input[i]=='*'||input[i]=='-'||input[i]=='+'){
                vector<int> left = diffWaysToCompute(input.substr(0,i));
                vector<int> right = diffWaysToCompute(input.substr(i+1,input.size()-i-1));
                for(int j = 0;j<left.size();j++){
                    for(int k =0;k<right.size();k++){
                       if(input[i]=='+'){
                            res.push_back(left[j]+right[k]);
                       }
                       else if(input[i]=='-'){
                           res.push_back(left[j]-right[k]);
                        }
                       else if(input[i]=='*'){
                           res.push_back(left[j]*right[k]);
                        } 
                    }
                }
            }
        }
        if(res.size()==0){
            res.push_back(stoi(input));
        }
        return res; 
    } 
};
```

