# Test Validation Log - Practical 07 (Mealy Machine)

**Student:** Krish Lalwani (Roll: 27)  
**Transducer:** Mealy Machine (`101` sequence detector)  

| No. | Input Vector | Expected Output | Observed Output | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|
| 1 | `101` | `001` | `001` | **PASS** |
| 2 | `10101` | `00101` | `00101` | **PASS** |
| 3 | `001010` | `000010` | `000010` | **PASS** |
| 4 | `101101` | `001001` | `001001` | **PASS** |
| 5 | `0000` | `0000` | `0000` | **PASS** |
| 6 | `11100` | `00000` | `00000` | **PASS** |

**Conclusion:** Output streams precisely match theoretical Mealy transducer definitions.
