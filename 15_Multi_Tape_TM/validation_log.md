# Test Validation Log - Practical 15 (Multi-Tape TM)

**Student:** Krish Lalwani (Roll: 27)  
**Architecture:** 2-Tape Deterministic Turing Machine  
**Function:** $f(w) = ww$ (String Duplication)  

| Input ($w$) | Expected Tape 1 | Expected Tape 2 | Observed Tape 1 | Observed Tape 2 | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|:---:|
| `0` | `00` | `0` | `00` | `0` | **PASS** |
| `1` | `11` | `1` | `11` | `1` | **PASS** |
| `01` | `0101` | `01` | `0101` | `01` | **PASS** |
| `10` | `1010` | `10` | `1010` | `10` | **PASS** |
| `101` | `101101` | `101` | `101101` | `101` | **PASS** |
| `1100` | `11001100` | `1100` | `11001100` | `1100` | **PASS** |

**Conclusion:** 2-Tape TM accomplishes linear time $O(n)$ string duplication without tape overwriting anomalies.
