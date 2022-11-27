# LeecodeNoteFor2023
drive link: https://drive.google.com/drive/folders/1e4Lboc4y1uaDwOWHhmAIXtQHzPPXAJVB


task link: https://ke.qq.com/course/package/31104?flowToken=1039500


Learning Time: 2:00-6:00 7:30-10:30 7h


### 数组字符串

- question: input/output基础 link: https://www.nowcoder.com/test/27976983/summary#question

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
// 自己的思路
//  * @param {string[]}
//  * @return {string[]}
//  */
// var commonChars = function(words) {
//     let res = [];
//     let firstMap = new Map()
//     for (let j = 0; j < words[0].length; j++) {
//         if (firstMap.has(words[0][j])) {
//             firstMap.set(words[0][j], firstMap.get(words[0][j]) + 1 );
//         } else {
//             firstMap.set(words[0][j], 1);
//         }
//     }
//     for (let i = 0; i < words.length; i++ ) {
//         let map = new Map();
//         let word = words[i];
//         for (let j = 0; j < word.length; j++) {
//             if (map.has(words[0][j])) {
//                 map.set(words[0][j], firstMap.get(words[0][j]) + 1 );
//             } else {
//                 map.set(words[0][j], 1);
//             }
//         }
//         firstSet = res = testSame(map, firstMap);
//     }
//     return res;
// };

// function testSame(map1, map2){
//     let res = new Map();
//     const iterator = map1.values();

//     for(let pair1 of map1) {
//         console.log("pair1 is ", pair1.key,  pair1.value)
//         for (let pair2 of map2) {
//             if (pair1.key == pair2.key) {
//                 res.set(pair1, (pair1.value > pair2.value)?pair2.value:pair2.value)
//             }
//         }
//     }
//     return res;
// }

/**
 * @param {string[]} words
 * @return {string[]}
 */
//主要思路为建立一个26个字母组成的arr来记录每单个单词的字母出现顺序，然后将arr放入arrlist当中，最后遍历arraylist26遍，每遍确定一个字母的数量，然后把对应数量的数组置于res结果数组中。
var commonChars = function(words) {
    let res = [];
    let arrayList = [];
    for (let word of words) {
        let array = new Array(26).fill(0); //.fill可以批量填充数组的值
        for (let char of word) {
            array[char.charCodeAt() - "a".charCodeAt()]++; //charCodeAt可以找对应字母deASCII码
        }
        arrayList.push(array);
    }

    for (let i = 0; i<26; i++) {
        let min = 100;
        for (let arr of arrayList) {
            if (arr[i] < min) {
                min = arr[i]
            }
        }
        for (let j = 0; j < min; j++) {
            res.push(String.fromCharCode(i + "a".charCodeAt()));
        }
    }
    return res;
};


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

``` js
/**
 * @param {string} s
 * @return {string}
 */

//  main idea: 使用数组的index作为字母键值对的key，Value作为字母出现的次数，将字符串s中的字母进行录入到数组。录入后，使用do while 语句先将26个元素遍历一遍，搞出第一遍的顺序，遍历时减少对应数组的value值，同时如果value依然大于0，就代表还要继续遍历，unfinish就是变为true。然后在while中以unfinish作为条件继续遍历。要实现反向顺序，就要使用另外一个boolean变量 inorder进行操作，默认正序，每轮遍历自目前，都要将此值反转。
var sortString = function(s) {
    let res = [];
    let alphaList = new Array(26).fill(0);
    let unfinish;
    let inorder = true;
    // add the data into alphaList
    for(let char of s) {
        alphaList[char.charCodeAt() - "a".charCodeAt()]++;
    }
    // 
    do {
        unfinish = false;
        if (inorder) {
            inorder = !inorder;
            for (let i = 0; i < 26; i ++) {
                if (alphaList[i]>0) {
                    res.push(String.fromCharCode("a".charCodeAt() + i));
                    alphaList[i]--;
                }
                if (alphaList[i]>0) {
                    unfinish = true;
                }
            }
        } else {
            inorder = !inorder;
            for (let i = 25; i >= 0; i --) {
                if (alphaList[i]>0) {
                    res.push(String.fromCharCode("a".charCodeAt() + i));
                    alphaList[i]--;
                }
                if (alphaList[i]>0) {
                    unfinish = true;
                }
            }
        }
    } while (unfinish)
    return res.join("");
};

// 借鉴
// unfinish 和 inorder不必要，可以使用(res.length=s.length)对循环进行判断
```

### 双指针

- question: LC283 移动零 link: https://leetcode.cn/problems/move-zeroes/
    - answer:
```python
# python code
# like quick sort
# 双指针，右指针指向的位置不为0时与左之指针交换
# 可以保持相对顺序，如果两者都不为0时，同时右移一格，并不会交换不为0的值。
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        
        left, right = 0,0

        while right < n:
            # 不为零可以写作 if nums[right]:
            if nums[right] != 0:
                nums[right], nums[left] = nums[left], nums[right]
                left += 1
            right += 1

        return nums
```

```java
// /**
//  * @param {number[]} nums
//  * @return {void} Do not return anything, modify nums in-place instead.
//  */
// // 方法1：使用双指针，两个指针全部从0到len, 左指针是代表按顺序的数组全部元素，思想是一位一位往里面填非零的数。右指针遍历数组查看非零的数，并将非零的数与左指针数值交换。
// var moveZeroes = function(nums) {
//     let res = [];
//     let zeros = [];
//     let left = 0;
//     for (let i = 0; i < nums.length; i ++) {
//         if (nums[i] !== 0) {
//             let temp = nums[i];
//             nums[i] = nums[left];
//             nums[left] = temp;
//             left++;
//         }
//     }
// };

// 方法2：使用slice删除0元素，同时在数组后面补0
var moveZeroes = function(nums) {
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] === 0) {
            nums.slice(0, i).concat(nums.slice(i+1, nums.length));
            nums.push(0);
        }
    }
};
```

- question: LC26 删除有序数组中的重复元素 link: https://leetcode.cn/problems/remove-duplicates-from-sorted-array/
    - answer:
```python
# python code
# 双指针，左指针记录唯一元素，如果重复，右指针右移直到不重复。
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:

        left, right = 1,1

        while right < len(nums):
            # 用加法不太好，容易超出范围，最好用减法
            # if not nums[right] == nums[left]:
            #     nums[left + 1] = nums[right]
            if nums[right] != nums[left - 1]
                nums[left] = nums[right]
                left += 1
            
            right += 1

        # left最终指向需要数组的后一格
        return left
```

```java
/**
 * @param {number[]} nums
 * @return {number}
 */
// 方法一： 快慢指针（慢指针变换条件为快指针与快指针前一位比较），slow的作用是一位一位的将符合条件的数字填入数组。条件为通过fast和fast前一位比较，确定nums[slow]的值。fast与fast前一位一致，那么就不改变slow，如果不一致没那么就可以使nums[slow]=nums[fast]。此外条件还可以比较slow和fast位置是否相等，如果不相等的话，那么就用fast位置的数值填入slow位置
 var removeDuplicates = function(nums) {
    let slow = 0;
    let fast = 1;
    while (fast < nums.length) {
        if (nums[fast] !== nums[slow]) {
            nums[slow + 1] = nums[fast];
            slow++;
        }
        fast++;
    }
    return slow+1;
};

// 方法二：使用splice，对nums从第一位left进行遍历，判断left位置和left上一位的数值是否相等，相等的话就继续检测下一位是否依然相等，然后统计出相等树枝的数量len，然后对nums数组使用nums.splice(left, len)进行裁剪。
 var removeDuplicates = function(nums) {
    let left = 1;
    while (left < nums.length) {
        if (nums[left] != nums[left - 1]) {
            left++;
        } else {
            let len = 1;
            while (nums[left-1] == nums[left+len]) {
                len++;
            }
            nums.splice(left, len);
        }
    }
};
```

- question: LC80 删除排序数组中的重复元素二 link: https://leetcode.cn/problems/remove-duplicates-from-sorted-array-ii/
    - answer:
```python
# python code
# 有个重复的就去检查前第几个数，并且双指针初始化时要相应改变。同时，用减法可以避免out of index的问题。
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        n = len(nums)

        left, right = 2,2

        while right < n:

            if nums[right] != nums[left - 2]:
                nums[left] = nums[right]
                left += 1

            right += 1

        # left最终指向需要数组的后一格
        return left
```

```java
/**
 * @param {number[]} nums
 * @return {number}
 */
// 同样的快慢指针，快慢指针一同从第3个元素出发，检验慢指针的前第二位是否与fast值相等，如果不相等，那么就对慢指针位置用快指针赋值，若果相等，那么慢指针不动，继续用下一个fast比较，如果不同再换。

var removeDuplicates = function(nums) {
    let slow = fast = 2;
    if (nums.length <= 2) return 2;
    while (fast < nums.length) {
        if (nums[slow-2] != nums[fast]) {
            nums[slow] = nums[fast];
            slow++;
        }
        fast++;
    }
    return slow;
};

//方法二：splice
var removeDuplicates = function(nums) {
    let start = 2;
    while (start < nums.length) {
        if (nums[start] == nums[start-2]) {
            let len = 1;
            while (nums[start + len] == nums[start]) {
                len++;
            }
            nums.splice(start, len)
        }
        start++;
    }
};
```

- question: LC27 移除元素 link: https://leetcode.cn/problems/remove-element/
    - answer:
```python
# python code
# 所有删除元素且不占用额外空间，都可以使用交换的方式。
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:

        n = len(nums)

        left, right = 0,0

        while right < n:
            if nums[right] != val:
                nums[left], nums[right] = nums[right], nums[left]
                left += 1

            right += 1

        return left

```

```java
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
// 方法一：快慢指针
var removeElement = function(nums, val) {
    let slow = fast = 0;
    while (fast < nums.length) {
        if (nums[fast] != val) {
            nums[slow] = nums[fast]
            slow++;
        }
        fast++;
    }
    return slow;
};



// 方法二:暴力splice
// var removeElement = function(nums, val) {
//     let start = 0;
//     while (start < nums.length) {
//         if (nums[start] == val) {
//             let len = 1;
//             while (nums[start] == nums[start+len]) {
//                 len++;
//             }
//             nums.splice(start,len);
//         }
//         start++;
//     }
// };
```

- question: LC344 反转字符串 link: https://leetcode.cn/problems/reverse-string/
    - answer:
```python
# easy to swap
# 双指针，一个开头， 一个结尾
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        
        n = len(s)

        right, left = 0, n-1
        
        while right < left:
            s[right], s[left] = s[left], s[right]
            right += 1
            left -= 1

        return s 
```

