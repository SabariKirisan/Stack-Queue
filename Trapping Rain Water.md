## Trapping Rain Water (stack) (c++)
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

## Example
![image](https://github.com/user-attachments/assets/8a5de918-7c89-43a3-b15c-6d16c65ffac6)

Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]

Output: 6

Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

## PROGRAM:(Main.cpp)
```
class Solution {
public:
    int trap(vector<int>& height) 
    {
        int n=height.size();
        int l_m=0,r_m=0;
        int total=0;
        int l=0,r=n-1;

        while(l<=r)
        {
            if(height[l]<=height[r])
            {
                if(l_m > height[l])
                {
                    total+=l_m-height[l];
                }   
                else
                {
                    l_m=height[l];
                }
                l++;
            }
            else
            {
                if(r_m > height[r])
                {
                    total+=r_m - height[r];
                }
                else
                {
                    r_m=height[r];
                }
                r--;
            }
        }
        return total;
    }
};
```
## Complexity
- Time complexity : O(N)

- Space complexity : O(1)
