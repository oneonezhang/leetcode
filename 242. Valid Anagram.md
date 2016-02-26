#Valid Anagram
##Problem:
Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = "anagram", t = "nagaram", return true.
s = "rat", t = "car", return false.

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?
##Idea:
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int sCount[26]={0};
        int tCount[26]={0};
        if(s.length()!=t.length()) return 0;
        for(int i=0;i<s.length();i++)
        {
            sCount[s[i]-'a']++;
            tCount[t[i]-'a']++;
        }
        for(int i=0;i<26;i++)
        {
            if(sCount[i]!=tCount[i]) return 0;
        }
        return 1;
    }
};
```
##To Study:
1.`sort`  可以适用于unicode
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort((char*)s.c_str(),(char*)s.c_str()+s.length());
        sort((char*)t.c_str(),(char*)t.c_str()+t.length());     
        return s==t;
    }
};
```
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        sort(s.begin(),s.end());
        sort(t.begin(),t.end());     
        return s==t;
    }
};
```  
第一种比第二种更快一些  
2.hash table
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        unordered_map<char,int>count;
        if(s.size()!=t.size()) return 0;
        for(int i=0;i<s.length();i++)
        {
            count[s[i]]++;
            count[t[i]]--;
        }
        for(auto i:count)
        {
            if(i.second) return 0;
        }
        return 1;
    }
};
```