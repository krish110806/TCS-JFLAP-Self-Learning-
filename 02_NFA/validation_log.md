# Test Validation Log - Practical 02 (NFA Contains 101)

**Student:** Krish Lalwani (Roll: 27)  
**Model:** Non-Deterministic Finite Automaton  
**Target Language:** $(0+1)^*101(0+1)^*$  

| No. | Input String | Target Present | Expected | Observed | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | `101` | Yes | Accept | Accept | **PASS** |
| 2 | `00101` | Yes | Accept | Accept | **PASS** |
| 3 | `11010` | Yes | Accept | Accept | **PASS** |
| 4 | `010110` | Yes | Accept | Accept | **PASS** |
| 5 | `101101` | Yes | Accept | Accept | **PASS** |
| 6 | `000` | No | Reject | Reject | **PASS** |
| 7 | `1111` | No | Reject | Reject | **PASS** |
| 8 | `1001` | No | Reject | Reject | **PASS** |
| 9 | `01100` | No | Reject | Reject | **PASS** |
| 10 | `0` | No | Reject | Reject | **PASS** |

**Conclusion:** 10/10 non-deterministic execution paths evaluated and confirmed correct.
