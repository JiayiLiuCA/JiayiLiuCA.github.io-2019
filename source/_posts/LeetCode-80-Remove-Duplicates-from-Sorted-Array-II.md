---
title: LeetCode 80. Remove Duplicates from Sorted Array II
date: 2020-03-13 16:02:59
categories: [algorithm]
tags: [leetcode]
---

### LeetCode #80

Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

**Example 1**
```
Given nums = [1,1,1,2,2,3]

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
```

**Example 2**
```
Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.
```
<!--more-->

### First accepted submission
```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size()<3) {
            return nums.size();
        }
        int x = 0;
        for(int i = 1; i<nums.size();i++) {
            if (x == 0 && nums[i] == nums[x] && i==1) {
                x++; //special case for i == 1;
            }
            if (nums[i] != nums[x]) {
                nums[++x] = nums[i];
                if (i<nums.size()-1 && nums[i+1] == nums[i]) {
                    nums[++x] = nums[i++];
                }
            }
        }
        return x+1;
    }
};
```

### Second submission, cleaner code

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int i = 0;
        for(int n : nums) {
            if (i<2 || n>nums[i-2]) {
                nums[i++] = n;
            }
        }
        return i;
    }
};
```

