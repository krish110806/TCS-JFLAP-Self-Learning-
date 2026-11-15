# Test Validation Log - Practical 03 (NFA to DFA Conversion)

**Student:** Krish Lalwani (Roll: 27)  
**Model Comparison:** Source NFA vs Converted DFA  

| Test String | Expected | NFA Output | DFA Output | Result |
|:---:|:---:|:---:|:---:|:---:|
| `ab` | Accept | Accept | Accept | **PASS** |
| `aab` | Accept | Accept | Accept | **PASS** |
| `bab` | Accept | Accept | Accept | **PASS** |
| `abaab` | Accept | Accept | Accept | **PASS** |
| `ba` | Reject | Reject | Reject | **PASS** |
| `abb` | Reject | Reject | Reject | **PASS** |
| `baba` | Reject | Reject | Reject | **PASS** |
| `bbbb` | Reject | Reject | Reject | **PASS** |

**Equivalence Confirmed:** $L(M_{NFA}) \equiv L(M_{DFA})$.
