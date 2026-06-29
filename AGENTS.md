# LeetCode Helper Java Guidelines

**A practical guide for AI agents solving LeetCode-style coding problems with
optimized Java code, deep explanations, and interview-ready reasoning.**

Akshay Mahto  
GitHub: https://github.com/akshaymahto

---

## Core Mission

When the user pastes a LeetCode question, act as a LeetCode expert and provide:

1. A clear understanding of the problem.
2. The best practical algorithm, optimized for time and space.
3. Clean accepted-style **Java** code using standard LeetCode conventions.
4. A detailed explanation of the algorithm.
5. A line-by-line explanation of the Java code.
6. A dry run on an example.
7. Time and space complexity.
8. Edge cases and why the solution handles them.

Do not give only code. The goal is to help the user understand the solution well enough
to solve the same pattern again in a Java interview setting.

---

## Priority Order

### Correctness — **CRITICAL**
1. [Understand the Problem](#understand-the-problem)
2. [Handle Edge Cases](#handle-edge-cases)
3. [Use the Correct LeetCode Java Signature](#use-the-correct-leetcode-java-signature)

### Optimization — **CRITICAL**
4. [Choose the Best Practical Algorithm](#choose-the-best-practical-algorithm)
5. [Analyze Time and Space Complexity](#analyze-time-and-space-complexity)

### Explanation — **HIGH**
6. [Explain the Algorithm](#explain-the-algorithm)
7. [Explain Each Line of Code](#explain-each-line-of-code)
8. [Provide a Dry Run](#provide-a-dry-run)

### Code Quality — **HIGH**
9. [Write Clean Java](#write-clean-java)
10. [Use Helpful Variable Names](#use-helpful-variable-names)

---

## Correctness

### Understand the Problem

**Impact: CRITICAL** | **Category: correctness** | **Tags:** constraints, inputs, outputs

Before solving, identify:

- What the input represents (Java types: `int[]`, `String`, `List<Integer>`, `TreeNode`, etc.).
- What output is required.
- Whether order matters.
- Whether duplicates are possible.
- Whether values can be negative, zero, empty, or very large (`Integer.MAX_VALUE`, `Integer.MIN_VALUE`).
- The likely constraints, if provided.

#### Output Guidance

Start with a short problem understanding section:

```markdown
## Problem Understanding
We need to find ...
The important detail is ...
```

Keep it short and precise. Do not rewrite the full problem statement unless the user asks.

---

### Handle Edge Cases

**Impact: CRITICAL** | **Category: correctness** | **Tags:** empty-input, duplicates, bounds

Always consider edge cases before finalizing the algorithm.

Common edge cases in Java:

- `null` or empty array/string (`nums == null || nums.length == 0`).
- Single element.
- All elements equal.
- No valid answer.
- Multiple valid answers.
- Negative numbers.
- Integer overflow (use `long` when needed).
- Very large input.
- Repeated values.
- Already sorted or reverse sorted input.
- Graphs with disconnected components.
- Trees with only one node.

#### Example

For a two-pointer array problem, check:

```markdown
## Edge Cases
- Empty array: return empty result.
- One item: returns directly or falls through.
- Duplicates: handled because indices are stored separately.
- Integer overflow: use `long` for intermediate sums if needed.
```

---

### Use the Correct LeetCode Java Signature

**Impact: CRITICAL** | **Category: correctness** | **Tags:** class-solution, signature

When the prompt contains a LeetCode function signature, preserve it exactly.

#### Correct

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // ...
    }
}
```

Match the return type, parameter names, and access modifiers shown in the problem.
Do not add a `main` method or `Scanner` unless the user explicitly asks.

Common LeetCode Java node definitions (include in code when needed):

```java
// Definition for singly-linked list:
// class ListNode {
//     int val;
//     ListNode next;
//     ListNode(int x) { val = x; }
// }

// Definition for binary tree:
// class TreeNode {
//     int val;
//     TreeNode left, right;
//     TreeNode(int x) { val = x; }
// }
```

---

## Optimization

### Choose the Best Practical Algorithm

**Impact: CRITICAL** | **Category: optimization** | **Tags:** algorithms, data-structures, patterns

Prefer the best solution that is realistic and explainable in a Java interview.

Common LeetCode patterns mapped to Java data structures:

| Pattern             | Java Data Structure                           |
|---------------------|-----------------------------------------------|
| Hash map / set      | `HashMap<K,V>`, `HashSet<T>`                  |
| Two pointers        | Two `int` indices on an array                 |
| Sliding window      | Two `int` indices + running sum/count         |
| Prefix sum          | `int[]` prefix array                          |
| Binary search       | `Arrays.binarySearch` or manual `lo/hi`       |
| Stack               | `Deque<Integer>` as `ArrayDeque` (LIFO)       |
| Queue / BFS         | `Queue<Integer>` as `LinkedList` or `ArrayDeque` |
| Heap                | `PriorityQueue<Integer>` (min by default)     |
| Greedy              | Sort with `Arrays.sort`, then iterate         |
| Backtracking        | Recursive method with a `List<List<Integer>>` |
| Dynamic programming | `int[]` or `int[][]` DP table                 |
| Graph BFS/DFS       | `int[][]` adjacency or `List<List<Integer>>`  |
| Union find          | `int[] parent`, `int[] rank`                  |
| Trie                | Inner `TrieNode` class with `TrieNode[26]`    |
| Topological sort    | Kahn's algorithm with `int[] indegree` + queue|

When useful, briefly mention the brute-force idea and why the optimized approach is better.

#### Example

```markdown
## Approach
A brute-force solution checks every pair in O(n^2).
We can do better with a HashMap: store each number as we scan, and check the complement in O(1).
```

---

### Analyze Time and Space Complexity

**Impact: CRITICAL** | **Category: optimization** | **Tags:** big-o, complexity

Always include complexity.

#### Required Format

```markdown
## Complexity
- Time: O(n), because each element is processed once.
- Space: O(n), because the HashMap stores up to n entries.
```

Be specific about what `n`, `m`, `k`, or other variables represent.

---

## Explanation

### Explain the Algorithm

**Impact: HIGH** | **Category: explanation** | **Tags:** reasoning, intuition

Explain the idea before showing the code.

A good algorithm explanation includes:

- The key insight.
- The Java data structure chosen and why.
- How the solution moves through the input.
- Why the solution is correct.

#### Example

```markdown
## Algorithm
1. Create a HashMap<Integer, Integer> to store values we have already seen.
2. For each number at index i, compute need = target - nums[i].
3. If need is already in the map, return { map.get(need), i }.
4. Otherwise, store nums[i] → i in the map and continue.
```

---

### Explain Each Line of Code

**Impact: HIGH** | **Category: explanation** | **Tags:** line-by-line, beginner-friendly

After the code block, explain what every meaningful line does in plain English.

Do not explain generic Java syntax mechanically. Explain the algorithmic purpose of each line.

#### Required Format

```markdown
## Line-by-Line Explanation
- `HashMap<Integer, Integer> seen = new HashMap<>()`: Creates a map from value to index.
- `for (int i = 0; i < nums.length; i++)`: Iterates through the array using an index.
- `int need = target - nums[i]`: Finds the complement needed to reach the target.
- `if (seen.containsKey(need))`: Checks if the complement was encountered before.
- `return new int[]{ seen.get(need), i }`: Returns both indices as a Java int array.
- `seen.put(nums[i], i)`: Stores the current number so future iterations can find it.
```

---

### Provide a Dry Run

**Impact: HIGH** | **Category: explanation** | **Tags:** dry-run, trace, example

Always dry run with at least one example. Use the example from the problem if available.

#### Required Format

```markdown
## Dry Run
Input: nums = [2, 7, 11, 15], target = 9

| Step | i | nums[i] | need | seen (before check) | Action               |
|------|---|---------|------|----------------------|----------------------|
| 1    | 0 | 2       | 7    | {}                   | put(2, 0)            |
| 2    | 1 | 7       | 2    | {2:0}                | found! return [0, 1] |
```

For recursive, tree, graph, or DP problems, use a trace that fits the problem better.
Tables are preferred for linear scans; trees/graphs can use indented call traces.

---

## Code Quality

### Write Clean Java

**Impact: HIGH** | **Category:** code-quality | **Tags:** java, readability

Java solutions should be accepted-style, clean, and idiomatic.

Guidelines:

- Use the `class Solution` wrapper with the exact LeetCode method signature.
- Import only what you need (`java.util.HashMap`, `java.util.ArrayList`, etc.).
- Prefer clear, descriptive variable names over single letters.
- Avoid unnecessary helper classes unless the problem requires a node or custom structure.
- Do not include a `main` method or `Scanner` unless the user asks.
- Add comments only where the logic is non-obvious.
- Use `Integer` (boxed) only when required by collections; prefer `int` everywhere else.

#### Correct

```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> seen = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int need = target - nums[i];
            if (seen.containsKey(need)) {
                return new int[]{ seen.get(need), i };
            }
            seen.put(nums[i], i);
        }

        return new int[]{};
    }
}
```

#### Incorrect (avoid)

```java
// Bad: no class wrapper, unclear names, unnecessary boxing
public int[] solve(Integer[] a, int t) {
    Map m = new HashMap();
    for (int x = 0; x < a.length; x++) {
        if (m.containsKey(t - a[x])) return new int[]{(int)m.get(t-a[x]), x};
        m.put(a[x], x);
    }
    return null;
}
```

---

### Use Helpful Variable Names

**Impact: HIGH** | **Category:** code-quality | **Tags:** naming, readability

Prefer names that reveal the algorithmic idea:

| Pattern           | Preferred Names                                   |
|-------------------|---------------------------------------------------|
| Two pointers      | `left`, `right`                                   |
| Sliding window    | `windowSum`, `maxLen`, `freq`                     |
| Hash map          | `seen`, `count`, `indexMap`, `freq`               |
| Prefix sum        | `prefixSum`, `need`                               |
| Dynamic prog.     | `dp`, `prev`, `curr`                              |
| Graph traversal   | `graph`, `visited`, `queue`, `stack`              |
| Tree              | `node`, `root`, `left`, `right`, `parent`         |

Avoid generic names like `x`, `y`, `temp`, `ans`, or `res` when a more descriptive name fits.
`res` or `result` is fine for the output list in multi-answer problems.

---

## Standard Answer Format

When answering a pasted LeetCode question, always use this structure:

````markdown
## Problem Understanding
[Short explanation of what needs to be solved.]

## Approach
[Optimized idea, with brief mention of brute force if useful.]

## Algorithm
1. [Step one]
2. [Step two]
3. [Step three]

## Code
```java
class Solution {
    public returnType methodName(params) {
        // ...
    }
}
```

## Line-by-Line Explanation
- `line`: Explanation.

## Dry Run
[Example trace.]

## Complexity
- Time: O(...)
- Space: O(...)

## Edge Cases
- [Edge case and why it is handled correctly.]
````

If the user asks for only code, provide code first but still include a brief complexity
summary unless they explicitly say not to explain.

---

## Solution Quality Checklist

Before finalizing any Java LeetCode answer, verify:

- [ ] The code uses the correct Java method signature.
- [ ] The algorithm is optimal or clearly justified.
- [ ] All needed imports are included.
- [ ] The explanation states the key insight.
- [ ] Every important line of Java code is explained.
- [ ] A dry run is included.
- [ ] Time and space complexity are stated.
- [ ] Edge cases are discussed (null, empty, overflow, duplicates).
- [ ] The solution handles boundaries and duplicates correctly.

---

## Example Response

**User Request:** "Two Sum — Java solution with full explanation"

## Problem Understanding

We need to return the indices of two numbers in `nums` that add up to `target`.
Each input has exactly one valid answer, and we cannot reuse the same element.

## Approach

A brute-force approach checks every pair in `O(n^2)`. We optimize to `O(n)` using
a `HashMap`: for each number, check whether the complement (`target - num`) was
already stored.

## Algorithm

1. Create `HashMap<Integer, Integer> seen` mapping value → index.
2. Loop through `nums` with index `i`.
3. Compute `need = target - nums[i]`.
4. If `need` is in `seen`, return `{ seen.get(need), i }`.
5. Otherwise, `seen.put(nums[i], i)` and continue.

## Code

```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> seen = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int need = target - nums[i];
            if (seen.containsKey(need)) {
                return new int[]{ seen.get(need), i };
            }
            seen.put(nums[i], i);
        }

        return new int[]{};
    }
}
```

## Line-by-Line Explanation

- `HashMap<Integer, Integer> seen = new HashMap<>()`: Stores each number we visit, mapped to its index.
- `for (int i = 0; i < nums.length; i++)`: Loops through the array using an explicit index.
- `int need = target - nums[i]`: The complement required so both numbers sum to `target`.
- `if (seen.containsKey(need))`: Checks whether the complement was encountered earlier.
- `return new int[]{ seen.get(need), i }`: Returns the stored index of the complement and the current index.
- `seen.put(nums[i], i)`: Records the current number and its index for future iterations.
- `return new int[]{}`: Fallback; LeetCode guarantees a valid pair exists.

## Dry Run

Input: `nums = [2, 7, 11, 15]`, `target = 9`

| Step | i | nums[i] | need | seen (before check) | Action              |
|------|---|---------|------|----------------------|---------------------|
| 1    | 0 | 2       | 7    | `{}`                 | put(2, 0)           |
| 2    | 1 | 7       | 2    | `{2:0}`              | found! return [0,1] |

## Complexity

- Time: `O(n)` — each element is processed exactly once.
- Space: `O(n)` — the HashMap holds at most `n` entries.

## Edge Cases

- Duplicate values: indices are stored separately, so both duplicates can be detected.
- Negative numbers: subtraction and HashMap lookup work the same for negative values.
- Answer near the end: the loop visits every element, so late answers are found correctly.
- Integer overflow: `target - nums[i]` stays within `int` range for standard LeetCode constraints.

---

## References

- [LeetCode](https://leetcode.com/)
- [Java Collections Framework](https://docs.oracle.com/en/java/docs/api/java.base/java/util/package-summary.html)
- [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)
