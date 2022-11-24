# LeecodeNoteFor2023
drive link: https://drive.google.com/drive/folders/1e4Lboc4y1uaDwOWHhmAIXtQHzPPXAJVB


task link: https://ke.qq.com/course/package/31104?flowToken=1039500


Learning Time: 2:00-6:00 7:30-10:30 7h


## 数组字符串

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

- question: lc54 剑指29 螺旋矩阵 link https://leetcode.cn/problems/spiral-matrix
    - answer:
```python
# python code

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

- question: lc59 螺旋矩阵二 link:
    - answer:
```python
# python code

```
```java

```

- question: lc498 对角线遍历 link:
    - answer:
```python
# python code

```
```java

```

- question:lc118 杨辉三角 link:
    - answer:
```python
# python code

```
```java

```

- question: lc119 杨辉三角二 link:
    - answer:
```python
# python code

```
```java

```

- question: lc28 实现 strStr() link:
    - answer:
```python
# python code

```
```java

```

- question: lc344 反转字符串 link:
    - answer:
```python
# python code

```
```java

```

- question: lc345 反转字符串中的元音字母 link:
    - answer:
```python
# python code

```
```java

```

- question: lc1119 删去字符串中的元音 link:
    - answer:
```python
# python code

```
```java

```

- question: lc541 反转字符串中的单词 link:
    - answer:
```python
# python code

```
```java

```

- question: lc557 反转字符串 link:
    - answer:

```python
# python code

```

```java
//巧用set

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

- question: lc58 最后一个单词的长度 link:
    - answer:
```python
# python code

```
```java

```

- question: lc165 比较版本号 link:
    - answer:
```python
# python code

```
```java

```

- question: lc12 整数转罗马数字 link: 
    - answer:
```python
# python code

```
```java

```

- question: lc13 罗马数字转整数 link:
    - answer:
```python
# python code

```
```java

```

- question: lc38 外观数列 link: 
    - answer:
```python
# python code

```
```java

```

- question: lc6 Z字形变换 link:
    - answer:
```python
# python code

```
```java

```

- question:  link:
    - answer:

```python
# python code

```

```java

```

