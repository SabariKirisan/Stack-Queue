## Sum of Subarray Ranges (stack) (c++)
You are given an integer array nums. The range of a subarray of nums is the difference between the largest and smallest element in the subarray.

Return the sum of all subarray ranges of nums.

A subarray is a contiguous non-empty sequence of elements within an array.

## Example
Input: nums = [1,2,3]

Output: 4

Explanation: The 6 subarrays of nums are the following:

[1], range = largest - smallest = 1 - 1 = 0 

[2], range = 2 - 2 = 0

[3], range = 3 - 3 = 0

[1,2], range = 2 - 1 = 1

[2,3], range = 3 - 2 = 1

[1,2,3], range = 3 - 1 = 2

So the sum of all ranges is 0 + 0 + 0 + 1 + 1 + 2 = 4.
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
            while(!st.empty() && arr[st.top()]>=arr[i]) st.pop();
            res[i] = st.empty() ? n : st.top();
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
            while(!st.empty() && arr[st.top()]>arr[i]) st.pop();
            res[i] = st.empty() ? -1 : st.top();
            st.push(i);
        } 
        return res;
    }

    long long sumSubarrayMins(vector<int>& arr) 
    {
        int n = arr.size();
        long long total = 0;

        vector<int> nse = findnse(arr, n);
        vector<int> pse = findpse(arr, n);

        for(int i=0; i<n; i++)
        {
            long long left = i - pse[i];
            long long right = nse[i] - i;
            total += left * right * arr[i];
        }
        return total;
    }

    vector<int> findnge(vector<int>& arr,int n)
    {
        stack<int> st; 
        vector<int> res(n); 
        for(int i=n-1;i>=0;i--)
        {
            while(!st.empty() && arr[st.top()]<=arr[i]) st.pop();
            res[i] = st.empty() ? n : st.top();
            st.push(i);
        } 
        return res;
    }

    vector<int> findpge(vector<int>& arr,int n)
    {
        stack<int> st; 
        vector<int> res(n); 
        for(int i=0;i<n;i++)
        {
            while(!st.empty() && arr[st.top()]<arr[i]) st.pop();
            res[i] = st.empty() ? -1 : st.top();
            st.push(i);
        } 
        return res;
    }

    long long sumSubarrayMaxs(vector<int>& arr) 
    {
        int n = arr.size();
        long long total = 0;

        vector<int> nge = findnge(arr, n);
        vector<int> pge = findpge(arr, n);

        for(int i=0;i<n;i++)
        {
            long long left = i - pge[i];
            long long right = nge[i] - i;
            total += left * right * arr[i];
        }
        return total;
    }

    long long subArrayRanges(vector<int>& nums) 
    {
        return sumSubarrayMaxs(nums) - sumSubarrayMins(nums);
    }
};

```
## Complexity
- Time complexity : O(10N) ~ O(N)

- Space complexity : O(10N) ~ O(N)
