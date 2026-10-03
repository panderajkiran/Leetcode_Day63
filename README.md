# Leetcode_Day63
# Day 62 – Maximum Equal Adjacent Pairs After at Most One Replacement

**LeetCode Problem:** 4066. Maximum Equal Adjacent Pairs After at Most One Replacement
**Difficulty:** Medium
**Language:** Java
**Status:** Accepted ✅

## Problem Description

Given an integer array `nums`, we can choose two distinct values `x` and `y` and replace every occurrence of `x` with `y` at most once.

The goal is to find the maximum number of adjacent pairs that become equal after performing this operation.

## Approach

1. Initialize `base` to count adjacent pairs that are already equal.
2. Traverse the array and compare each element with its previous element.
3. If both elements are equal, increment `base`.
4. Otherwise, create a key representing the smaller and larger values of the pair.
5. Use a `HashMap` to count how many times each unordered pair occurs.
6. Track the maximum frequency in `max`.
7. Return `base + max` as the maximum possible number of equal adjacent pairs.

### Java Solution

```java
import java.util.HashMap;

class Solution {
    public int maxEqualAdjacentPairs(int[] nums) {
        HashMap<Long, Integer> map = new HashMap<>();

        int base = 0;
        int max = 0;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) {
                base++;
            } else {
                int a = Math.min(nums[i], nums[i - 1]);
                int b = Math.max(nums[i], nums[i - 1]);

                long key = (long) a * 1000000001L + b;

                map.put(key, map.getOrDefault(key, 0) + 1);

                int cnt = map.get(key);
                max = Math.max(max, cnt);
            }
        }

        return base + max;
    }
}
```

## Example

**Input:**

```text
nums = [1, 2, 3, 2]
```

**Output:**

```text
2
```

**Explanation:**

The adjacent pairs are `(1,2)`, `(2,3)`, and `(3,2)`.

The pairs `(2,3)` and `(3,2)` contain the same two values. By replacing every occurrence of `3` with `2`, the array becomes `[1,2,2,2]`.

There are now two equal adjacent pairs, so the answer is `2`.

## Complexity Analysis

* **Time Complexity:** `O(n)` — We traverse the array once, and each HashMap operation takes expected constant time.
* **Space Complexity:** `O(n)` — The HashMap may store up to `n - 1` distinct adjacent value pairs.

## What I Learned

* How to use a HashMap to count the frequency of adjacent value pairs.
* Why sorting two values before creating a key helps treat `(a, b)` and `(b, a)` as the same pair.
* How to separate the pairs that are already equal from the pairs that can become equal after one replacement.
* How frequency counting can help solve array problems efficiently.

## Takeaway

Today's problem reminded me that a small observation can simplify a problem that initially looks complicated. Understanding the relationship between adjacent elements helped me turn the replacement operation into a frequency-counting problem.

**Day 62 complete! Consistency, one problem and one lesson at a time.** 🚀
