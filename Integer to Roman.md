#Integer to Roman
##Problem:
Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.
##Idea:
```cpp
class Solution {
public:
    string intToRoman(int num) {
        string roman;
        while(num)
        {
            if(num>=1000)
            {
                roman += 'M';
                num -= 1000;
            }
            else if(num>=900)
            {
                roman += "CM";
                num -= 900;
                
            }
            else if(num>=500)
            {
                roman += 'D';
                num -= 500;
            }
            else if(num>=400)
            {
                roman += "CD";
                num -= 400;
            }
            else if(num>=100)
            {
                roman += 'C';
                num -= 100;
            }
            else if(num>=90)
            {
                roman += "XC";
                num -= 90;
            }
            else if(num>=50)
            {
                roman += 'L';
                num -= 50;
            }
            else if(num>=40)
            {
                roman += "XL";
                num -= 40;
            }
            else if(num>=10)
            {
                roman += 'X';
                num -= 10;
            }
            else if(num>=9)
            {
                roman += "IX";
                num -= 9;
            }
            else if(num>=5)
            {
                roman += 'V';
                num -= 5;
            }
            else if(num>=4)
            {
                roman += "IV";
                num -= 4;
            }
            else
            {
                roman += 'I';
                num -= 1;
            }
            
        }
        return roman;
    }
};
```
##To Study:
用数组将各位上的数字与罗马数字对应
```cpp
class Solution {
public:
    string intToRoman(int num) {
        string M[]={"","M","MM","MMM"};
        string C[]={"","C","CC","CCC","CD","D","DC","DCC","DCCC","CM"};
        string X[]={"","X","XX","XXX","XL","L","LX","LXX","LXXX","XC"};
        string I[]={"","I","II","III","IV","V","VI","VII","VIII","IX"};
        return M[num/1000]+C[(num%1000)/100]+X[(num%100)/10]+I[(num%10)];
    }
};
```