```java
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseString = function(s) {
    let left = 0;
    let right = s.length - 1;
    while (left < right) {
        let temp = s[left];
        s[left] = s[right];
        s[right] = temp;
        left ++;
        right --;
    }
    return s;
};
```

- question: LC125 验证回文串 link: https://leetcode.cn/problems/valid-palindrome/
    - answer:
```python
# python code
# 重点在于处理字符串，去除空格用str.strip()，去除别的字符用str.isalnum()，只包含数字和字母时返回TRUE。
class Solution:
    def isPalindrome(self, s: str) -> bool:

        s = "".join(ch.lower() for ch in s if ch.isalnum())

        left, right = 0, len(s)-1

        while left < right:
            if s[left] != s[right]:
                return False
            
            left += 1
            right -= 1

            
        return True
```

```java
var isPalindrome = function(s) {
    s=s.replace(/[^a-zA-Z0-9]/g,"").replace(/\s/g,"").toLowerCase(); // replace 函数替换字符串中的非字母字符
    //toLowerCase()用于对字符串进行全小写处理
    let left = 0;
    let right = s.length - 1;
    while (left <= right) {
        if (s[left] !== s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
};
```

- question: LC11 盛最多水的容器 link: https://leetcode.cn/problems/container-with-most-water/
    - answer:
```python
# python code
# 双指针，一头一尾，每次找最短边向内收缩直到双指针相遇。
class Solution:
    def maxArea(self, height: List[int]) -> int:
        n = len(height)

        left, right = 0, n-1
        v = 0

        while left < right:

            temp = min(height[left], height[right]) * (right - left)
            
            v = max(v, temp)

            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        
        return v
```

```java
/**
 * @param {number[]} height
 * @return {number}
 */
// 收尾双指针向内收缩，短的一边收缩。
var maxArea = function(height) {
    let max = 0;
    let left = 0;
    let right = height.length - 1;
    while (left < right){
        let width = right - left;
        let shortest = height[left] < height[right] ? height[left++] : height[right--];
        let currentVolume =  width * shortest;
        if (currentVolume > max) {
            max = currentVolume;
        }
    }
    return max;
};
```


### 一维数组

- question: LC1480 一维数组的动态和（前缀和） link: https://leetcode.cn/problems/running-sum-of-1d-array/
    - answer:
```python
# python code
# 当前项等于前一项加上自己。
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:

        for i in range(1, len(nums)):
            nums[i] += nums[i-1]
        
        return nums
```

```java
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var runningSum = function(nums) {
    let runningSum = [];
    let sum = 0;
    for (let i = 0; i < nums.length; i++) {
        sum += nums[i]
        runningSum[i] = sum;
    }
    return runningSum;
};
```

- question: LC238 除自身以外数组的乘积 link: https://leetcode.cn/problems/product-of-array-except-self/
    - answer:
```python
# python code
# 除自身外的除数分两部分，一部分是左边所有数相乘，一部分是右边所有数相乘，最后两边相乘。
# 计算单边是，分开计算，叠加会更高效
# 只用一个数组来存储可以节省空间，但要考虑到最左边和最右边的点，初始化为1。
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n = len(nums)
        ans = [0] * n

        ans[0] = 1 
        
        for i in range(1, n):
            ans[i] = ans[i-1] * nums[i-1]
        
        r = 1
        
        # for i in reversed(range(length)):
        # reversed 可以使得 i 从n到0进行遍历
        for i in range(1, n+1):
            ans[n-i] = ans[n-i] * r
            r *= nums[n-i]

        return ans
```
```java
// 左右积合一起
var productExceptSelf = function(nums) {
  let ans = [];
  let left = [];
  left.push(1);
  let right = [];
  right.push(1);
  let len = nums.length;
  for (let i = 1; i < len; i++) {
      left.push(left[i-1] * nums[i-1])
      right.push(right[i - 1] * nums[len - i])
      console.log("nums[len - i - 1]", nums[len - i - 1]);
  }
  right = right.reverse();
  for (let i = 0; i < len; i++) {
      console.log("i: ", i, "left: ", left[i], "right: ", right[i]);
      ans[i] = left[i] * right[i];
  }
  return ans;
};

console.log(productExceptSelf([1,2,3,4]));
```

- question: LC941 有效的山脉数组 link: https://leetcode.cn/problems/valid-mountain-array/
    - answer:
```python
# python code
# 双循环检索，第一个循环检索上坡，第二个循环检测下坡，中间任何间断则报错。
class Solution:
    def validMountainArray(self, arr: List[int]) -> bool:
        N = len(arr)
        i = 0

        while i + 1 < N and arr[i] < arr[i + 1]:
            i += 1

        if i == 0 or i == N - 1:
            return False

        while i + 1 < N and arr[i] > arr[i + 1]:
            i += 1

        return i == N - 1
```

```java

//顺序扫描数组，查看扫描一升一降(或)后的i的位置是否是原数组的长度。如果短了那么说明不是山脉数组。但是要注意山脉数组的最高点不能是第一位和最后一位
var validMountainArray = function(arr) {
    const N = arr.length;
    let i = 0;

    // 递增扫描
    while (i + 1 < N && arr[i] < arr[i + 1]) {
        i++;
    }

    // 最高点不能是数组的第一个位置或最后一个位置
    if (i === 0 || i === N - 1) {
        return false;
    }

    // 递减扫描
    while (i + 1 < N && arr[i] > arr[i + 1]) {
        i++;
    }

    return i === N - 1;
};
```

- question: LC189 旋转数组 link: https://leetcode.cn/problems/rotate-array/
    - answer:
```python
# python code
# 关键点一：原地改动nums，任何的赋值操作都会导致nums的id变化，只对nums内的元素做操作才不会导致id变化。
# nums = nums[::-1] 会导致nums的id变化
# nums[:] = nums[::-1] 不会导致nums的id变化，因为nums[:]表示对nums内每个元素对应赋值。
# 关键点二：k值大于len(nums)时，需要对k做处理，当k等length时，相当于对数组没操作，所以对length取余则可以得到最终的k。
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        k = k % len(nums)
        
        nums[:] = nums[::-1]

        nums[k:len(nums)] = nums[k:len(nums)][::-1]

        nums[0:k] = nums[0:k][::-1]

        return nums
```
```java
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
// 旋转数组，将数组切为两份，然后将后一份放置于前一份前。注意本题需要最后在原数组的地址上进行数组变更，另外要注意旋转次数大于数组长度的情况，使用取余将问题简化。
var rotate = function(nums, k) {
    let len = nums.length;
    k = k % len;
    let num1 = nums.slice(len - k, len);
    let num2 = nums.slice(0, len - k);
    let newNums = num1.concat(num2);
    for (let i = 0; i < len; i ++) {
        nums[i] = newNums[i]
    }
    return nums;
};
```

- question: LC665 非递减数列 link: https://leetcode.cn/problems/non-decreasing-array/
    - answer:
```python
# python code
# 遇到突变时，检测突变时检测当前位置与前两位的大小，必须使得当前位置大于前两位的值，否则就需要更改不止一次，如果是小于前两位的值，则当前位置能选择的最小值则是前一位的值。
class Solution:
    def checkPossibility(self, nums: List[int]) -> bool:
        n = len(nums)

        flag = True

        for i in range(1, n):
            if nums[i] < nums[i-1]:
                if flag:
                    flag = False
                else:
                    return flag

                if i > 1 and nums[i] < nums[i-2]:
                    nums[i] = nums[i-1]

        return True
```
```java
[3,4,2,3]
为了方便处理我前面和后面加入两个哨兵元素后数组变为
[-Infinity,3,4,2,3,Infinity]
当i等于3时，4>2，出现了一个减小的情况。
关键来了，这时我们有两种改变方法，满足一个即可。
将4改为2 ，这时必须满足 4左边的元素小于等于2
将2改为4，这时必须满足4小于等于2右边的元素。 如果上述两种都不能成立其中一个，那么就说不能修改，返回false即可。
关键就是上面的两个情况。相信各位大佬能简单看懂。希望各位大佬提出修改意见

var checkPossibility = function(nums) {
    let sum = 0;
    nums.push(Infinity)
    nums.unshift(-Infinity)
    for (let i = 2; i < nums.length - 1; i++) {
        if (nums[i-1]> nums[i]) {
            sum++;
            if (nums[i-1]>nums[i+1] && nums[i] < nums[i-2]) return false;
        }
        if (sum>1) {
            return false;
        }
        
    }
    return true;
};
```

- question: LC228 汇总区间 link: https://leetcode.cn/problems/summary-ranges/
    - answer:
```python
# python code
# 移动end，满足条件则end移动，否则更新start和end，最后跳出循环后还得再append。
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:

        n = len(nums)
        if not nums:
            return []

        start, end = nums[0],nums[0]

        ans = []

        for i in range(1, n):
            if nums[i] == end + 1:
                end = nums[i]
            else:
                if start != end:
                    ans.append("->".join((str(start), str(end))))
                else:
                    ans.append(str(start))

                start, end = nums[i], nums[i]
        
        if start != end:
            ans.append("->".join((str(start), str(end))))
        else:
            ans.append(str(start))

        return ans
```
```java
/**
 * @param {number[]} nums
 * @return {string[]}
 */
// var summaryRanges = function(nums) {
//     let end = 1;
//     let res = [];
//     while (end < nums.length) {
//         start = end - 1;
//         while (nums[end - 1] + 1 == nums[end]) {
//             end++;
//         }
//         if (start == end - 1) {
//             res.push(nums[start].toString());
//             end++
//         } else {
//             res.push(nums[start]+"->"+nums[end]);
//         }
//     }
//     return res;
// };

var summaryRanges = function(nums) {
    let piv = 0;
    let res = [];
    while (piv < nums.length) {
        start = piv;
        while (nums[piv] + 1 == nums[piv + 1]) {
            piv++;
        }
        if (piv == start) {
            res.push(nums[start].toString());
        } else {
            res.push(nums[start]+"->"+nums[piv]);
        }
        piv++;
    }
    return res;
};
```

- question: LC163 缺失的区间(vip) link: https://blog.csdn.net/ft_sunshine/article/details/103445054
    - answer:
