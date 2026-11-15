# Test Validation Log - Practical 04 (DFA Minimization)

**Student:** Krish Lalwani (Roll: 27)  
**Model Comparison:** 5-State Original DFA vs 3-State Minimized DFA  

| Test String | Expected | Original DFA (5 states) | Minimized DFA (3 states) | Result |
|:---:|:---:|:---:|:---:|:---:|
| `01` | Accept | Accept | Accept | **PASS** |
| `001` | Accept | Accept | Accept | **PASS** |
| `101` | Accept | Accept | Accept | **PASS** |
| `11101` | Accept | Accept | Accept | **PASS** |
| `00` | Reject | Reject | Reject | **PASS** |
| `010` | Reject | Reject | Reject | **PASS** |
| `10` | Reject | Reject | Reject | **PASS** |
| `011` | Reject | Reject | Reject | **PASS** |

**Conclusion:** State reduction from 5 states to 3 states (40% compression) preserves formal language equivalence.
