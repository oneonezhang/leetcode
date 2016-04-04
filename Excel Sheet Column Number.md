#Excel Sheet Column Number
##Problem:
Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
##Idea:
类似于26进制数
```cpp
class Solution {
public:
    int titleToNumber(string s) {
        int col=0;
        for(int i=0;i<s.length();i++)
        {
            col += pow(26,s.length()-1-i)*(s[i]-'A'+1);
        }
        return col;
    }
};
```
##To Study:
```cpp
class Solution {
public:
    int titleToNumber(string s) {
        int col=0;
        for(int i=0;i<s.length();i++)
        {
            col = col*26+s[i]-'A'+1;
        }
        return col;
    }
};
```