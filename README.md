# LeetCode Helper — Java Edition

LeetCode Helper (Java) is a Codex skill for solving LeetCode-style coding interview
problems with optimized solutions and detailed explanations — all in **Java**.

## Owner

Aman Attar  
GitHub: https://github.com/amanattar/

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
