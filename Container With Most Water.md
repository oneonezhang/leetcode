#Container With Most Water
##Problem:
Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container.
##Idea:
method of exhaustion——O(n2)    
Time Limit Exceeded
##To Study:
`Two Pointers`
```
1.min(height[lineLeft],height[lineRight]) decides the height of container  
2.initial state: lineLeft=0,lineRight=height.size()-1 ——widest  
3.when height[lineLeft]<=height[lineRight], there is no need to compute the volume of (left=lineLeft,lineLeft<right<lineRight), because they are smaller than the current volume.  
For the same reason, we can skip (lineLeft<left<lineRight,right=lineRight) when height[lineLeft]>height[lineRight].
```
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int water=0;
        int lineLeft=0;
        int lineRight=height.size()-1;
        while(lineLeft<lineRight)
        {
            if(height[lineLeft]<=height[lineRight])
            {
                water=max(water,height[lineLeft]*(lineRight-lineLeft));
                lineLeft++;
            }
            else
            {
                water=max(water,height[lineRight]*(lineRight-lineLeft));
                lineRight--;
            }
        }
        return water;
    }
};
```
  
`An Optimized One`  
If the new height of the container isn't larger than the old one, skip it.
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int water=0;
        int lineLeft=0;
        int lineRight=height.size()-1;
        while(lineLeft<lineRight)
        {
            int h=min(height[lineLeft],height[lineRight]);
            water=max(water,h*(lineRight-lineLeft));
            while(height[lineLeft]<=h&&lineLeft<lineRight) lineLeft++;
            while(height[lineRight]<=h&&lineLeft<lineRight) lineRight--;
        }
        return water;
    }
};
```
