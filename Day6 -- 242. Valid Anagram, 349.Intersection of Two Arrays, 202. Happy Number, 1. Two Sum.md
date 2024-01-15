## 242. Valid Anagram

**Link:** [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/description/)

**Thoughts:** 

 - Hashtable to check the existance of element in an array or a string
 - can use array [ ], set(), or hashmap {} as the hashtable based on different needs

**Solution:**

```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        countS = {}
        countT = {}
        for n in s:
            countS[n] = countS.get(n,0) + 1

        for n in t:
            countT[n] = countT.get(n,0) + 1
        
        return countS == countT
```    

**Time Complexity:**  O(s+t)

**Spcae Complexity:**  O(s+t)

Another Solution: (use Array as Hashtable)
```
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = [0] * 26
        for i in s:
            #并不需要记住字符a的ASCII，只要求出一个相对数值就可以了
            record[ord(i) - ord("a")] += 1
        for i in t:
            record[ord(i) - ord("a")] -= 1
        for i in range(26):
            if record[i] != 0:
                #record数组如果有的元素不为零0，说明字符串s和t 一定是谁多了字符或者谁少了字符。
                return False
        return True
```


## 349. Intersection of Two Arrays

**Link:** [349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/description/)

**Thoughts:** 

 - use set() to remove dup 

**Solution:**
```
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        
        set1 = set(nums1)
        set2 = set(nums2)
        res = []
        
        for i in set1:
            if i in set2:
                res.append(i)
        return res
```    
**Time Complexity:**  O(m + n) where `n` and `m` are arrays' lengths. `O(n)` is used to convert `nums1` into set, `O(m)` is used to convert `nums2`, and `contains/in` operations are `O(1)` in the average case.

**Spcae Complexity:**  O(m + n) in the worst case when all elements in the arrays are different.



## 202. Happy Number

**Link:** [202. Happy Number](https://leetcode.com/problems/happy-number/description/)

**Thoughts:** 

 - **loops endlessly in a cycle**，that means duering the sum process, the value of sum will be repeated.

 - 当我们遇到了要**快速判断一个元素是否出现集合里**的时候，就要考虑哈希法了。

 - use hashtable, to check whether the value of sum is repeated, if yes, then return false, otherwise, return true.
  
  
**Solutions:** 
```
class Solution:
    def isHappy(self, n: int) -> bool:
        def calculate_happy(num):
            sum_ = 0
            
            # 从个位开始依次取，平方求和
            while num:
                sum_ += (num % 10) ** 2
                num = num // 10
            return sum_

        # 记录中间结果
        record = set()

        while True:
            n = calculate_happy(n)
            if n == 1:
                return True
            
            # 如果中间结果重复出现，说明陷入死循环了，该数不是快乐数
            if n in record:
                return False
            else:
                record.add(n)
```
**Time Complexity:**  O(logN)

**Spcae Complexity:**  O(logN)



## 1. Two Sum

**Link:** [1. Two Sum](https://leetcode.com/problems/two-sum/description/)

**Thoughts:** 

 - Why we use hashtable? **need to store the element and check whether the element's exist** （为什么会想到用哈希表）
 - Why use hashmap? not array or set? **we need to store both value and index for the element** (哈希表为什么用map)
 - In hashmap, what we store? **the key in hashmap is the element value in the array, the value in hashmap is the element index** (本题map是用来存什么的)
 
**Solution:**
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}

        for index, num in enumerate(nums):
            remain = target - num
            if remain in hashmap.keys(): return [index,hashmap[remain]]
            hashmap[num] = index
```

**Time Complexity:**  O(n)

**Spcae Complexity:**  O(n)
