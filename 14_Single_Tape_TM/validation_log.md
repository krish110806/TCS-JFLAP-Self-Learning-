# Test Validation Log - Practical 14 (Single-Tape TM)

**Student:** Krish Lalwani (Roll: 27)  
**Model:** Single-Tape Deterministic Turing Machine  
**Function:** $f(w) = w + 1$ (Binary Incrementer)  

| Input Tape ($w$) | Decimal In | Expected Output ($w+1$) | Decimal Out | Observed Tape | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|:---:|
| `0` | 0 | `1` | 1 | `1` | **PASS** |
| `1` | 1 | `10` | 2 | `10` | **PASS** |
| `10` | 2 | `11` | 3 | `11` | **PASS** |
| `11` | 3 | `100` | 4 | `100` | **PASS** |
| `100` | 4 | `101` | 5 | `101` | **PASS** |
| `101` | 5 | `110` | 6 | `110` | **PASS** |
| `111` | 7 | `1000` | 8 | `1000` | **PASS** |
| `1101` | 13 | `1110` | 14 | `1110` | **PASS** |

**Conclusion:** All binary ripple-carry arithmetic operations verified on Turing machine tape.
