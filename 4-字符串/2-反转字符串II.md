# 541. 反转字符串II

[代码随想录文档链接](https://www.programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)

[力扣题目链接](https://leetcode.cn/problems/reverse-string-ii/)
给定一个字符串 s 和一个整数 k，从字符串开头算起，每计数至 2k 个字符，就反转这 2k 字符中的前 k 个字符。

- 如果剩余字符少于 k 个，则将剩余字符全部反转。
- 如果剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符，其余字符保持原样。
```text
示例 1：
输入：s = "abcdefg", k = 2
输出："bacdfeg"

示例 2：
输入：s = "abcd", k = 2
输出："bacd"
```

## 1. C++库函数reverse的版本

```cpp
class Solution {
public:
    string reverseStr(string s, int k) {
        for(int i = 0; i <　s.size(); i += 2*k){
            // 1. 每隔 2k 个字符的前 k 个字符进行反转
            // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
            if(i + k <= s.size()){
                reverse(s.begin()+i, s.begin()+i+k);
            }
            else{
                // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
                reverse(s.begin()+i, s.end());
            }
        }
        return s;
    }
};
```

## 2. 自己实现reverse的版本
注意函数传递参数 使用的是引用

函数 void reverse(string &s, int start, int end) 中的参数 string &s 使用的是引用传递。在 C++ 中，通过引用传递参数可以直接操作原始对象，而不是对对象进行复制。这种方式可以提高效率，尤其是当对象较大时，因为不需要复制整个对象，只需要传递对象的引用即可。
```cpp
class Solution {
public:
    void reverse(string &s, int start, int end){
        for(int i = start, j = end; i < j; i++, j--){
            swap(s[i], s[j]);
        }
    }

    string reverseStr(string s, int k) {
        for(int i = 0; i <　s.size(); i += 2*k){
            // 1. 每隔 2k 个字符的前 k 个字符进行反转
            // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
            if(i + k <= s.size()){
                reverse(s, i, i+k-1);
            }
            else{
                // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
                reverse(s, i, s.size()-1);
            }
        }
        return s;
    }
};
```
## 3. while实现反转
```cpp
class Solution {
public:
    string reverseStr(string s, int k) {
        int pos = 0, n = s.size();
        while(pos < n){
            // 剩余字符串大于等于k的情况
            if(pos + k < n){ // 当pos+k = n 时考虑在了else的情况里了
                reverse(s.begin()+pos, s.begin()+pos+k);
            }
            // 剩余字符串小于k的情况
            else{
                reverse(s.begin()+pos, s.end());
            }
            pos += 2*k;
        }
        return s;
    }
};
```