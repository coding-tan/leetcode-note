# 

[代码随想录文档链接]()

[力扣题目链接]()

```text

```

## 1. 暴力求解法
时间复杂度`O(m*n)`,
空间复杂度`O(1)`.
```cpp
// 暴力求解法
class Solution {
public:
    int strStr(string haystack, string needle) {
        if(needle.empty()){ // 如果模板串为空，返回0
            return 0;
        }
        int i = 0, j = 0;
        while(haystack[i] != '\0' && needle[j] != '\0'){
            if(haystack[i] == needle[j]){
                i++;
                j++;
            }
            else{
                i = i - j + 1;
                j = 0;
            }
        }
        if(needle[j] == '\0'){
            return i-j;
        }
        return -1;
    }
};
```
## 2. KMP算法求解字符匹配
时间复杂度`O(m+n)`,
空间复杂度`O(m)`.
未理解透彻！！！前缀表生成，以及kmp使用过程！
```cpp
// KMP算法
// KMP算法
class Solution {
public:
    void getNext(int *next, string &s){ // 生成Next数组（前序表）
        int j = 0; // j指向前缀末尾位置， i指向后缀末尾位置
        next[0] = j;
        for(int i = 1; i < s.size(); i++){ // 注意i从1开始
            while(j > 0 && s[i] != s[j]){ // 前后缀不相同
                j = next[j - 1]; // 向前回退
            }
            if(s[i] == s[j]){ // 找到相同的前后缀
                j++;
            }
            next[i] = j; // 将j（前缀的长度）赋给next[i]
        }
    }
    int strStr(string haystack, string needle) {
        if(needle.empty()){ // 如果模板串为空，返回0
            return 0;
        }
        int next[needle.size()];
        getNext(next, needle);
        int j = 0; 因为next数组里记录的起始位置为0
        for(int i = 0; i < haystack.size(); i++){ // 注意i就从0开始
            while(j > 0 && haystack[i] != needle[j]){  // 不匹配
                j = next[j - 1]; // j 寻找之前匹配的位置
            }
            if(haystack[i] == needle[j]){ // 匹配，j和i同时向后移动
                j++; // i的增加在for循环里
            }
            if(j == needle.size()){ // 文本串s里出现了模式串t
                return (i - needle.size() + 1);
            }
        }
        return -1;
    } 
};
```