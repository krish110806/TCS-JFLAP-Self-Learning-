# Test Validation Log - Practical 10 (PDA for w c w^R)

**Student:** Krish Lalwani (Roll: 27)  
**Model:** Deterministic Pushdown Automaton (DPDA)  
**Language:** $L = \{ w c w^R \mid w \in \{a,b\}^* \}$  

| No. | Input Vector | Description | Expected | Observed | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | `c` | Base case $w = \epsilon$ | Accept | Accept | **PASS** |
| 2 | `aca` | Length 1 palindrome | Accept | Accept | **PASS** |
| 3 | `bcb` | Length 1 palindrome | Accept | Accept | **PASS** |
| 4 | `abcba` | Length 2 palindrome | Accept | Accept | **PASS** |
| 5 | `abbcbba` | Length 3 palindrome | Accept | Accept | **PASS** |
| 6 | `aabacabaa`| Multi-symbol palindrome | Accept | Accept | **PASS** |
| 7 | `acb` | Mismatched characters | Reject | Reject | **PASS** |
| 8 | `abc` | Incomplete right half | Reject | Reject | **PASS** |
| 9 | `abca` | Length mismatch | Reject | Reject | **PASS** |
| 10 | `ab` | Missing center marker | Reject | Reject | **PASS** |

**Conclusion:** 10/10 test vectors passed. All LIFO stack properties verified in JFLAP.
