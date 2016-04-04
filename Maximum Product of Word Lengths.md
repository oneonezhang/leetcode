#Maximum Product of Word Lengths
##Problem:
Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

Example 1:
Given `["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]`  
Return `16`  
The two words can be `"abcw", "xtfn"`.  

Example 2:
Given `["a", "ab", "abc", "d", "cd", "bcd", "abcd"]`  
Return `4`  
The two words can be `"ab", "cd"`.  

Example 3:
Given `["a", "aa", "aaa", "aaaa"]`  
Return `0`  
No such pair of words.
##Idea:
暴力求解method of exhaustion，用bool[26]记录字母是否出现过。
##To Study:
可以用mask(int型)来记录每个字母是否出现  
用 & 判断是否有共同的字母  
```cpp
class Solution {
public:
    int maxProduct(vector<string>& words) {
        int maxLen=0;
        vector<int> mask(words.size());
        for(int i=0;i<words.size();i++)
        {
            for(char c:words[i])
            {
                mask[i] |= 1 << (c-'a');
            }
        }
        for(int i=0;i<words.size();i++)
        {
            for(int j=i+1;j<words.size();j++)
            {
                if(!(mask[i]&mask[j]))
                maxLen=(words[i].size()*words[j].size()>maxLen)?words[i].size()*words[j].size():maxLen;
            }
        }
        return maxLen;
    }
};
```