```python
# python code
def summaryRanges(nums, lower, upper):

    n = len(nums)
    if not nums:
        return []

    ans = []
    start = lower
    
    for i in range(1, n):
        if nums[i] == start + 1:
            start = nums[i]
        else:
            start += 1
            if nums[i] < upper:
                end = nums[i] - 1
                if start != end:
                    ans.append("->".join((str(start), str(end))))
                else:
                    ans.append(str(start))
                    
            else:
                end = upper
                if start != end:
                    ans.append("->".join((str(start), str(end))))
                else:
                    ans.append(str(start))
                break
                
            start = nums[i]

    if upper > nums[n-1]:
        start += 1
        end = upper
        if start != end:
            ans.append("->".join((str(start), str(end))))
        else:
            ans.append(str(start))
            
    return ans
```
```java
//简化版
var antiSummaryRanges = function(nums) {
  let res = [];
  let piv = 0;
  let start = 0;
  let end = 0;
  while (piv < nums.length - 1) {
    console.log("piv ", piv)
    if (nums[piv] + 1 != nums[piv+1]) {
      start = nums[piv] + 1;
      let len = 0;
      console.log("start " + start);
      end = nums[piv+1] - 1;
      console.log("end " + end);


      // print the array
      if (end == start) {
        res.push(start);
      } else {
        res.push(start+"->"+end);
      }
    }
    piv++;
  }
  return res;
}

console.log(antiSummaryRanges([0, 1, 3, 50, 75]));
```

- question: LC31 下一个排列 link: https://leetcode.cn/problems/next-permutation/
    - answer:
```python
# python code
# 先从尾部开始，找到下降点，下降点右边的点比较，找到大于下降点的最小值，与之交换，交换后，将下降点右边的点倒序，得到下一个值。
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)

        i, k = n-2, n-1

        while i >= 0 and nums[i] >= nums[i+1]:
            i -= 1
        
        if i >= 0:
            while nums[i] >= nums[k]:
                k -= 1
            
            nums[i], nums[k] = nums[k], nums[i]
        
        i, k = i + 1, n - 1

        while nums[i] > nums[k] and i < k:
            nums[i], nums[k] = nums[k], nums[i]
            i += 1
            k -= 1

        return nums
        
```
```java
不会啊，交给时间吧
 var nextPermutation = function(nums, n = nums.length) {
  if (!n) return []
  let p = n - 1, p1 = n - 1, nearIndex = 0, minD = Infinity
  while(p > 0) {
    if (nums[p] > nums[p - 1]) break
    p -- // p为末尾开始算起的第一个非递减序列的起始值
  }
  if (p === 0) {
    nums.sort((a, b) => a - b)
    return nums
  }
  while (p1 > p - 1) {
    if (minD > nums[p1] - nums[p - 1] && nums[p1] > nums[p - 1]) {
      minD = nums[p1] - nums[p - 1]
      nearIndex = p1
    }
    p1 --
  }
  // 交换邻近大值
  let tmp = nums[nearIndex]
  nums[nearIndex] = nums[p - 1
  nums[p - 1] = tmp

  for (let i = p; i < n; i++) { // 在区间i ~ n - 1做插排
    let min = Infinity, k = i
    for (let j = i; j < n; j++) {
      if (min > nums[j]) {
        min = nums[j]
        k = j
      }
    }
    if (k !== i) {
      nums[k] = nums[i]
      nums[i] = min
    }
  }
  return nums
};

```

- question: LC135 分发糖果（困难） link: https://leetcode.cn/problems/candy/
    - answer:
```python
# python code
# 两次遍历，先从右边开始，找比右边大的，再从左边开始，找比左边大的。两者取最大值
class Solution:
    def candy(self, ratings: List[int]) -> int:
        n = len(ratings)
        left = [1] * n

        for i in range(1, n):
            if ratings[i] > ratings[i - 1]:
                left[i] = left[i - 1] + 1

        right = 1

        for i in reversed(range(n-1)):
            if ratings[i] > ratings[i + 1]:
                right += 1
            else:
                right = 1

            left[i] = max(right, left[i])
        
        return sum(left)
```
```java
//我们遍历该数组两次，处理出每一个学生分别满足左规则或右规则时，最少需要被分得的糖果数量。每个人最终分得的糖果数量即为这两个数量的最大值。
var candy = function(ratings) {
    const n = ratings.length;
    const left = new Array(n).fill(0);
    for (let i = 0; i < n; i++) {
        if (i > 0 && ratings[i] > ratings[i - 1]) {
            left[i] = left[i - 1] + 1;
        } else {
            left[i] = 1;
        }
    }

    let right = 0, ret = 0;
    for (let i = n - 1; i > -1; i--) {
        if (i < n - 1 && ratings[i] > ratings[i + 1]) {
            right++;
        } else {
            right = 1;
        }
        ret += Math.max(left[i], right);
    }
    return ret;
};

```

- question: LC605 种花问题 link: https://leetcode.cn/problems/can-place-flowers/
    - answer:
```python
# python code
# 找到1的位置，记录下来，每次找到1与之前的1的位置相减之后再减2并整除2，得到可以种花的位置。循环结束后要寻找n+1的位置与当前pre的位置之间是否可以再种。
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:

        m = len(flowerbed)

        pre, cnt = -1, 0

        for i in range(m):
            if flowerbed[i] == 1:
                if pre == -1:
                    cnt += i//2
                else:
                    cnt += (i - pre - 2) // 2
                pre = i

                if cnt >= n:
                    return True
        
        if pre == -1:
            cnt += (m + 1) // 2
        else:
            cnt += (m - pre - 1) // 2
        
        return True if cnt >= n else False
        
```
```java
// /**
//  * @param {number[]} flowerbed
//  * @param {number} n
//  * @return {boolean}
//  */
// var canPlaceFlowers = function(flowerbed, n) {
//     let space = 0;
//     let pivot = 0;

//     if (n == 0) {
//         return true
//     }

//     if (flowerbed.length == 1) {
//         console.log("!", flowerbed[0])
//         return flowerbed[0] == 0;
//     }
//     if (flowerbed.length == 2) {

//         if (flowerbed[1] == 0 && flowerbed[0] == 0) {
//             space++
//         }
//         return space>=n;
//     }


//     if (flowerbed[0] == 0 && flowerbed[1] == 0) {
//         flowerbed[0] = 1;
//         space++;
//         console.log("pre", space);
//     }
//     while (pivot < flowerbed.length - 1) {
//         if (flowerbed[pivot] == 0) {
//             if (flowerbed[pivot - 1] != 1 && flowerbed[pivot + 1] != 1) {
//             flowerbed[pivot] = 1;
//             space++;
//             console.log("in", space);
//         }
//         }
//         pivot ++;
//     }
    
//     if (flowerbed[flowerbed.length - 1] == 0 && flowerbed[flowerbed.length - 2] == 0) {
//         flowerbed[0] = 1;
//         space++;
//         console.log("end", space);
//     }
//     console.log(space)
//     return space>=n
// };

var canPlaceFlowers = function(flowerbed, n) {
    let space = 0;
    let pivot = 0;


    // 当存在当前值需要前后比较时，将首元素和尾元素的特殊情况可以使用||与前后值的比较相结合，比如，如果前置比较||首值的特殊情况 。
    while (pivot < flowerbed.length) {
        if (flowerbed[pivot] == 0) {
            if ((pivot == 0 || flowerbed[pivot - 1] == 0) && (pivot == flowerbed.length - 1 || flowerbed[pivot + 1] == 0)) {
            flowerbed[pivot] = 1;
            space++;
            console.log("pivot is ", pivot)
            }
        }
        pivot ++;
    }
    
    console.log(space)
    return space>=n
};
```

- question: LC860 柠檬水找零 link: https://leetcode.cn/problems/lemonade-change/
    - answer:
```python
# python code
# hard code, find all possible situations.
from collections import Counter
class Solution:
    def lemonadeChange(self, bills: List[int]) -> bool:
        five, ten = 0,0
        for i in bills:
            if i == 5:
                five += 1

```
```java
/**
 * @param {number[]} bills
 * @return {boolean}
 */
var lemonadeChange = function(bills) {
    let len = bills.length;
    let five = 0;
    let ten = 0;
    for (let i= 0; i < len; i++) {
        let money = bills[i];
        if(money == 5) {
            five++;
        } else if (money == 10) {
            ten++
        }
         {
            while (money > 10 && ten > 0){
                money-=10;
                ten--;
            }
            while (money > 5) {
                console.log(money)
                money -= 5;
                five --;
            }
            if (five<0) {
                return false;
            }
        }
    }
    return true;
};
```

### 二维数组

- question: lc867 矩阵转置 link: https://leetcode.cn/problems/transpose-matrix/
    - answer:
```python
# python code

        for i in range(n):
            dic1 = {}
            dic2 = {}
            for j in range(n):
                if board[i][j] != '.':
                    if board[i][j] in dic1:
                        return False
                    else:
                        dic1[board[i][j]] = 1

                if board[j][i] != '.':
                    if board[j][i] in dic2:
                        return False
                    else:
                        dic2[board[j][i]] = 1

        for i in range(0,n,3):
            for j in range(0,n,3):
                dic = {}
                for m in range(n):
                    if board[i+(m//3)][j+(m%3)] != '.':
                        if board[i+(m//3)][j+(m%3)] in dic:
                            return False
                        else:
                            dic[board[i+(m//3)][j+(m%3)]] = 1

        return True    
```
```java
/**
 * @param {number[][]} matrix
 * @return {number[][]}
 */
var transpose = function(matrix) {
    let res = [];
    let m = matrix.length;
    let n = matrix[0].length;
    for (let i = 0; i< n; i++) {
        let row = matrix[i];
        let resLine = []

        for (let j = 0; j < m; j++) {
            resLine.push(matrix[j][i]);
        }
        res.push(resLine);
    }
    return res;
};

```

- question: lc48 旋转图像 link: https://leetcode.cn/problems/rotate-image
    - answer:
```python
# python code
# 两种思路解决，第一是通过先转置，再reverse。第二种，找对应关系m[i][j] 对应 m[j][n-1-i]。
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        
        for i in range(n):
            matrix[i][:] = matrix[i][::-1]

```
```java
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */

// js初始定义数组的时候，不要使用fill 要使用 Array.from(Array(n), item => new Array(n).fill(0)将数组变换
var rotate = function(matrix) {
    let n = matrix.length
    let arr = Array.from(Array(n), item => new Array(n).fill(0))
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++){
            arr[j][n - 1 - i] = matrix[i][j]
        }
    }
    console.log(arr);
    for (let i = 0; i < n; i++) {
        for (let j = 0; j < n; j++){
            matrix[i][j] = arr[i][j]
        }
    }
};
```

- question: lc36 有效的数独 link: https://leetcode.cn/problems/valid-sudoku
    - answer:
