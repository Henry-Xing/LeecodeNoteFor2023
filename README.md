# LeecodeNoteFor2023
drive link: https://drive.google.com/drive/folders/1e4Lboc4y1uaDwOWHhmAIXtQHzPPXAJVB


task link: https://ke.qq.com/course/package/31104?flowToken=1039500


Learning Time: 2:00-6:00 7:30-10:30 7h


### date: 2022/11/11 数组字符串

- question: input/output基础 link: https://www.nowcoder.com/test/27976983/summary#question

- question: HJ12 字符串反转 link: https://www.nowcoder.com/practice/e45e078701ab4e4cb49393ae30f1bb04?tpId=37&tqId=21235&ru=/exam/oj
    - answer:
``` python
# python code
import sys
# 逆序遍历数组 <=> 切片stride = -1 <=> list[start: end: stride]
for line in sys.stdin:
    a = line.split()
    # line.split() return a list
    print(a[0][::-1])
```

``` java

```

- question: HJ68 成绩排序 link: https://www.nowcoder.com/practice/8e400fd9905747e4acc2aeed7240978b?tpId=37&tqId=21291&ru=/exam/oj
    - answer:
``` python
# python code
import sys
# read one line only
n = int(input())
# Python三目运算符
order = True if int(input()) == 0 else False

score = []
for line in sys.stdin:
    s = line.split()
    score.append([s[0], int(s[1])])

# 按照key排序, 默认排序为升序, reverse是否逆序.
score.sort(key=lambda x: x[1], reverse=order) 

# print(*s) 可以直接将list打印出来且间隔为一个空格.
for s in score:
    # print(*s)
    print(s[0], s[1])
```

``` java

```


- question: LC442 数组中重复的数据 link: https://leetcode.cn/problems/find-all-duplicates-in-an-array/
    - answer:
``` py
# python code
class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        # store freq
        dic = {}
        # store ans
        ans = []

        for n in nums:
            # record freq, get value from dic according to key and default value is 0
            dic[n] = dic.get(n, 0) + 1
            if dic[n] > 1:
                ans.append(n)
        
        return ans
```

``` java

```

- question: LC448 找到所有数组中消失的数字 link: https://leetcode.cn/problems/find-all-numbers-disappeared-in-an-array/
    - answer:
``` py
# python code
# 如果遍历1—len(nums)+1，去寻找对应值在nums出现与否会超时。
# 不允许使用额外空间，利用nums充当字典，先遍历nums，nums中的值作为key，改变对应key的value为负值以此标记此值是否出现过，最后筛选value大于0的key则是没出现过的key。
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        # get n from nums as the key to reverse nums[n]
        for n in nums:
            # because the value appeared is negative, use abs to get positive value
            nums[abs(n)-1] = - abs(nums[abs(n)-1])

        # python一行赋值list [目标值 循环方式 条件]
        ans = [n+1 for n in range(len(nums)) if nums[n] > 0]
        
        return ans
```

``` java

```

- question: LC1002 查找共用字符 link: https://leetcode.cn/problems/find-common-characters/
    - answer:
``` py
# python code
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        # simple version
        minFreq = [float("inf")] * 26

        for word in words:
            freq = [0] * 26
            for latter in word:
                freq[ord(latter) - ord("a")] += 1
            
            for i in range(26):
                minFreq[i] = min(minFreq[i], freq[i])
        
        ans = []
        for i in range(26):
            ans.extend([chr(i + ord("a"))] * minFreq[i])

        return ans
```
```python
# python code
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        # enhanced version
        # Counter to create a dic about the string count the freq for every char
        freq = Counter(words[0])

        for word in words:
            freq &= Counter(word)

        # Counter.elements() returns value keys, if "a":3 then "a a a"
        return list(freq.elements())

        # more enhanced version
        # reduce叠加遍历 reduce(function, list)
        # return list(reduce(lambda x, y: x & y, map(collections.Counter, words)).elements())
```

``` java

```

- question: LC1370 上升下降字符串 link: https://leetcode.cn/problems/increasing-decreasing-string/
    - answer:
``` py
# python code
# 如果题目指出字符串只有a-z最好使用26长度的数组
# 字典也可以进行排序 sorted(dic, key=some key)
class Solution:
    def sortString(self, s: str) -> str:
        alpha = [0] * 26
        # count for s
        for l in s:
            alpha[ord(l)-ord("a")] += 1
        
        ans = []

        while len(ans) < len(s):
            # start from min
            for i in range(26):
                if alpha[i]:
                    ans.append(chr(i + ord("a")))
                    alpha[i] -= 1
            # start from max
            for i in range(26):
                if alpha[26-i-1]:
                    ans.append(chr(26-i-1 + ord("a")))
                    alpha[26-i-1] -= 1
        
        # "".join(list) can get a string combination
        return "".join(ans)
```

``` java

```

### date: 2022/11/12 双指针

- question: LC283 移动零 link: https://leetcode.cn/problems/move-zeroes/
    - answer:
```python
```

```java
```

- question: LC26 删除有序数组中的重复元素 link: https://leetcode.cn/problems/remove-duplicates-from-sorted-array/
    - answer:
```python
```

```java
```

- question: LC80 删除排序数组中的重复元素二 link: https://leetcode.cn/problems/remove-duplicates-from-sorted-array-ii/
    - answer:
```python
```

```java
```

- question: LC27 移除元素 link: https://leetcode.cn/problems/remove-element/
    - answer:
```python
```

```java
```

- question: LC344 反转字符串 link: https://leetcode.cn/problems/reverse-string/
    - answer:
```python
```

```java
```

- question: LC125 验证回文串 link: https://leetcode.cn/problems/valid-palindrome/
    - answer:
```python
```

```java
```

- question: LC11 盛最多水的容器 link: https://leetcode.cn/problems/container-with-most-water/
    - answer:
```python
```

```java
```

- question: LC1480 一维数组的动态和（前缀和） link: https://leetcode.cn/problems/running-sum-of-1d-array/
    - answer:
```python
```

```java
```

- question: LC238 除自身以外数组的乘积 link: https://leetcode.cn/problems/product-of-array-except-self/
    - answer:
```python
```

```java
```
