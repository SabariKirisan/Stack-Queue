## Remove K Digits (c++)

Given string num representing a non-negative integer num, and an integer k, return the smallest possible integer after removing k digits from num.

## Example
Input: num = "1432219", k = 3

Output: "1219"

Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
## PROGRAM:(Main.cpp)
```
class Solution {
public:
    string removeKdigits(string num, int k) 
    {
        int n=num.size();
        if (k >= n) return "0";

        stack<char> st;
        for(int i=0;i<n;i++)
        {
            while(!st.empty() && k>0 && (st.top()-'0') > (num[i]-'0'))
            {
                st.pop();
                k--;
            }
            st.push(num[i]);
        }
        while(k>0) 
        {
            st.pop();
            k--;
        }
        if(st.empty()) return "0";

        string res="";
        while(!st.empty())
        {
            res.push_back(st.top());
            st.pop();
        }
        while(res.size()!=0 && res.back()=='0')
        {
            res.pop_back();
        }
        reverse(res.begin(),res.end());

        if(res.empty()) return "0";

        return res;
    }
};
```
## Complexity
- Time complexity : O(3N)+ O(k)

- Space complexity : O(N + N)
