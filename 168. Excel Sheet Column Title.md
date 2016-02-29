#Excel Sheet Column Title
##Problem:
Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
##Idea:
```cpp
class Solution {
public:
    string convertToTitle(int n) {
        string title;
        while(n)
        {
            title += (n-1)%26 + 'A';
            n = (n-1)/26;
        }
        for(int i=0;i<title.length()/2;i++)
        {
            swap(title[i],title[title.length()-1-i]);
        }
        return title;
    }
};
```