```python
# python code
# 进行三次扫描，第一次找每一行，第二次找每一列，第三次找每个3x3。其中，最后一步中，m从0~8，对应3x3的行数为m//3，列数为m%3。由此得到3x3内的位置。
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        n = len(board)

        for i in range(n):
            dic1 = {}
            dic2 = {}
            for j in range(n):
                if board[i][j] != '.':
                    if board[i][j] in dic1:
                        return False
                    else:
                        dic1[board[i][j]] = 1

                if board[j][i] != '.':
                    if board[j][i] in dic2:
                        return False
                    else:
                        dic2[board[j][i]] = 1

        for i in range(0,n,3):
            for j in range(0,n,3):
                dic = {}
                for m in range(n):
                    if board[i+(m//3)][j+(m%3)] != '.':
                        if board[i+(m//3)][j+(m%3)] in dic:
                            return False
                        else:
                            dic[board[i+(m//3)][j+(m%3)]] = 1

        return True    
```
```java
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
    // check the line
    for (let i = 0; i<9; i++) {
        let arr = new Array(9).fill(false);
        for (let j = 0; j < 9; j++) {
            if (arr[board[i][j]] == true) {
                console.log(i, j, "return false by row")
                return false;
            } 
            if (board[i][j] != ".") {
                arr[board[i][j]] = true;
            }
        }
    };

    for (let i = 0; i<9; i++) {  
        let arr = new Array(9).fill(false);
        for (let j = 0; j < 9; j++) {
            if (arr[board[j][i]] == true) {
                console.log(i, j, arr[board[j][i]], board[j][i], "return false by column")
                return false;
            } 
            if (board[j][i] != ".") {
                arr[board[j][i]] = true;
            }
        }
    };

    
    // 寻找起始点然后开启3*3小循环
    for (let a = 0; a < 9; a += 3){
        for (let b = 0; b < 9; b+= 3) {
            let arr = new Array(9).fill(false);
            for (let i = a; i < a+3; i++) {
                for (let j = b; j < b+3; j++) {
                    if (arr[board[i][j]] == true) {
                        console.log(i, j, "return false by group")
                        return false;
                    } 
                    if (board[i][j] != ".") {
                        arr[board[i][j]] = true;
                    }
                }
            }
        }
    }
    return true;
};
```

- question: lc73 矩阵置零 link: https://leetcode.cn/problems/set-matrix-zeroes/
    - answer:
```python
# python code
# 利用自身数组的第一行与第一列记录是否需要变为零，同时需要两个变量来记录第一行与第一列是否需要变为全零。进阶版本可以只使用一个变量来记录但过程不是很清晰。
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        row = len(matrix)
        col = len(matrix[0])

        col_flag, row_flag = True, True

        for i in range(row):
            if matrix[i][0] == 0:
                col_flag = False
                break

        for i in range(col):
            if matrix[0][i] == 0:
                row_flag = False
                break

        for i in range(1, row):
            for j in range(1, col):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0
                    matrix[0][j] = 0
        
        for i in range(1, row):
            for j in range(1, col):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0

        if not row_flag:
            for i in range(col):
                matrix[0][i] = 0
        
        if not col_flag:
            for i in range(row):
                matrix[i][0] = 0
```
```java
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function(matrix) {
    let m = matrix.length;
    let n = matrix[0].length;
    let zerosIndexI = new Set();
    let zerosIndexJ = new Set();
    // let arr = Array.from(new Array(m), item => new Array(n).fill(false));
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            // arr[i][j] = true;
            if (matrix[i][j] == 0) {
               zerosIndexI.add(i)
               zerosIndexJ.add(j)
            }
        }
    }
    for (let i = 0; i < m; i++) {
        for (let j = 0; j < n; j++) {
            if (zerosIndexI.has(i) || zerosIndexJ.has(j)) {
                matrix[i][j] = 0;
            }
        }
    }
};
```

- question: lc54 剑指29 螺旋矩阵 link: https://leetcode.cn/problems/spiral-matrix/
    - answer:
```python
# python code
# 外层循环，大循环内有四次小循环，代表最外层。
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:

        n = len(matrix)
        m = len(matrix[0])

        ans = []
        start = 0

        while len(ans) < n*m:

            for i in range(start, m-start):
                ans.append(matrix[start][i])
            if len(ans) == n*m:
                break

            for i in range(1+start, n-start):
                ans.append(matrix[i][m-start-1])
            if len(ans) == n*m:
                break

            for i in reversed(range(start, m-start-1)):
                ans.append(matrix[n-start-1][i])
            if len(ans) == n*m:
                break

            for i in reversed(range(start+1, n-start-1)):
                ans.append(matrix[i][start])
            
            start += 1

        return ans
```
```java
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
    let res =[];
    let m = matrix.length;
    let n = matrix[0].length;
    let row = 0;
    let column = 0;
    let total = m*n;
    console.log(total)
    directionIndex = 0;
    let visited = new Array(m).fill(0).map(() => new Array(n).fill(false));
    // 右下左上
    let directions = [[0,1], [1,0], [0,-1], [-1, 0]];
    for (let i = 0; i < total; i++) {
        visited[row][column] = true;
        console.log(row, column, matrix[row][column])
        res.push(matrix[row][column])
        let Nrow = row + (directions[directionIndex][0]);
        let Ncolumn = column +  (directions[directionIndex][1]);
        if (Ncolumn >= n || Ncolumn <0 || Nrow >= m || Nrow < 0 || visited[Nrow][Ncolumn]) {
            directionIndex = (directionIndex + 1) % 4; 
            
        }
        row = row + (directions[directionIndex][0]);
        column = column +  (directions[directionIndex][1]);
    }
    
    return res;
};
```

- question: lc59 螺旋矩阵二 link: https://leetcode.cn/problems/spiral-matrix-ii/
    - answer:
```python
# python code
# 类似 lc54 但这个是方阵，所以不用做if检测。
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0]*n for _ in range(n)]
        init = 1
        start = 0

        while init <= n*n:

            for i in range(start, n-start):
                matrix[start][i] = init
                init += 1

            for i in range(1+start, n-start):
                matrix[i][n-start-1] = init
                init += 1

            for i in reversed(range(start, n-start-1)):
                matrix[n-start-1][i] = init
                init += 1

            for i in reversed(range(start+1, n-start-1)):
                matrix[i][start] = init
                init += 1
            
            start += 1

        return matrix
```
```java
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    let res = [];
    let matrix = [];
    let row = 0;
    let column = 0;
    let total =n*n;
    directionIndex = 0;
    for (let i = 0; i < n; i++) {
        matrix.push(new Array());
        for (let j = 0; j < n; j++) {
            matrix[i].push(0);
        }
    }
    let visited = new Array(n).fill(0).map(() => new Array(n).fill(false));
    // 右下左上
    let directions = [[0,1], [1,0], [0,-1], [-1, 0]];    
    for (let i = 0; i < total; i++) {
        visited[row][column] = true;
        matrix[row][column] = i+1;
            console.log(matrix)
        let Nrow = row + (directions[directionIndex][0]);
        let Ncolumn = column +  (directions[directionIndex][1]);
        if (Nrow >= n || Ncolumn >= n || Ncolumn <0  || Nrow < 0 || visited[Nrow][Ncolumn]) {
            directionIndex = (directionIndex + 1) % 4; 
            
        }
        row = row + (directions[directionIndex][0]);
        column = column +  (directions[directionIndex][1]);
    }

    for (let i = 0; i<n; i++) {
        res.push(new Array())
        for (let j = 0; j < n; j++) {
            res[i].push(matrix[i][j]);
        }
    }
    
    return res;
};
```

- question: lc498 对角线遍历 link: https://leetcode.cn/problems/diagonal-traverse/
    - answer:
```python
# python code
# 对角线的数量为n + m - 1，当对角线为偶数时，从下往上遍历，当对角线为奇数时，从上往下遍历。当i为偶数且小于行数时，起始点为（i，0），当i大于行数时，起始点为（行数-1，i-(m-1))。
class Solution:
    def findDiagonalOrder(self, mat: List[List[int]]) -> List[int]:
        m = len(mat)
        n = len(mat[0])

        ans = []

        for i in range(n + m - 1):
            if i % 2:
                if i < n:
                    x = 0
                    y = i
                else:
                    x = i - n + 1
                    y = n - 1
                while x < m and y >= 0:
                    ans.append(mat[x][y])
                    x += 1
                    y -= 1
            else:
                if i < m:
                    x = i
                    y = 0
                else:
                    y = i - m + 1
                    x = m - 1
                while x >= 0 and y < n:
                    ans.append(mat[x][y])
                    x -= 1
                    y += 1
        
        return ans

```
```java
/**
 * @param {number[][]} mat
 * @return {number[]}
 */
//利用x, y 遍历数组。因为对角线只有两个方向，我们就用两个方向的情况讨论。方向1为右上方向，他的终止条件是碰到上墙壁和有墙壁。方向2为左下方向，他的终止条件为碰到下墙壁和做墙壁。

var findDiagonalOrder = function(mat) {
    let direction = 1;
    let m = mat.length;
    let n = mat[0].length;
    let total = m * n
    let x = 0;
    let y = 0;
    let res = [];
    for (let i = 0; i<total; i++) {
        res.push(mat[y][x]);
        if (direction == 1) {
            if (x + 1 == n) {
                y++;
                direction = 2;
            } else if (y - 1 < 0){
                x++;
                direction = 2;
            } else {
                x++;
                y--;
            }
        } else {
            if (y + 1 == m) {
                x++;
                direction = 1;
            } else if (x - 1 < 0){
                y++;
                direction = 1;
            } else {
                y++;
                x--;
            }
        }
    }
    return res;
};
```

- question:lc118 杨辉三角 link: https://leetcode.cn/problems/pascals-triangle/
    - answer:
```python
# python code
# 每一行第0和最后一个元素都为1，其他元素都为上一行的第j-1与j项相加之和。第n行m个数用公式为Cmn = n! / m!(n-m)! = cm-1n * ((n-m+1) / m)
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        ans = []

        for i in range(numRows):
            temp = []
            for j in range(i + 1):
                if j == 0 or j == i:
                    temp.append(1)
                else:
                    temp.append(ans[i-1][j-1]+ans[i-1][j])
            ans.append(temp)

        return ans
```
```java
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    let res = new Array(numRows);
    for (let i = 0; i < numRows; i++) {
        
        res[i] = new Array(i+1);
        res[i][0] = 1;
        res[i][i] = 1;
        console.log(res);
        for (let j = 1; j < i; j++) {
            res[i][j] = res[i - 1][j] + res[i - 1][j - 1];
        }
    }
    return res;
};
```

- question: lc119 杨辉三角二 link: https://leetcode.cn/problems/pascals-triangle-ii/
    - answer:
```python
# python code
# 代入公式: ans[i] = ans[i-1] * (n-i+1) / i
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        ans = [1] * (rowIndex + 1)
    
        for i in range(1, rowIndex + 1):

            ans[i] = int(ans[i-1] * (rowIndex - i + 1) / i)
        
        return ans
```
```java
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    let res = [];
    for (let i = 0; i <= rowIndex; i++) {
        let row = new Array(i+1);
        row[0] = 1;
        row[row.length - 1] = 1; 

        for (let j = 1; j < i; j++) {
            row[j] = res[i - 1][j] + res[i - 1][j - 1]
        }
        if (i == rowIndex) {
            return row
        }
        res.push(row);
    }
};
```

