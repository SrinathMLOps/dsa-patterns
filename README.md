# Pattern 1 — Two Pointers

> **Difficulty level covered:** Beginner → Advanced  
> **Live interactive demo:** [Click here to run it](https://srinathmlops.github.io/dsa-patterns/two-pointers/)  
> **LeetCode problems solved with this pattern:** Two Sum II, 3Sum, Container With Most Water, Valid Palindrome, Trapping Rain Water

---

## What is Two Pointers?

Imagine you have a **sorted row of numbers** and two fingers.

- Put one finger at the **start** (position 0)
- Put another finger at the **end** (last position)
- Add the two numbers your fingers are pointing at
- **Too big?** Move the right finger LEFT
- **Too small?** Move the left finger RIGHT
- **Match?** You found your answer!

```
arr = [2, 5, 8, 11, 14]   target = 16
       L               R

Step 1: L=0(2)  R=4(14)  → 2+14=16 ✅ Found!
```

---

## Why Not Just Use Two Loops?

A beginner would write this — it works but it is slow:

```python
# ❌ Beginner approach — O(n²)
for i in range(len(arr)):
    for j in range(i+1, len(arr)):
        if arr[i] + arr[j] == target:
            return [i, j]
# For 1000 numbers = 1,000,000 checks
```

Two Pointers does the same job 1000x faster:

```python
# ✅ Two Pointers — O(n)
left, right = 0, len(arr) - 1
while left < right:
    s = arr[left] + arr[right]
    if s == target:   return [left, right]
    elif s < target:  left += 1
    else:             right -= 1
# For 1000 numbers = ~1000 checks
```

---

## The Code — Line by Line

| Line | Code | Plain English |
|------|------|---------------|
| 1 | `left, right = 0, len(arr) - 1` | Place left finger at start, right finger at end |
| 2 | `while left < right:` | Keep going until fingers meet |
| 3 | `s = arr[left] + arr[right]` | Add the two numbers under your fingers |
| 4 | `if s == target:` | Did we find the answer? |
| 5 | `return [left, right]` | Yes! Return both positions |
| 6 | `elif s < target: left += 1` | Too small — move left finger right |
| 7 | `else: right -= 1` | Too big — move right finger left |

---

## Step by Step Walkthrough — Example 1

```
arr = [2, 5, 8, 11, 14]   target = 13

Step 1:  L→2   R→14   sum=16  TOO BIG   → move R left
         [2, 5, 8, 11, 14]
          L           R

Step 2:  L→2   R→11   sum=13  MATCH ✅
         [2, 5, 8, 11, 14]
          L        R

Answer: positions [0, 3] → values 2 and 11
```

## Step by Step Walkthrough — Example 2

```
arr = [2, 5, 8, 11, 14]   target = 10

Step 1:  L→2   R→14   sum=16  TOO BIG   → move R left
Step 2:  L→2   R→11   sum=13  TOO BIG   → move R left
Step 3:  L→2   R→8    sum=10  MATCH ✅

Answer: positions [0, 2] → values 2 and 8
```

---

## The 3 Rules to Memorise

> 1. Array **MUST be sorted** — this only works on sorted data
> 2. Sum too **small** → move **LEFT** pointer right (towards bigger numbers)
> 3. Sum too **big** → move **RIGHT** pointer left (towards smaller numbers)

---

## Big O Analysis

| Approach | Time | Space | For n=10,000 |
|----------|------|-------|--------------|
| Brute force (two loops) | O(n²) | O(1) | 100,000,000 ops |
| Two Pointers | O(n) | O(1) | 10,000 ops |
| Hash Map (unsorted) | O(n) | O(n) | 10,000 ops + memory |

Two Pointers wins when the array is already sorted — O(n) time AND O(1) space.

---

## LeetCode Problems — Solve in This Order

| # | Problem | Difficulty | What to focus on |
|---|---------|------------|-----------------|
| 167 | Two Sum II | Easy | Classic template — start here |
| 125 | Valid Palindrome | Easy | Both pointers move inward |
| 15 | 3Sum | Medium | Sort first, then two pointers inside a loop |
| 11 | Container With Most Water | Medium | Maximise area by moving shorter side |
| 42 | Trapping Rain Water | Hard | Track max from both sides |

---

## When To Use This Pattern

Ask yourself these questions:

- ✅ Is the array **sorted** (or can I sort it)?
- ✅ Am I looking for a **pair** or **triplet** that meets a condition?
- ✅ Do I need to **compare** elements from both ends?
- ✅ Am I checking for **palindrome** properties?

If yes to any → think Two Pointers first.

---

## Variations

### Variation 1 — Same direction (fast and slow pointers)
Both pointers start at the beginning but move at different speeds.
Used for: detecting cycles in linked lists, finding middle of linked list.

### Variation 2 — Remove duplicates in-place
```python
def remove_duplicates(nums):
    if not nums: return 0
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1
```

### Variation 3 — Three pointers (3Sum)
Fix one element, then use two pointers on the rest.

---

## My Solution Template (Copy This)

```python
def two_sum_sorted(arr, target):
    left, right = 0, len(arr) - 1
    
    while left < right:
        current_sum = arr[left] + arr[right]
        
        if current_sum == target:
            return [left, right]          # found
        elif current_sum < target:
            left += 1                     # need bigger sum
        else:
            right -= 1                    # need smaller sum
    
    return [-1, -1]                       # not found
```

---

*Part of my DSA Patterns series — [View all patterns](../README.md)*  
*Srinath Kaithoju | Senior DevOps Engineer | [LinkedIn](https://linkedin.com/in/srinath-kaithoju)*
