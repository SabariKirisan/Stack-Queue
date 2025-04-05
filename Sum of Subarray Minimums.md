## Sum of Subarray Minimums (stack) (c++)
Given an array of integers arr, find the sum of min(b), where b ranges over every (contiguous) subarray of arr. Since the answer may be large, return the answer modulo 109 + 7.

## Example
Input: arr = [3,1,2,4]

Output: 17

Explanation: 

Subarrays are [3], [1], [2], [4], [3,1], [1,2], [2,4], [3,1,2], [1,2,4], [3,1,2,4].

Minimums are 3, 1, 2, 4, 1, 1, 2, 1, 1, 1.

Sum is 17.
## PROGRAM:(Main.cpp)
```
class Solution {
public:
    vector<int> findnse(vector<int>& arr,int n)
    {
        stack<int> st; 
        vector<int> res(n); 
        for(int i=n-1;i>=0;i--)
        {
         while(!st.empty() && arr[st.top()]>=arr[i])
         {
            st.pop();
         }
        res[i]=st.empty() ? n : st.top();
        st.push(i);
        } 
        return res;
    }
    vector<int> findpse(vector<int>& arr,int n)
    {
        stack<int> st; 
        vector<int> res(n); 
        for(int i=0;i<n;i++)
        {
         while(!st.empty() && arr[st.top()]>arr[i])
         {
            st.pop();
         }
        res[i]=st.empty() ? -1 : st.top();
        st.push(i);
        } 
        return res;
    }
    int sumSubarrayMins(vector<int>& arr) 
    {
        int n=arr.size();

        long long total=0;
        int mod=1e9+7;

        vector<int> nse=findnse(arr,n);

        vector<int> psee=findpse(arr,n);

        for(int i=0;i<n;i++)
        {
            int left= i - psee[i];

            int right= nse[i] - i;

            total = (total + (1LL*left * right % mod * arr[i] % mod)) % mod;
        }
        return total;
    }
};
```
## Complexity
- Time complexity : O(5N) ~ O(N)

- Space complexity : O(5N) ~ O(N)
