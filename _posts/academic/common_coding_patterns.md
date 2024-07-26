---
title: 'Coding Patterns'
date: 2024-07-26
permalink: /posts/2024/07/coding-patterns/
tags:
  - interview
  - coding
---
# Coding Patterns

## Linked List

A common theme in a linked-list is the idea of a slow and a fast pointer. The fast pointer moves twice as fast as the slow pointer. This is useful for finding the middle of the linked list, detecting cycles, etc.

Here is the example of finding a cycle using the slow and fast pointer technique:

```Python
def hasCycle(self, head: ListNode) -> bool:
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

Here is the example of finding the middle of the linked list:

```Python
def middleNode(self, head: ListNode) -> ListNode:
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow
```

## Binary Search

```Python
def search(self, nums: List[int], target: int) -> int:
    lo, hi = 0, len(nums) - 1
    while lo < hi:
        mid = (lo + hi) // 2
        if nums[mid] >= target:
            hi = mid
        else:
            lo = mid + 1

    if nums[lo] == target:
        return lo
    else:
        return -1
```

This is a template for binary search that works on a sorted array. The search space is reduced by half in each iteration. The time complexity is O(log n).

Notes:
1. The stopping condition is `lo < hi` instead of `lo <= hi`. This is because `hi` is always updated to `mid` and `mid` is always rounded down. So, if `lo == hi`, then `mid` will be equal to `lo` and the loop will not terminate.
2. The final answer is found at `lo` because the loop terminates when `lo == hi`.
3. The search condition `nums[mid] >= target` is used to find the first element that is greater than or equal to the target. If the condition is `nums[mid] > target`, then the first element that is greater than the target will be found.

## Backtracking

```Python
ans = [] # Note: This can be a set() as well

def is_valid_state(state):
    # check if it is a valid solution
    return True

def get_candidates(state):
    return []

def backtrack(state):
    if is_valid_state(state):
        ans.append(state.copy())
        # return

    for candidate in get_candidates(state):
        state.append(candidate)
        backtrack(state)
        state.remove(candidate)

state = []
search(state)
```

Notes:
1. `is_valid_state` checks if the current state is a valid solution. If it is, then the current state is added to the answer. Optionally, you can return after.
2. `get_candidates` returns a list of candidates that can be added to the current state. This
function should in theory check the "validity" of adding a candidate to the current state.
A common constraint would for example be to not add a candidate that is already in the state.