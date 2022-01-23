# Day 2 (Leetcode)

## 349.两个数组的交集

+ 把第一个数组倒置成一个元组, 形成索引

  ```python
  class Solution:
      def intersection(self, nums1, nums2):
          """
          :type nums1: List[int]
          :type nums2: List[int]
          :rtype: List[int]
          """
          nums2 = list(set(nums2))
          back = []
          dictNums1 = {}
          for num1 in nums1:
              dictNums1[num1] = 1
   
          for num2 in nums2:
              if dictNums1.get(num2) == 1:
                  back.append(num2)
          return back
   
  if __name__ == '__main__':
      a = Solution();
      print(a.intersection,1,2,3], [3,2,3,4]))
  ```

+ 这题用set貌似更简便

  ```python
  class Solution:
      def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
          return list(set(nums1) & set(nums2))    # 两个数组先变成集合，求交集后还原为数组
  
  ```

  

## 88.合并两个有序数组

+ 假设nums1和nums2里的元素分别为m和n,然后对组1，组2遍历，如果组1已遍历，组2还有未放入的元素的话，直接遍历然后放入组1尾部

  ```python
  class solution:
      def merge (self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
          """
          Do not return anything, modify nums1 in-place instead.
          """
          nums1[m:]=nums2
          nums1.sort()
  ```

  

## 234.回文链表

+ 遍历，然后判断结果是否为题目所求。(然而下面这个是我报错的代码，我还没找出哪里错了。)

```python
 class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if not head:
            return True
        tmp = []
        pre = head
        while pre.next:
            tmp.append(pre.val)
            pre = pre.next
        tmp.append(pre.val)
        return tmp == tmp[::-1]


```

