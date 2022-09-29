实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回 -1。



> 示例 1: 输入: haystack = "hello", needle = "ll" 输出: 2
>
> 示例 2: 输入: haystack = "aaaaa", needle = "bba" 输出: -1
>
> 说明: 当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。 对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。



**这题主要用到了KMP算法，它主要用在文本匹配，比如给定**

**一个文本串aabaabaaf**

**一个模式串aabaaf 要求模式串是否在文本串内出现**

需要用到**前缀表，它储存的是最长相等前后缀**

前缀表可以记录访问到当前字符了，发现不匹配，那么回退到哪里重新匹配比较好

**比如说访问到aabaaf的f了，我们回退一位查看aabaaf的最后一个a的next数组的值，就知道可以从b再开始匹配**

 

```cpp
// next数组，模式串s
void getNext(int* next, string s)
    //初始化next数组
    //j表示前缀的末尾，也表示i当前所指元素最长前后缀的大小
    int j = 0;
	next[j] = 0;
	for (int i = 0; i < s.size(); i++) {
        while (j > 0 && s[i] != s[j]) {
            j = next[j - 1];
        }
        if (s[i] == s[j]) {
            j++;
        }
        next[i] = j;
    }

int strStr(string haystack, string needle) {
    int next[needle.size()];
    getNext(next, needle);
    int j = 0;    //记录匹配的长度
    for (int i = 0; i < haystack.size(); i++) {
        while (j != 0 && haystack[i] != neddle[j]) {
            j = next[j - 1];
        }
        if (haystack[i] == needle[j]) {
            j++;
        }
        if (j == neddle.size()) {
            return i - j + 1;
        }
    }
    return -1;
}
```

