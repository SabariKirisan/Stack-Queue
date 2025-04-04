## Check for Balanced Parentheses(stack) (c++)

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.

Open brackets must be closed in the correct order.

Every close bracket has a corresponding open bracket of the same type.

## Example
Input: s = "()[]{}"

Output: true

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    bool isValid(string s) 
    {
        stack<char> st;
        for(auto it:s)
        {
            if(it=='(' || it=='[' || it=='{') st.push(it);

            else 
            {
                if(st.size()==0) return false;

                char ch=st.top();
                st.pop();
                if((it==')' and ch=='(') or (it==']' and ch=='[') or (it=='}' and ch=='{'))  continue;
                else return false;
            }
        }
        return st.empty();        
    }
};
```
## Complexity
- Time complexity : O(N)

- Space complexity : O(N)
