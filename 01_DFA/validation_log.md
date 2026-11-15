# Test Validation Log - Practical 01 (DFA Divisible by 3)

**Student:** Krish Lalwani (Roll: 27)  
**Model:** Deterministic Finite Automaton  
**Target Language:** Binary Numbers Divisible by 3  

| No. | Input String | Decimal | Expected Result | Observed Result | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | `0` | 0 | Accept | Accept | **PASS** |
| 2 | `11` | 3 | Accept | Accept | **PASS** |
| 3 | `110` | 6 | Accept | Accept | **PASS** |
| 4 | `1001` | 9 | Accept | Accept | **PASS** |
| 5 | `1100` | 12 | Accept | Accept | **PASS** |
| 6 | `1111` | 15 | Accept | Accept | **PASS** |
| 7 | `1` | 1 | Reject | Reject | **PASS** |
| 8 | `10` | 2 | Reject | Reject | **PASS** |
| 9 | `100` | 4 | Reject | Reject | **PASS** |
| 10 | `101` | 5 | Reject | Reject | **PASS** |
| 11 | `111` | 7 | Reject | Reject | **PASS** |
| 12 | `1010` | 10 | Reject | Reject | **PASS** |

**Conclusion:** 12/12 test vectors passed with zero divergence.
