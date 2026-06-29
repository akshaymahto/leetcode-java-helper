# LeetCode Helper — Java Edition

LeetCode Helper (Java) is a Codex skill for solving LeetCode-style coding interview
problems with optimized solutions and detailed explanations — all in **Java**.

## Owner

Akshay Mahto  
GitHub: https://github.com/akshaymahto

## What It Does

When you paste a LeetCode problem, this skill guides the agent to provide:

- Problem understanding in plain language.
- An optimized algorithmic approach.
- Clean LeetCode-ready **Java** code using standard `class Solution` conventions.
- Step-by-step algorithm explanation.
- Line-by-line Java code explanation.
- A dry run using an example input.
- Time and space complexity analysis.
- Important edge cases (including null, empty, overflow, duplicates).

## Skill Files

| File        | Purpose                                                        |
|-------------|----------------------------------------------------------------|
| `SKILL.md`  | Skill metadata, trigger rules, output format, and Java example |
| `AGENTS.md` | Detailed behavior rules, Java patterns, answer format, example |
| `README.md` | Overview, usage guide, and Java-specific notes                 |

## Java-Specific Features

This skill is tuned for Java interviews and includes:

- Correct usage of `HashMap`, `HashSet`, `ArrayList`, `ArrayDeque`, `PriorityQueue`.
- Proper LeetCode Java signatures (`class Solution { public ... }`).
- Integer overflow handling (`long` when needed).
- Common node class definitions for trees and linked lists.
- A pattern-to-data-structure reference table for quick selection.

## Example Use

Paste a LeetCode question and ask for an optimized Java solution.

**Example prompt:**
```
Solve Two Sum in Java with full explanation.
```

**The response will include:**
- Problem Understanding
- Approach (with brute-force comparison)
- Algorithm steps
- Java code inside `class Solution`
- Line-by-line explanation
- Dry run table
- Time and space complexity
- Edge cases

## Supported Algorithm Patterns

- Hash Map / Hash Set
- Two Pointers
- Sliding Window
- Prefix Sum
- Binary Search
- Stack / Monotonic Stack
- Heap / PriorityQueue
- Greedy
- Backtracking
- Dynamic Programming
- BFS / DFS (Graph and Tree)
- Union Find
- Trie
- Topological Sort

## Getting Started

1. Copy this skill folder into your Claude/Codex skills directory.
2. Paste any LeetCode problem into the chat.
3. Ask for a Java solution with explanation.

The skill will automatically follow the structured response format defined in
`AGENTS.md`.

## License

MIT

# 🧠 LeetCode Java Solutions

> Clean, optimized, and well-explained Java solutions for LeetCode problems — built for coding interview prep.

---

## 📌 Table of Contents