### 字符串操作

- question: lc28 实现 strStr() link: https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/
    - answer:
```python
# python code
# 匹配过程中，检测是否有头部，匹配失败后直接移动到头部位置而不是一步一步移动。
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        nh = len(haystack)
        nn = len(needle)

        if nn >= nh:
            return 0 if needle == haystack else -1
        
        start = 0
        nextstart = 0

        flag = False
        first = True

        while start < nh:
            if haystack[start] == needle[0]:
                j = 0
                while j < nn:
                    if j+start < nh and haystack[j+start] == needle[j]:
                        if haystack[j+start] == needle[0] and first:
                            first = False
                            nextstart = j+start
                        flag = True
                        j += 1
                    else:
                        if not first:
                            start = nextstart
                        else:
                            start = j+start-1
                            nextstart = start
                        
                        first = True
                        flag = False
                        break
                if flag:
                    return start
            
            start += 1

        return -1
```
```java
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
var strStr = function(haystack, needle) {
    let hl = haystack.length;
    let nl = needle.length;
    let a = 0;
    let b = 0;
    while (a <= hl) {
        if (haystack[a] == needle[b]) {
            if (b == nl - 1) {
                return a - b;
            }
            b++;
        } else {
            a = a - b;
            b = 0
        }
        a++;
    }
    return -1;
};
```

- question: lc344 反转字符串 link: https://leetcode.cn/problems/reverse-string/
    - answer:
```python
# python code
# 赋值的方式可以通过双指针的形式首尾进行交换，或者反向切片并逐个赋值。
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        
        n = len(s)

        right, left = 0, n-1
        
        while right < left:
            s[right], s[left] = s[left], s[right]
            right += 1
            left -= 1

        return s 
        # s[:] = s[::-1]
        # return s
```
```java
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    let space = " ".charCodeAt();
    let res = 0
    let spaceNum = 0;
    let shouldReturn = s[s.length - 1] == " "? false : true;
    for (let i = s.length - 1; i >= 0; i--) {
        console.log(s[i 
        if (s[i] == " ") {
            if ( shouldReturn) {
                 return  res;
            }
            spaceNum ++;
            continue;
        }
        shouldReturn = true;
        res++;
    }
    return s.length - spaceNum;
};


// 使用前后指针 后指针end记录空位，前指针start记录满足要求的单词，详见得到res
// var lengthOfLastWord = function(s) {
//     let end = s.length - 1;
//     while(end >= 0 && s[end] == ' ') end--;
//     if(end < 0) return 0;
//     let start = end;
//     while(start >= 0 && s[start] != ' ') start--;
//     return end - start;
// };
```

- question: lc345 反转字符串中的元音字母 link: https://leetcode.cn/problems/reverse-vowels-of-a-string/
    - answer:
```python
# python code
# str无法直接更改，需要将str先变为list再去更改，str.lower()变小写，str.upper()变大写。in检查某个元素是否在list中。
class Solution:
    def reverseVowels(self, s: str) -> str:
        n = len(s)
        right, left = 0, n-1

        s = list(s)

        yuan = ['a', 'e', 'i', 'o', 'u']

        while right < left:
            if s[right].lower() in yuan and s[left].lower() in yuan:
                s[right], s[left] = s[left], s[right]
                right += 1
                left -= 1
            elif s[right].lower() in yuan:
                left -= 1
            elif s[left].lower() in yuan:
                right += 1
            else:
                right += 1
                left -= 1
        
        return "".join(s)
            
```
```java
/**
 * @param {string} s
 * @return {string}
 */
var reverseVowels = function(s) {
    let set = new Set(['a','e','i','o','u','A','E','I','O','U']);
    let left = 0;
    let right = s.length - 1;
    let res = s.split("");
    while (left < right) {
        console.log(left, right)
        while ((!set.has(s[left]))){
            left++;
            if (left >= right) {
                return res.join("");
            }
        } 
        while ((!set.has(s[right]))){
            right--;
            if (left >= right) {
                return res.join("");
            }
        }
        console.log("fin currect: ", left, right)
        console.log(res[left])
        res[left] = s.charAt(right);
        console.log(res[left])
        res[right] = s.charAt(left);
        console.log(res)
        left++;
        right--;
    }
    return res.join("");
};

// 使用 arr.indexOf()
var reverseVowels = function(s) {
    var result;
    var temp
    var arr = ['a','e','i','o','u','A','E','I','O','U']
    var t = s.split('')
    var i = 0; j = t.length

    
    while(i<j){
        while(i<j && arr.indexOf(t[i]) == -1){
            i++;
        }
        while(i<j && arr.indexOf(t[j]) == -1){
            j--
        }
        temp = t[i];
        t[i] = t[j];
        t[j] = temp

        i++;
        j--
    }
    result = t.join('');
    return result
};
```

- question: lc1119 删去字符串中的元音（vip） link:
    - answer:
```python
# python code

```
```java

```

- question: lc557 反转字符串中的单词 link: https://leetcode.cn/problems/reverse-words-in-a-string-iii/
    - answer:
    - For python, the split() method splits a string into a list. You can specify the separator, default separator is any whitespace.
    - For python, The strip() method removes any leading (spaces at the beginning) and trailing (spaces at the end) characters (space is the default leading character to remove)
    - For python, string can not be changed directly.
```python
# python code
class Solution:
    def reverseWords(self, s: str) -> str:
        # allstr = s.split()

        # ans = allstr[0][::-1]

        # for i in range(1, len(allstr)):
        #     ans += " " + allstr[i][::-1]

        # return ans

        return " ".join([word[::-1] for word in s.split(" ")])
```
```java
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    let arr = s.split(" ");
    for (let i = 0; i < arr.length; i++) {
        arr[i] = arr[i].split("").reverse().join("")
    }
    return arr.join(" ");
};
```

- question: lc541 反转字符串 link: https://leetcode.cn/problems/reverse-string-ii/
    - answer:

```python
# python code
# 2k为步长，每次反转i：i+2k，python切片时，即使末尾超出数组，也不会报错，只会遍历到尾部。
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        t = list(s)
        for i in range(0, len(t), 2 * k):
            t[i: i + k] = reversed(t[i: i + k])
        return "".join(t)
```
```java
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
    let arr = s.split(" ");
    for (let i = 0; i < arr.length; i++) {
        arr[i] = arr[i].split("").reverse().join("")
    }
    return arr.join(" ");
};
```

- question: lc58 最后一个单词的长度 link: https://leetcode.cn/problems/length-of-last-word/
    - answer:
    
```python
# python code
# 按空格划分，然后返回最后一个元素，index为-1.
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        return len(s.split()[-1])
```
```java
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function(s) {
    let space = " ".charCodeAt();
    let res = 0
    let spaceNum = 0;
    let shouldReturn = s[s.length - 1] == " "? false : true;
    for (let i = s.length - 1; i >= 0; i--) {
        console.log(s[i])
        if (s[i] == " ") {
            if ( shouldReturn) {
                 return  res;
            }
            spaceNum ++;
            continue;
        }
        shouldReturn = true;
        res++;
    }
    return s.length - spaceNum;
};


// 使用前后指针 后指针end记录空位，前指针start记录满足要求的单词，详见得到res
// var lengthOfLastWord = function(s) {
//     let end = s.length - 1;
//     while(end >= 0 && s[end] == ' ') end--;
//     if(end < 0) return 0;
//     let start = end;
//     while(start >= 0 && s[start] != ' ') start--;
//     return end - start;
// };
```

- question: lc165 比较版本号 link: https://leetcode.cn/problems/compare-version-numbers/
    - answer:
```python
# python code
# 按"."划分后先比较相同长度的信息，再比较多出来的信息。
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        v1 = version1.split(".")
        v2 = version2.split(".")

        n1 = len(v1)
        n2 = len(v2)

        for i in range(min(n1,n2)):
            if int(v1[i]) > int(v2[i]):
                return 1
            elif int(v1[i]) < int(v2[i]):
                return -1
        
        if n1 > n2:
            for i in range(n2, n1):
                if int(v1[i]) != 0:
                    return 1
        elif n1 < n2:
            for i in range(n1, n2):
                if int(v2[i]) != 0:
                    return -1

        return 0
```
```java
/**
 * @param {string} version1
 * @param {string} version2
 * @return {number}
 */
var compareVersion = function(version1, version2) {
    let v1Arr = version1.split(".");
    let v2Arr = version2.split(".");
    let i = 0;
    while (parseInt(v1Arr[i]) == parseInt(v2Arr[i])) {
        i++;
    }
    let minLen = v1Arr.length > v2Arr.length ? v2Arr.length:v1Arr.length;
    let maxArr = v1Arr.length > v2Arr.length ? v1Arr:v2Arr;
    if (i == minLen) {
        if (v1Arr.length == v2Arr.length) return 0;
        while (i < maxArr.length) {
            if(parseInt(maxArr[i]) != 0) {
                return v1Arr.length > v2Arr.length ? 1:-1
            }
            i++
        }
        return 0
    } 
    return parseInt(v1Arr[i]) > parseInt(v2Arr[i]) ? 1 : -1;
};
```

- question: lc12 整数转罗马数字 link: https://leetcode.cn/problems/integer-to-roman/
    - answer:
```python
# python code
# 拆除特殊字符进行特殊处理。
class Solution:
    def intToRoman(self, num: int) -> str:
        mapR = ['I', 'X', 'C', 'M']
        mapS = ['V', 'L', 'D']
        map4 = ['IV', 'XL', 'CD']
        map9 = ['IX', 'XC', 'CM']
        ans = []

        for i in reversed(range(4)):
            n = num//(10**i)
            num = num - n*(10**i)
            if n < 4:
                ans.append("".join([mapR[i]]*n))
            elif n == 4:
                ans.append(map4[i])
            elif n > 4 and n < 9:
                ans.append(mapS[i] + "".join([mapR[i]]*(n-5)))
            elif n == 9:
                ans.append(map9[i])

        return "".join(ans)
```
```java
//方法一: 列举全部大单位，由大到小逐位相减
/**
 * @param {number} num
 * @return {string}
 */
var intToRoman = function(num) {
    const valueSymbols = [[1000, "M"], [900, "CM"], [500, "D"], [400, "CD"], [100, "C"], [90, "XC"], [50, "L"], [40, "XL"], [10, "X"], [9, "IX"], [5, "V"], [4, "IV"], [1, "I"]];
    const roman = [];
    for (const [value, symbol] of valueSymbols) {
        while (num >= value) {
            num -= value;
            roman.push(symbol);
        }
        if (num == 0) {
            break;
        }
    }
    return roman.join('');
};


//方法一: 列举个十百千全部元素，由大到小逐位放置
var intToRoman = function(num) {
    const thousands = ["", "M", "MM", "MMM"];
    const hundreds = ["", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"];
    const tens     = ["", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"];
    const ones     = ["", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"];

    const roman = [];
    roman.push(thousands[Math.floor(num / 1000)]);
    roman.push(hundreds[Math.floor(num % 1000 / 100)]);
    roman.push(tens[Math.floor(num % 100 / 10)]);
    roman.push(ones[num % 10]);
    return roman.join('');
};
```

