# Test Validation Log - Practical 12 (CYK Parsing)

**Student:** Krish Lalwani (Roll: 27)  
**Parsing Model:** CYK Algorithm (Dynamic Programming $O(n^3)$)  

| Input String | Length | Root Cell $V[1, n]$ Contains $S$? | Expected | JFLAP CYK Result | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|:---:|
| `ab` | 2 | Yes ($V[1,2] = \{S\}$) | Accept | Accept | **PASS** |
| `aabb` | 4 | Yes ($V[1,4] = \{S\}$) | Accept | Accept | **PASS** |
| `aaabbb` | 6 | Yes ($V[1,6] = \{S\}$) | Accept | Accept | **PASS** |
| `ba` | 2 | No ($V[1,2] = \emptyset$) | Reject | Reject | **PASS** |
| `abab` | 4 | No ($S \notin V[1,4]$) | Reject | Reject | **PASS** |
| `aab` | 3 | No ($S \notin V[1,3]$) | Reject | Reject | **PASS** |

**Conclusion:** CYK dynamic table rigorously discriminates membership in $O(n^3)$ complexity.