- [About](#about)
- [How to Use](#how-to-use)
- [Problems](#problems)
  - [3Sum — Two Pointers](#3sum--two-pointers)
- [Complexity Cheat Sheet](#complexity-cheat-sheet)
- [Contributing](#contributing)

---

## About

This repository contains Java solutions to popular LeetCode problems. Each solution includes:

- **Problem understanding** in plain language
- **Optimized approach** with reasoning
- **Clean Java code** using standard collections
- **Step-by-step dry run** with a real example
- **Time and space complexity** analysis
- **Edge cases** to watch out for

---

## How to Use

Each solution is self-contained inside a `Solution` class, ready to paste directly into LeetCode.

```bash
# Clone the repo
git clone https://github.com/your-username/leetcode-java-solutions.git
cd leetcode-java-solutions
```

---

## Problems

---

### 3Sum — Two Pointers

**LeetCode #15** · Difficulty: `Medium` · Pattern: `Sorting + Two Pointers`

#### Problem

Given an integer array `nums`, return all unique triplets `[nums[i], nums[j], nums[k]]` such that they are distinct indices and `nums[i] + nums[j] + nums[k] == 0`.

**Example:**
```
Input:  nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
```

---

#### Approach

Sort the array first. Then fix one element (the **anchor**) and use **two pointers** — one from the left, one from the right — to find pairs that sum to the negation of the anchor.

Sorting makes it easy to:
- Skip duplicate anchors and pointer values (to avoid duplicate triplets)
- Move pointers in the right direction based on whether the sum is too small or too large

---

#### Algorithm

1. Sort `nums`.
2. Loop through each index `i` as the anchor.
3. Skip duplicate anchors: `if (i > 0 && nums[i] == nums[i-1]) continue`.
4. Set `left = i + 1`, `right = nums.length - 1`.
5. While `left < right`:
   - **Sum == 0** → record triplet, skip duplicates, shrink window.
   - **Sum < 0** → move `left` right (need a bigger value).
   - **Sum > 0** → move `right` left (need a smaller value).

---

#### Code

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 2; i++) {
            // Skip duplicate anchor values
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {
                    result.add(Arrays.asList(nums[i], nums[left], nums[right]));

                    // Skip duplicates on both sides
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;

                    left++;
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    right--;
                }
            }
        }

        return result;
    }
}
```

---

#### Line-by-Line Explanation

| Line | Purpose |
|------|---------|
| `Arrays.sort(nums)` | Sorts the array so duplicates are adjacent and two-pointer logic works |
| `for (int i = 0; i < nums.length - 2; i++)` | Iterates up to `length - 2` — at least 2 more elements needed for left/right |
| `if (i > 0 && nums[i] == nums[i - 1]) continue` | Skips duplicate anchor values to avoid duplicate triplets |
| `int left = i + 1; int right = nums.length - 1` | Sets two-pointer boundaries around the rest of the array |
| `int sum = nums[i] + nums[left] + nums[right]` | Computes the current three-way sum |
| `result.add(Arrays.asList(...))` | Records a valid triplet |
| Inner `while` loops after match | Skips over duplicate values of `left` and `right` before moving the pointers |
| `left++; right--` | Shrinks the window to continue searching for more triplets |
| `else if (sum < 0) left++` | Sum is too small — move left pointer right for a bigger value |
| `else right--` | Sum is too big — move right pointer left for a smaller value |

---

#### Dry Run

**Input:** `nums = [-1, 0, 1, 2, -1, -4]`  
**After sort:** `[-4, -1, -1, 0, 1, 2]`

| Step | i | anchor | left | right | sum | action |
|------|---|--------|------|-------|-----|--------|
| 1 | 0 | -4 | -1 (idx 1) | 2 (idx 5) | -3 | sum < 0 → left++ |
| 2 | 0 | -4 | -1 (idx 2) | 2 (idx 5) | -3 | sum < 0 → left++ |
| 3 | 0 | -4 | 0 (idx 3) | 2 (idx 5) | -2 | sum < 0 → left++ |
| 4 | 0 | -4 | 1 (idx 4) | 2 (idx 5) | -1 | sum < 0 → left++ |
| 5 | 1 | -1 | -1 (idx 2) | 2 (idx 5) | 0 | ✅ add `[-1,-1,2]`, skip dups, left++, right-- |
| 6 | 1 | -1 | 0 (idx 3) | 1 (idx 4) | 0 | ✅ add `[-1,0,1]`, left++, right-- |
| 7 | 2 | -1 | skip (dup anchor) | — | — | continue |
| 8 | 3 | 0 | 1 (idx 4) | 2 (idx 5) | 3 | sum > 0 → right-- |

**Result:** `[[-1, -1, 2], [-1, 0, 1]]` ✅

---

#### Complexity

| | Complexity | Notes |
|-|------------|-------|
| **Time** | `O(n²)` | Sort is `O(n log n)`; nested loop dominates at `O(n²)` |
| **Space** | `O(1)` | Sorting is in-place; no extra data structures (output list excluded) |

---

#### Edge Cases

| Case | Input | Behavior |
|------|-------|----------|
| All zeros | `[0, 0, 0, 0]` | Correctly outputs `[[0, 0, 0]]` — duplicate-skip handles it |
| No valid triplet | `[1, 2, 3]` | Loop finds no sum = 0, returns empty list |
| All same negatives | `[-1, -1, -1]` | Returns empty — three negatives can never sum to 0 |
| All same positives | `[1, 1, 1]` | Returns empty — three positives can never sum to 0 |
| Early exit (optional optimization) | anchor `> 0` | If `nums[i] > 0`, all remaining are also positive → `break` early |

---

## Complexity Cheat Sheet

| Pattern | Time | Space | When to Use |
|---------|------|-------|-------------|
| Two Pointers (sorted) | O(n) or O(n²) | O(1) | Pair/triplet sums in sorted arrays |
| HashMap | O(n) | O(n) | Unsorted arrays, index lookups |
| Sliding Window | O(n) | O(1) | Subarrays/substrings with constraints |
| Binary Search | O(log n) | O(1) | Sorted arrays, monotonic functions |
| BFS / DFS | O(V+E) | O(V) | Graphs, trees, connected components |

---

## Contributing

Pull requests are welcome! Please follow this format for new solutions:

1. Add your solution under a new section with problem number and pattern.
2. Include: approach, code, line-by-line explanation, dry run, complexity, edge cases.
3. Keep the code LeetCode-ready (no `main` method, no stdin/stdout).

---

> ⭐ If this helped you, consider starring the repo!