- question: lc13 罗马数字转整数 link: https://leetcode.cn/problems/roman-to-integer/
    - answer:
```python
# python code
# 当前罗马字符如果大于等于下一个罗马字符，则结果加上对应数值，否则减去对应数值。
class Solution:
    def romanToInt(self, s: str) -> int:
        dic = {
            "M" : 1000,
            "D" : 500,
            "C" : 100,
            "L" : 50,
            "X" : 10,
            "V" : 5,
            "I" : 1
        }

        ans = 0

        for i in range(len(s) - 1):
            if dic[s[i]] >= dic[s[i+1]]:
                ans += dic[s[i]]
            else:
                ans -= dic[s[i]]

        ans += dic[s[-1]]

        return ans

```
```java
/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
    let keys = ["I", "V", "X", "L", "C", "D", "M"];
    let values = [1, 5, 10, 50, 100, 500, 1000];
    let res =0;
    for (let i = 0; i < s.length; i++) {
        if (keys.indexOf(s.charAt(i)) >= keys.indexOf(s.charAt(i+1))) {
            res+=values[keys.indexOf(s.charAt(i))];
        } else {
            res-=values[keys.indexOf(s.charAt(i))];
        }
    }
    return res;
};


//除此之外，还可以使用function进行对数组的存储
function getchar() {
        switch(ch) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
            default: return 0;
        }
    }
```

- question: lc38 外观数列 link: https://leetcode.cn/problems/count-and-say/
    - answer:
```python
# python code
# 计数统计，循环结束后需要再插值一次。
class Solution:
    def countAndSay(self, n: int) -> str:
        num = "1"
        if n == 1:
            return num

        for j in range(n-1):
            count = 1
            cur = num[0]
            ans = ""

            for i in range(1, len(num)):
                if num[i] == cur:
                    count += 1
                else:
                    ans += str(count) + str(cur)
                    cur = num[i]
                    count = 1

            ans += str(count) + str(cur)
            num = ans

        return num
```
```java
// 好题
/**
 * @param {number} n
 * @return {string}
 */
var countAndSay = function(n) {

    let pre = "1";
    for (let i = 1; i < n; i++) {
        let start = 0;
        let pos = 0;
        let line = ""
        while (pos < pre.length) {
            while (pos < pre.length && pre[pos] == pre[start]) {
                pos++;
            }
            line = line + (pos - start) + pre[start]
            start = pos;
        }
        pre = line;
    }
    return pre;
};
```

- question: lc6 Z字形变换 link: https://leetcode.cn/problems/zigzag-conversion/
    - answer:
```python
# python code
# 初始化n行string，每次i到达numRows-1与0时，改变方向.
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows <= 1:
            return s
            
        ans = ["" for i in range(numRows)]
        # 初始化n个字符串

        i = 0
        flag = -1
        # 移动方向
        for c in s:
            ans[i] += c
            if i == numRows-1 or i == 0:  
                flag = -flag  
                # 改变方向
            i += flag

        return "".join(ans)
```
```java
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function(s, numRows) {
    let arr = new Array(numRows).fill("");
    let flag = 1;
    let index = 0;
    if (numRows == 1) {
        return s;
    }
    for (let i = 0; i < s.length; i++) {
        arr[index]+=s.charAt(i);
        index += flag;
        if (index == numRows - 1 || index == 0) {
            flag = -flag;
        }
    }
    return arr.join('')
    
};
```

### 数学相关

- question: lc7 整数反转 link: https://leetcode.cn/problems/reverse-integer/
    - answer:
```python
# mod 10 and reverse the numbers
# or convert to string and reversed
class Solution:
    def reverse(self, x: int) -> int:
        if x < -2**31 or x > 2**31 - 1:
            return 0

        flag = True if x > 0 else False

        x = abs(x)

        ans = 0

        while x > 0:
            ans = ans*10 + x%10
            x //= 10

        if ans < -2**31 or ans > 2**31 - 1:
            return 0

        return ans if flag else -ans
```
```java
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
    let res = 0;
    let absx = x >= 0 ? x : -x;
    while (absx != 0) {
        let temp = absx%10;
        absx = Math.floor(absx / 10)
        res = res * 10 + temp; 
        if(res > Math.pow(2, 31) - 1 || res < Math.pow(-2, 31)) return 0;
    }
    return x >= 0 ? res : -res;
};
```

- question: lc9 回文数 link: https://leetcode.cn/problems/palindrome-number/
    - answer:
```python
# 双指针头尾同时检测并向内侧移动（允许使用string的时候）
# 不允许使用string时，需要用数学方法得到反转后的数字，检查是否相等。
class Solution:
    def isPalindrome(self, x: int) -> bool:
        # s = str(x)
        # right, left = len(s)-1, 0

        # while left < right:
        #     if s[left] != s[right]:
        #         return False
            
        #     left += 1
        #     right -= 1
        
        # return True

        if x < 0:
            return False

        n = x

        ans = 0

        while n > 0:
            ans = ans*10 + n%10
            n = n//10
        
        return True if ans == x else False
```
```java
/**
 * @param {number} x
 * @return {boolean}
 */
var isPalindrome = function(x) {
    if (x < 0) return false
    let x2 = x.toString();
    let left = 0;
    let right = x2.length - 1
    while (left < right) {
        if (x2.charAt(right--) != x2.charAt(left++)) return false;
    }
    return true
};
```

- question: lc989 数组形式的整数加法 link: https://leetcode.cn/problems/add-to-array-form-of-integer/
    - answer:

```
逐位相加解题思路

while ( A 没完 || B 没完)
    A 的当前位
    B 的当前位
    和 = A 的当前位 + B 的当前位 + 进位carry
    当前位 = 和 % 10;
    进位 = 和 / 10;
```

```python
# 不转换为字符串，则需要将k转为list形式，相加有进位就进位。
class Solution:
    def addToArrayForm(self, num: List[int], k: int) -> List[int]:
        n = len(num)

        lk = []
        num[:] = num[::-1]

        while k > 0:
            lk.append(k%10)
            k //= 10

        if len(lk) > n:
            num.extend([0]*(len(lk)-n))
            n = len(lk)
        else:
            lk.extend([0]*(n-len(lk)))

        ans = [0] * (n+1)
        
        for i in range(n):
            ans[i] += lk[i] + num[i]
            if ans[i] >= 10:
                ans[i] %= 10
                ans[i+1] += 1

        if ans[-1] == 0:
            ans.pop()

        return ans[::-1]

# 转换为字符串后，连接再转为int然后相加最后拆成list返回。
        # n = int("".join([str(c) for c in num])) + k

        # ans = []

        # while n > 0:
        #     ans.append(n%10)
        #     n //= 10
        
        # return ans[::-1]
```
```java
/**
 * @param {number[]} num
 * @param {number} k
 * @return {number[]}
 */
var addToArrayForm = function(num, k) {
    let karr = [];
    let res = []
    while (k != 0) {
        let temp = k % 10;
        karr.push(temp);
        k = Math.floor(k / 10);
    }
    karr.reverse();
    let i = num.length - 1;
    let j = karr.length - 1;
    let carry = 0;
    while (i >= 0 || j >= 0) {
        let x = i >= 0 ? num[i--] : 0; 
        let y = j >= 0 ? karr[j--] : 0; 
        let sum = carry + x + y
        res.push(sum%10);
        carry = Math.floor(sum/10);
    }
    if (carry == 1) {
        res.push(1);
    }
    return res.reverse();

};
```

- question: lc66 加1 link: https://leetcode.cn/problems/plus-one/
    - answer:
```python
# 翻转后先hardcode给第一项加1，之后遍历0~n-2项，大于等于10则进位。跳出循环后，如果最后一位大于等于10则在末尾append（1）。
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:

        digits[:] = digits[::-1]

        digits[0] += 1

        for i in range(len(digits) - 1):
            if digits[i] >= 10:
                digits[i] %= 10
                digits[i+1] += 1
        
        if digits[-1] >= 10:
            digits[-1] %= 10
            digits.append(1)
        
        return digits[::-1]
```
```java
/**
 * @param {number[]} digits
 * @return {number[]}
 */
var plusOne = function(digits) {
    let i = digits.length - 1;
    let carry = 1;
    while (i >= 0) {
        let sum = carry + digits[i];
        digits[i] = sum % 10;
        carry = Math.floor(sum / 10);
        i--;
    }
    if (carry != 0) {
        digits.unshift(1);
    }
    return digits
};
```

- question: lc415 字符串相加 link: https://leetcode.cn/problems/add-strings/
    - answer:
```python
# 无法转为int时，用ord（str） - ord（‘0’）
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:
        i = len(num1) - 1
        j = len(num2) - 1
        carry = 0

        ans = ""

        while i >= 0 or j >= 0 or carry != 0:
            x = ord(num1[i]) - ord('0') if i >= 0 else 0
            y = ord(num2[j]) - ord('0') if j >= 0 else 0

            ans += chr((x + y + carry)%10 + ord('0'))
            carry = (x + y + carry)//10

            i -= 1
            j -= 1

        return ans[::-1] 
```
```java

```

- question: lc67 剑指002 二进制求和 link: https://leetcode.cn/problems/add-binary/
    - answer:
```python
# 类似上一题,把进位改成2就行,当前位置为result%2, 进位为result//2.
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        i = len(a) - 1
        j = len(b) - 1

        carry = 0

        ans = ""

        while i >= 0 or j >= 0 or carry != 0:
            x = ord(a[i]) - ord('0') if i >= 0 else 0
            y = ord(b[j]) - ord('0') if j >= 0 else 0

            ans += chr((x + y + carry)%2 + ord('0'))
            carry = (x + y + carry)//2

            i -= 1
            j -= 1

        return ans[::-1] 
```
```java

```

- question: lc2 两数相加 link: https://leetcode.cn/problems/add-two-numbers/
    - answer:
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        ans = head = ListNode(0)
        carry = 0
        while l1 or l2 or carry:
            x = l1.val if l1 else 0
            y = l2.val if l2 else 0
            result = x + y + carry
            head.next = ListNode(result%10)
            head = head.next
            carry = result//10
            l1 = l1.next if l1 else l1
            l2 = l2.next if l2 else l2
        
        return ans.next 
