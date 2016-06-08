#Plus One
##Problem:
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.
##Idea:
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n=digits.size();
        vector<int> result(n);
        if(n)
        {
            int i;
            for(i=n-1;i>=0;i--)
            {
                if(digits[i]!=9) break;
            }
            if(i<0)
            {
                result.insert(result.begin(),1);//The position of insert must be an iterator
            }
            else
            {
                for(int j=0;j<i;j++) result[j]=digits[j];
                result[i]=digits[i]+1;
            }
        }
        return result;
    }
};
```
##To Study:
do it in place
```cpp
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n=digits.size();
        int carry=1;
        for(int i=n-1;i>=0&&carry;i--)
        {
            digits[i]++;
            carry=digits[i]/10;
            digits[i]=digits[i]%10;
        }
        if(carry)
        {
            digits.insert(digits.begin(),1);
        }
        return digits;
    }
};
```