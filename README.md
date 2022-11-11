# LeecodeNoteFor2023
drive link: https://drive.google.com/drive/folders/1e4Lboc4y1uaDwOWHhmAIXtQHzPPXAJVB


task link: https://ke.qq.com/course/package/31104?flowToken=1039500


Learning Time: 2:00-6:00 7:30-10:30 7h


## date: 2022/11/11 数组字符串

### question: input/output基础

-  link: https://www.nowcoder.com/test/27976983/summary#question

    - ACM模式下Java代码格式

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
      //从控制台输入
      Scanner scanner = new Scanner(System.in);
      String str = scanner.nextLine();
      String res = "";
      System.out.Println(res);
    }
  }
```

    - ACM模式下JavaScript(V8)代码格式

```javaScript
//从控制台输入
const str = readline();
let res = str
print(res);//或使用console.log(res)
```

    - ACM模式下JavaScript(Node)代码格式

        - 单行

```js
const readline = require('readline')

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
})

rl.on('line', function(line) {
      let res = line
      console.log(res)
})

```

        - 多行输入

```js
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});


const inputArr = [];
rl.on('line', function(line){
    inputArr.push(line);//将输入流转换为数字类型保存到inputArr中
}).on('close', function(){
    sortScore(inputArr);//调用解决函数并输出
})

//解决函数
function sortScore(inputArr) {
    
}

```



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

``` js
// Js code
const readline = require("readline");

const rl = readline.createInterface({
    input: process.stdin,
    output:process.stdout
})

rl.on("line", function line(line) {
    let res = ""
    for (var i = line.length - 1; i >= 0; i--) {
        res += line[i];
    }
    console.log(res)
});
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

``` js
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});
//js遇到多行输入问题时，首先用rl.on('line', function(line){})逐行读取字符串存入inputArr中，随后在.on('close', function())中用特定函数对inputArr处理
const inputArr = [];
rl.on('line', function(line){
    inputArr.push(line);//将输入流转换为数字类型保存到inputArr中
}).on('close', function(){
    sortScore(inputArr);//调用解决函数并输出
})

//解决函数 
function sortScore(inputArr) {
    let studentNum = inputArr[0];
    let flag = parseInt(inputArr[1]);
    let students = [];

    // push the students into the array
    // js 的数组可以存json类型的数据，即键值对
    for (let i = 0; i < studentNum; i++) {
        var line = inputArr[2+i].split(" ");
        var name = line[0];
        var score = parseInt(line[1]);
        students.push({"name":name, "score":score, "index":i});
    }

    // sort the array
    // js sort默认情况是按照从小到大排序，如果数据是json键值对，那么需要编写sort的回调函数来定义顺序规则，升序s1-s2，降序s2-s1。json数据可用.name的方法进行比较
    if (flag == 0) {
        students.sort((s1, s2) => {
            return s2.score - s1.score || s1.index - s2.index
        })
    } else if (flag == 1) {
        students.sort((s1, s2) => {
            return s1.score - s2.score
        })
    }
    for (var student of students) {
        console.log(student.name + " " + student.score);
    }
}

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
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var findDuplicates = function(nums) {
    let res =[];
    nums.sort();
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] == nums[i-1]) {
            res.push(nums[i]);
        }
    }
    return res;
};
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

``` js
/**
 * 使用Js set不能存储重复值的特性以及set.has()方法判断nums中的缺失值
 * @param {number[]} nums
 * @return {number[]}
 */
var findDisappearedNumbers = function(nums) {
    let set = new Set();
    let res = [];
    // add nums into the set
    for (let i = 0; i < nums.length; i++) {
        set.add(nums[i]);
    }
    // vertify every num from [1,n] if they are existed in the set
    for (let i = 1; i <= nums.length; i++) {
        if (!set.has(i)) {
            res.push(i);
        } 
    }
    return res;
};
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
