## 977. Squares of a Sorted Array

**Link:** [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

**Thoughts:** 

 - Two pointers:
 - Treat the array as two sorted arrays. After squaring, the largest element will be selected from first element and last element
![b6c29e9b5a2ce2d398ce836eed58d3b](https://github.com/nemo3536/Leetcode-Tracking/assets/155724737/6e22505c-030f-4c11-b5a8-e07983860bcb)

```
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;
        vector<int>sqr_nums(nums.size(),0);
        int k = right;
        while(left <= right){
            if (nums[left] * nums[left] >= nums[right] * nums[right]){
                sqr_nums[k--] = nums[left] * nums[left];
                left++;
            }
            else{
                sqr_nums[k--] = nums[right] * nums[right];
                right--;
            }
        }
        return sqr_nums;
    }
};
```    

**Time Complexity:**  O(N)

**Spcae Complexity:**  O(1)


## 209. Minimum Size Subarray Sum

**Link:** [209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

**Thoughts:** 

 - Sliding window:
 - Add current element val to sum until the `sum >= target` (move right side of window)
 - When `sum >= target`, remove left most elment val from sum (move left side of window), and record the size of subarray, take the min size. 

**Templete for sliding window:**
```
    left = 0, right = 0

    while right < len(s): 
        // 增大窗口
        window.add(s[right])
        right += 1
    
        while (window needs shrink) 
            // 缩小窗口
            window.remove(s[left])
            left += 1
```    
**Time Complexity:**  O(N) Each element can be visited atmost twice, once by the right pointer and (atmost)once by the left pointer.

**Spcae Complexity:**  O(1)


## 59. Spiral Matrix II

**Link:** [59. Spiral Matrix II](https://leetcode.com/problems/spiral-matrix-ii/description/)

**Thoughts:** 

 - 2D Matrix Iteration:
  
  ![image](https://user-images.githubusercontent.com/69004164/206582312-27b58369-78a7-40ea-aa12-64539d9a0a27.png)
  
**Solutions:** 
```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        res = [[0 for __ in range(n)] for __ in range(n)]
        colStart, rowStart = 0, 0
        colEnd, rowEnd = n - 1, n - 1

        number = 1

        while colStart <= colEnd and rowStart <= rowEnd:
            # top
            for i in range(colStart,colEnd + 1):
                res[rowStart][i] = number
                number += 1
            # right
            for i in range(rowStart + 1, rowEnd + 1):
                res[i][colEnd] = number
                number += 1
            # bottom
            for i in range(colEnd - 1, colStart - 1, -1):
                res[rowEnd][i] = number
                number += 1
            # left
            for i in range(rowEnd - 1, rowStart, -1):
                res[i][colStart] = number
                number += 1
            colStart += 1
            colEnd -= 1
            rowStart += 1
            rowEnd -= 1
        return res
```
**Time Complexity:**  O(N^2) Here N is given input and we are iterating over N * N matrix in spiral form.

**Spcae Complexity:**  O(1)
