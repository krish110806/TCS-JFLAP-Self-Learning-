# Test Validation Log - Practical 11 (CNF Conversion)

**Student:** Krish Lalwani (Roll: 27)  
**Transformation:** CFG $\to$ Chomsky Normal Form  

| Input String | Original CFG Status | Converted CNF Status | Length in CNF ($2n-1$ steps) | Result |
|:---:|:---:|:---:|:---:|:---:|
| `ab` | Derived | Derived | 3 steps ($2(2)-1 = 3$) | **PASS** |
| `aabb` | Derived | Derived | 7 steps ($2(4)-1 = 7$) | **PASS** |
| `aaabbb` | Derived | Derived | 11 steps | **PASS** |
| `a` | Failed | Failed | N/A | **PASS** |
| `aab` | Failed | Failed | N/A | **PASS** |
| `abb` | Failed | Failed | N/A | **PASS** |

**Conclusion:** CNF grammar preserves strict language equivalence with standard $2|w|-1$ derivation length.