```
```java

```

- question: lc43 字符串相乘 link: https://leetcode.cn/problems/multiply-strings/
    - answer:
```python
# 利用竖式乘法规则, 小数每一位与大数相乘再求和.
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        if num1 == "0" or num2 == "0":
            return "0"
        
        if len(num1) < len(num2):
            num1, num2 = num2, num1
        
        n1 = len(num1)
        n2 = len(num2)

        result = 0

        for i in range(n2):
            temp = 0
            for j in range(n1):
                temp = temp + (ord(num2[n2-1-i]) - ord("0")) * (ord(num1[n1-1-j]) - ord("0"))*(10**j)

            result += temp*(10**i)

        ans = ""

        while result > 0:
            ans += chr(result%10 + ord("0"))
            result //= 10

        return ans[::-1]
```
```java

```

- question: lc204 计数质数 link: https://leetcode.cn/problems/count-primes/
    - answer:
```python
# 筛选法,先初始化一个长度为n,且都为1的数组,当当前数组值为1时,将所有i的倍数的值都赋值为0,最后剩下的1就都是质数.
class Solution:
    def countPrimes(self, n: int) -> int:
        if n < 2:
            return 0

        isPrime = [1] * n
        isPrime[0] = isPrime[1] = 0 
        
        for i in range(2, int(n ** 0.5) + 1):
            if isPrime[i]:
                for j in range(i+i, n, i):
                    isPrime[j] = 0

        return sum(isPrime)
```
```java

```

- question: lc233 剑指43 数字1的个数 link: https://leetcode.cn/problems/number-of-digit-one/
    - answer:
```python

```
```java

```

- question: lc1232 缀点成线 link: https://leetcode.cn/problems/check-if-it-is-a-straight-line/
    - answer:
```python
# 通过计算斜率是否相同来得到，但需要注意不要用除法，可以换成乘法:
# (yi-1 - yi)*(xi - xi+1) ?= (yi - yi+1) * (xi-1 - xi)
class Solution:
    def checkStraightLine(self, coordinates: List[List[int]]) -> bool:
        if len(coordinates) < 2:
            return False

        for i in range(1,len(coordinates)-1):
            if (coordinates[i-1][1] - coordinates[i][1]) * (coordinates[i][0] - coordinates[i+1][0]) != \
            (coordinates[i][1] - coordinates[i+1][1]) * (coordinates[i-1][0] - coordinates[i][0]):
                return False
        
        return True
```
```java

```

### 位运算
 
- question: lc191 位1的个数 link: https://leetcode.cn/problems/number-of-1-bits/
    - answer:
```python

```
```java

```

- question: lc461 汉明距离 link: https://leetcode.cn/problems/hamming-distance/
    - answer:
```python

```
```java

```

- question: lc477 汉明距离总和 link: https://leetcode.cn/problems/total-hamming-distance/
    - answer:
```python

```
```java

```

- question: lc231 2的幂 link: https://leetcode.cn/problems/power-of-two/
    - answer:
```python

```
```java

```

- question: lc371 两整数之和 link: https://leetcode.cn/problems/sum-of-two-integers/
    - answer:
```python

```
```java

```

- question: lc29 两数相除 link: https://leetcode.cn/problems/divide-two-integers/
    - answer:
```python

```
```java

```

- question: lc136 只出现一次的数字 link: https://leetcode.cn/problems/single-number/
    - answer:
```python

```
```java

```

- question: lc137 只出现一次的数字II link: https://leetcode.cn/problems/single-number-ii/
    - answer:
```python

```
```java

```

- question: lc1318 或运算的最小翻转次数 link: https://leetcode.cn/problems/minimum-flips-to-make-a-or-b-equal-to-c/
    - answer:
```python

```
```java

```

- question: lc201 数字范围按位与 link: https://leetcode.cn/problems/bitwise-and-of-numbers-range/
    - answer:
```python

```
```java

```

- question: lc476 数字的补数 link: https://leetcode.cn/problems/number-complement/
    - answer:
```python

```
```java

```

- question: lc405 数字转换为十六进制数 link: https://leetcode.cn/problems/convert-a-number-to-hexadecimal/
    - answer:
```python

```
```java

```

- question: lc190 颠倒二进制位 link: https://leetcode.cn/problems/reverse-bits/
    - answer:
```python

```
```java

```

### 排序
阿里面试题 - 快速查找第二大数

- question: lc912 ：排序数组 link:
    - answer:
```python

```
```java

```

- question: lc628 ：三个数的最大乘积 link:
    - answer:
```python

```
```java

```

- question: lc88 ：合并两个有序数组 link:
    - answer:
```python

```
```java

```

- question: 剑指51 ：数组中的逆序对 link:
    - answer:
```python

```
```java

```

- question: lc315 ：计算右侧小于当前元素的个数 link:
    - answer:
```python

```
```java

```

- question: lc327 ：区间和的个数 link:
    - answer:
```python

```
```java

```

- question: lc493 ：翻转对 link:
    - answer:
```python

```
```java

```

- question: lc50剑指16 ：Pow(x, n) link:
    - answer:
```python

```
```java

```

- question: lc75 ：颜色分类 link:
    - answer:
```python

```
```java

```

- question: lc179剑指45 ：最大数 link:
    - answer:
```python

```
```java

```

- question: lc56剑指74 ：合并区间 link:
    - answer:
```python

```
```java

```

- question: lc57 ：插入区间 link:
    - answer:
```python

```
```java

```

- question: lc905 ：按奇偶排序数组 link:
    - answer:
```python

```
```java

```

- question: lc922 ：按奇偶排序数组 II link:
    - answer:
```python

```
```java

```

- question: lc1365 ：有多少小于当前数字的数字 link:
    - answer:
```python

```
```java

```

- question: lc164 ：最大间距 link:
    - answer:
```python

```
```java

```

### 查找

- question: lc704 ：二分查找 link:
    - answer:
```python

```
```java

```

- question: lc34 ：排序数组中找元素的第一个和最后一个位置 link:
    - answer:
```python

```
```java

```

- question: lc35 ：搜索插入位置 link:
    - answer:
```python

```
```java

```

- question: lc278 ：第一个错误的版本 link:
    - answer:
```python

```
```java

```

- question: lc33 ：搜索旋转排序数组 link:
    - answer:
```python

```
```java

```

- question: lc153 ：寻找旋转排序数组中的最小值 link:
    - answer:
```python

```
```java

```

- question: lc154 ：寻找旋转排序数组中的最小值 II link:
    - answer:
```python

```
```java

```

- question: lc852 ：山脉数组的峰顶索引 link:
    - answer:
```python

```
```java

```

- question: lc1095 ：山脉数组中查找目标值 link:
    - answer:
```python

```
```java

```

- question: lc162 ：寻找峰值 link:
    - answer:
```python

```
```java

```

- question: lc74 ：搜索二维矩阵 link:
    - answer:
```python

```
```java

```

- question: lc240 ：搜索二维矩阵 II【top100】 link:
    - answer:
```python

```
```java

```

- question: lc69 ：x 的平方根 link:
    - answer:
```python

```
```java

```

- question: lc1539 ：第 k 个缺失的正整数 link:
    - answer:
```python

```
```java

```

- question: lc771 ：宝石与石头 link:
    - answer:
```python

```
```java

```

- question: lc888 ：公平的糖果棒交换 link:
    - answer:
```python

```
```java

```

- question: lc128 ：最长连续序列 link:
    - answer:
```python

```
```java

```

- question: lc136 ：只出现一次的数字 link:
    - answer:
```python

```
```java

```

- question: lc389 ：找不同 link:
    - answer:
```python

```
```java

```

- question: lc554 ：砖墙 link:
    - answer:
```python

```
```java

```

- question: lc205 ：同构字符串 link:
    - answer:
```python

```
```java

```

- question: lc290 ：单词规律 link:
    - answer:
```python

```
```java

```

- question: lc242 ：有效的字母异位词 link:
    - answer:
```python

```
```java

```

- question: lc49 ：字母异位词分组 link:
    - answer:
```python

```
```java

```

- question: lc560 ：和为K的子数组 link:
    - answer:
```python

```
```java

```

- question: lc41 ：缺失的第一个正数 link:
    - answer:
```python

```
```java

```

- question: lc1122 ：数组的相对排序 link:
    - answer:
```python

```
```java

```


### 栈与队列

lc 20 ：有效的括号【top100】
lc 71 &amp; 剑指 017 ：简化路径
lc 394 ：字符串解码【top100】
lc 224 号算法题：基本计算器
lc 227 号算法题：基本计算器二
lc 946 &amp; 剑指 31 ：验证栈序列
lc 739 &amp; 剑指 038 ：每日温度【top100】
lc 42 ：接雨水【top100】
lc 84 &amp; 剑指 039 ：柱状图中最大的矩形【top100】
lc 85 &amp; 剑指 040 ：最大矩形【top100】
lc 321 号算法题：拼接最大数
lc 456 号算法题：132 模式
lc 151 &amp; 剑指 58-1：翻转字符串里的单词"
堆和优先队列回顾
lc 1046 号算法题：最后一块石头的重量
lc 215 &amp; 剑指 076 ：数组中的第 K 个最大元素【top100】
lc 347 &amp; 剑指 060：前 K 个高频元素【top100】
lc 973 号算法题：最接近原点的 K 个点
lc 703 &amp; 剑指 059：数据流中的第 K 大元素
lc 295 &amp; 剑指 41：数据流的中位数
lc 4 ：寻找两个正序数组的中位数【top100】
lc 239 &amp; 剑指 59-1 ：滑动窗口最大值【top100】

- question:  link:
    - answer:
```python

```
```java

```

### 滑动窗口

lc 643 ：子数组最大平均数 I
lc 209 &amp; 剑指 008 ：长度最小的子数组
lc 3 &amp; 剑指 016 ：无重复字符的最长子串【top100】
lc 76 ：最小覆盖子串【top100】
lc 485 ：最大连续 1 的个数
lc 487 ：最大连续1的个数 II
lc 1004 ：最大连续 1 的个数 III
lc 1151 ：最少交换次数来组合所有的 1
lc 30 ：串联所有单词的子串
lc 567 &amp; 剑指 014 ：字符串的排列
lc 763 ：划分字母区间
lc 845 ：数组中的最长山脉

- question:  link:
    - answer:
```python

```
```java

