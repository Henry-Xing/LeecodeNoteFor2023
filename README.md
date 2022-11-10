# LeecodeNoteFor2023
drive link: https://drive.google.com/drive/folders/1e4Lboc4y1uaDwOWHhmAIXtQHzPPXAJVB


task link: https://ke.qq.com/course/package/31104?flowToken=1039500


Learning Time: 2:00-6:00 7:30-10:30 7h


### date: 2022/11/11

- question: input/output基础 link: https://www.nowcoder.com/test/27976983/summary#question

- question: HJ12 字符串反转 link: https://www.nowcoder.com/practice/e45e078701ab4e4cb49393ae30f1bb04?tpId=37&tqId=21235&ru=/exam/oj
- answer:
  - how?

- question: HJ68 成绩排序 link: https://www.nowcoder.com/practice/8e400fd9905747e4acc2aeed7240978b?tpId=37&tqId=21291&ru=/exam/oj
- answer:
  - how?

- question: LC442 数组中重复的数据 link: https://leetcode.cn/problems/find-all-duplicates-in-an-array/
- answer:
  - how?

- question: LC448 找到所有数组中消失的数字 link: https://leetcode.cn/problems/find-all-numbers-disappeared-in-an-array/
- answer:
  - how?

- question: LC1002 查找共用字符 link: https://leetcode.cn/problems/find-common-characters/
- answer:
  - how?

- question: LC1370 上升下降字符串 link: https://leetcode.cn/problems/increasing-decreasing-string/
- answer:
  - how?

### date: 2022/11/12
```python
def checkInclusion(s1: str, s2: str) -> bool:
    n1 = len(s1)
    n2 = len(s2)

    temp = list(s1).copy()

    for i in range(n2):
        if i <= n2 - n1:
            for j in range(n1):
                print(temp, i, i+j, s2[i+j])
                if s2[i+j] in temp:
                    temp.remove(s2[i+j])
                else:
                    temp = list(s1).copy()
                    break
                if not temp:
                    return True
        else:
            return False

    return False if temp else True
  ```
