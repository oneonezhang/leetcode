#Roman to Integer
##Problem:
Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.
##Idea:
If a letter is smaller than the next one, subtract it; else add it.  
`Hash Table`
```cpp
class Solution {
public:
    int romanToInt(string s) {
        //I（1）、V（5）、X（10）、L（50）、C（100）、D（500）、 M（1000）
        int value=0;
        unordered_map<char,int> roman_int;
        roman_int['I']=1;
        roman_int['V']=5;
        roman_int['X']=10;
        roman_int['L']=50;
        roman_int['C']=100;
        roman_int['D']=500;
        roman_int['M']=1000;
        for(int i=0;i<(int)s.size()-1;i++)
        {
            int current=roman_int[s[i]];
            if(roman_int[s[i]]<roman_int[s[i+1]]) current*=-1;
            value += current;
        }
        if(s.size()) value += roman_int[s[s.size()-1]];//s[s.size()-1] can be replaced by s.back()
        return value;
    }
};
```
`switch-case and each letter is read only once`  //faster
```cpp
class Solution {
public:
    int romanToInt(string s) {
        int value=0;
        if(!s.size()) return 0;
        else
        {
            int current;
            int next;
            switch(s[0])
            {
                case 'I':current=1;break;
                case 'V':current=5;break;
                case 'X':current=10;break;
                case 'L':current=50;break;
                case 'C':current=100;break;
                case 'D':current=500;break;
                case 'M':current=1000;break;
            }
            for(int i=0;i<s.size()-1;i++)
            {
                switch(s[i+1])
                {
                case 'I':next=1;break;
                case 'V':next=5;break;
                case 'X':next=10;break;
                case 'L':next=50;break;
                case 'C':next=100;break;
                case 'D':next=500;break;
                case 'M':next=1000;break;
                }
                if(current<next) value -= current;
                else value += current;
                current=next;
            }
            value += current;
            return value;
        }
    }
};
```