```

### 综合应用I

lc 1 ：两数之和【top100】
lc 167 &amp; 剑指 006 ：两数之和：输入有序数组
lc 170 ：两数之和：数据结构设计
lc 653 ：两数之和：输入 BST
lc 15 &amp; 剑指 007 ：三数之和【top100】
lc 18 ：四数之和
lc 349 : 两个数组的交集
lc 350 ：两个数组的交集 II
lc 169  &amp; 剑指 39 ：多数元素【top100】
lc 229 ：多数元素变形题
lc 844 ：比较含退格的字符串
lc 318 &amp; 剑指 005 ：最大单词长度乘积

- question:  link:
    - answer:
```python

```
```java

```

### 链表

lc 203 ：移除链表元素
lc 237 删除链表中的节点
lc 83 ：删除排序链表中的重复元素
lc 82 ：删除排序链表中的重复元素 II
lc 876 ：链表的中间结点
lc 19 &amp; 剑指 021 ：删除链表的倒数第 N 个结点【top100】
lc 141 ：环形链表【top100】
lc 142 &amp; 剑指 022 ：环形链表 II【top100】
lc 206 &amp; 剑指 024 ：反转链表【top100】
lc 92 ：反转链表 II
lc 61 ：旋转链表
lc 328 ：奇偶链表
lc 725 ：分隔链表
lc 24 ：两两交换链表中的节点
lc 25 ：K 个一组翻转链表
lc 234 &amp; 剑指 027 ：回文链表【top100】
lc 138 &amp; 剑指 35 ：复制带随机指针的链表
lc 138 ：复制带随机指针的链表
lc 86 ：分隔链表
lc 160 &amp; 剑指 023 ：相交链表【top100】
lc 2 ：两数相加【top100】
lc 445 &amp; 剑指 025 ：两数相加 II
lc 21 &amp; 剑指 25 ：合并两个有序链表【top100】
lc 23 &amp; 剑指 078 ：合并K个升序链表【top100】
lc 147 ：对链表进行插入排序"
lc 148 &amp; 剑指 077 ：排序链表【top100】

- question:  link:
    - answer:
```python

```
```java

```

### 二叉树

lc 144 ：二叉树的前序遍历
lc 94 ：二叉树的中序遍历【top100】"
lc 145 ：二叉树的后序遍历

#### BFS与DFS
lc 102 &amp; 剑指 32-2 ： 二叉树的层序遍历【top100】
lc 107 ：二叉树的层序遍历 II
lc 104 &amp; 剑指 55-1 ：二叉树的最大深度【top100】
lc 543 ：二叉树的直径【top100】
lc 110 &amp; 剑指 55-2 ：平衡二叉树
lc 111 ：二叉树的最小深度
lc 404 ：左叶子之和
lc 103 &amp; 剑指 32-3 ：二叉树的锯齿形层序遍历
lc 515 &amp; 剑指 044 ：在每个树行中找最大值
lc 199 &amp; 剑指 046 ：二叉树的右视图
lc 100 ：相同的树
lc 101 &amp; 剑指 28 ：对称二叉树 【top100】
lc 662 ：二叉树最大宽度
lc 222 ：完全二叉树的节点个数
lc 114 ：二叉树展开为链表【top100】
lc 236 &amp; 剑指 68-2 ：二叉树的最近公共祖先【top100】

#### 回溯思想
lc 112 ：路径总和
lc 113 &amp; 剑指 34 ：路径总和 II
lc 257 ：二叉树的所有路径
lc 437 ：路径总和 III【top100】
lc 124 ：二叉树中的最大路径和【top100】
lc 226 &amp; 剑指 226 ：翻转二叉树【top100】
lc 617 ：合并二叉树【top100】
lc 105 &amp; 剑指 7 ：从前序与中序遍历序列构造二叉树【top100】
lc 106 ：从中序与后序遍历序列构造二叉树
lc 116 ：填充每个节点的下一个右侧节点指针

#### 二叉搜索树
lc 701 ：二叉搜索树中的插入操作
lc 108 ：将有序数组转换为二叉搜索树
lc 235 &amp; 剑指 68-1 ：二叉搜索树的最近公共祖先
lc 98 ：验证二叉搜索树【top100】
lc 501 ：二叉搜索树中的众数
lc 99 ：恢复二叉搜索树
lc 538 &amp; 剑指 054 ：把二叉搜索树转换为累加树【top100】
lc 589 ：N 叉树的前序遍历
lc 590 ：N 叉树的后序遍历
lc 429 ：N 叉树的层序遍历
lc 690 ：员工的重要性

#### 图的 DFS 和 BFS
lc 733 ：图像渲染
lc 463 ：岛屿的周长
lc 200 ：岛屿数量【top100】
lc 695 ：岛屿的最大面积
lc 130 ：被围绕的区域
lc 1034 ：边框着色
lc 529 ：扫雷游戏
lc 994 ：腐烂的橘子

- question:  link:
    - answer:
```python

```
```java

```

### 数据结构设计

lc 155 &amp; 剑指 30 ：最小栈 【top100】
lc 225 ：用队列实现栈
lc 622 ：设计循环队列
lc 380 &amp; 剑指 030 ：O(1) 时间插入、删除和获取随机元素
lc 381 ：O(1) 时间插入、删除和获取随机元素 - 允许重复
缓存机制
FIFO 缓存机制
lc 146 &amp; 剑指 031 ：LRU 缓存机制
lc 460 ：LFU 缓存
并查集 20-11
并查集优化 20-12
lc 547 &amp; 剑指 116 ：省份数量
lc 200 ：岛屿数量【top100】
lc 721 ：账户合并

- question:  link:
    - answer:
```python

```
```java

```

### 综合应用II

lc 217 ：存在重复元素
lc 219 ：存在重复元素 II
lc 220 &amp; 剑指 057 ：存在重复元素 III
lc 258 ：各位相加
lc 202 ：快乐数
lc 263 ：丑数

#### 字典树 - 前缀树 - Tire
lc 208 &amp; 剑指 062 ：实现 Trie (前缀树)【top100】
lc 642 ：搜索自动补全系统
lc 421 &amp; 剑指 067 ：数组中两个数的最大异或值
lc 440 ：字典序的第K小数字

- question:  link:
    - answer:
```python

```
```java

```

### 回溯算法

lc 112 和 113 &amp; 剑指 34 ：路径总和
lc 46 和 47 &amp; 剑指 083 和 084 ：全排列【top100】
lc 77 &amp; 剑指 080 ：组合
lc 39 和 40 &amp; 剑指 081 和 082  ：组合总和【top100】
lc 78 和 90 &amp; 剑指 079：子集【top100】
lc 17 ：电话号码的字母组合【top100】
lc 93 &amp; 剑指 087 ：复原 IP 地址
lc 22 &amp; 剑指 085 ：括号生成【top100】
lc 51 ：N 皇后
lc 37 ：数独问题
lc 401 ：二进制手表
lc 131 &amp; 剑指 086 ：分割回文串
lc 842 ：将数组拆分成斐波那契序列
lc 79 &amp; 剑指 12 ： 单词搜索 【top100】
lc 679 ：24 点游戏

- question:  link:
    - answer:
```python

```
```java

```

### 贪心算法

lc 455 ：分发饼干 - 贪心思想
lc 322 &amp; 剑指 103 ：零钱兑换 - 贪心 + 回溯【top100】
贪心算法特点总结 25-4
lc 45 ：跳跃游戏 Ⅱ
lc 55 ：跳跃游戏【top100】
lc 1578 ：避免重复字母的最小删除成本
lc 402 ：移掉K位数字
lc 409 ：最长回文串
lc 680 &amp; 剑指 019 ：验证回文字符串 Ⅱ
lc 316 ：去除重复字母
lc 1047 ：删除字符串中的所有相邻重复项
lc 1209 ：删除字符串中的所有相邻重复项 II
lc 976 ：三角形的最大周长
lc 674 ：最长连续递增序列
lc 738 ：单调递增的数字
lc 134 ： 加油站
lc 767 ：重构字符串
lc 621 ： 任务调度器【top100】
lc 670 ：最大交换
lc 861 ：翻转矩阵后的得分
lc 1029 ：两地调度
lc 330 ：按要求补齐数组

- question:  link:
    - answer:
```python

```
```java

```

### 动态规划

lc 509 &amp; 剑指 10-1 ：斐波那契数列问题 - 动态规划入门
lc 322 &amp; 剑指 103 ：零钱兑换
动态规划总结 27-4
lc 64 &amp; 剑指 099 ：最小路径和【top100】
lc 53 &amp; 剑指 42 ：最大子数组之和【top100】
lc 53 &amp; 剑指 42 ：最大子数组之和【top100】
lc 647、5、131 &amp; 剑指 086 、020  ：回文子串【top100】
lc 516 ：最长回文子序列
lc 300 ：最长上升子序列【top100】
lc 1143 &amp; 剑指 095 ：最长公共子序列
lc 72 ：编辑距离【top100】
lc 44 ：通配符匹配
lc 486 ：预测赢家
lc 70 &amp; 剑指 10 - 2： 爬楼梯【top100】
lc 746 &amp; 剑指 088 ：使用最小花费爬楼梯
lc 198 &amp; 剑指 089 ：打家劫舍【top100】
lc 213 &amp; 剑指 090 ：打家劫舍 II
lc 337 ：打家劫舍 III【top100】
0 - 1 背包问题 28-7
#### 完全背包问题 28-8
lc 322 &amp; 剑指 103 ：零钱兑换
lc 518 ：零钱兑换 II
lc 377 &amp; 剑指 104 ：组合总和 Ⅳ
lc 494 &amp; 剑指 102 ：目标和【top100】
lc 416 &amp; 剑指 101 ：分割等和子集【top100】
lc 279 ：完全平方数【top100】
lc 474 ：一和零
lc 139 ：单词拆分【top100】
lc 62 &amp; 剑指 098 ：不同路径【top100】
lc 63 ：不同路径 II
lc 120 &amp; 剑指 100 ：三角形最小路径和
lc 97 &amp; 剑指 096 ：交错字符串
lc 221 ： 最大正方形【top100】
#### 系列算法题：买卖股票的最佳时机
lc 121 &amp; 剑指 63 ：买卖股票的最佳时机【top100】
lc 122 ：买卖股票的最佳时机 II
lc 123 ：买卖股票的最佳时机 III
lc 188 ：买卖股票的最佳时机 IV
lc 309 ：最佳买卖股票时机含冷冻期【top100】
lc 714 ：买卖股票的最佳时机含手续费
lc 139. 单词拆分【top100】"
lc 140. 单词拆分 II
lc 91. 解码方法
lc 32. 最长有效括号【top100】
lc 10 &amp; 剑指 19. 正则表达式匹配【top100】
lc 718. 最长重复子数组
lc 354. 俄罗斯套娃信封问题
lc 152. 乘积最大子数组【top100】
lc 376. 摆动序列

- question:  link:
    - answer:
```python

```
```java

```

###

- question:  link:
    - answer:
```python

```
```java

```
