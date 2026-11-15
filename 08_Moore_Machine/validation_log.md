# Test Validation Log - Practical 08 (Moore Machine)

**Student:** Krish Lalwani (Roll: 27)  
**Transducer:** Moore Machine (Binary Modulo 3 Evaluator)  

| Input String | Decimal Value | Expected Output | Observed Output | Result |
|:---:|:---:|:---:|:---:|:---:|
| `0` | 0 | `00` | `00` | **PASS** |
| `1` | 1 | `01` | `01` | **PASS** |
| `10` | 2 | `012` | `012` | **PASS** |
| `11` | 3 | `010` | `010` | **PASS** |
| `100` | 4 | `0121` | `0121` | **PASS** |
| `101` | 5 | `0122` | `0122` | **PASS** |
| `110` | 6 | `0100` | `0100` | **PASS** |
| `111` | 7 | `0101` | `0101` | **PASS** |

**Conclusion:** State output synchronization rigorously satisfies $\text{val}(w) \pmod 3$.
