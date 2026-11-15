# Test Validation Log - Practical 05 (RE to DFA)

**Student:** Krish Lalwani (Roll: 27)  
**Regular Expression:** `(a+b)*abb`  

| Input String | Suffix Matched | Expected | DFA Observed | Status |
|:---:|:---:|:---:|:---:|:---:|
| `abb` | `abb` | Accept | Accept | **PASS** |
| `aabb` | `abb` | Accept | Accept | **PASS** |
| `babb` | `abb` | Accept | Accept | **PASS** |
| `ababb` | `abb` | Accept | Accept | **PASS** |
| `a` | `a` | Reject | Reject | **PASS** |
| `ab` | `ab` | Reject | Reject | **PASS** |
| `abba` | `a` | Reject | Reject | **PASS** |
| `bb` | $\epsilon$ | Reject | Reject | **PASS** |

**Conclusion:** Converted DFA accurately tracks regular expression language properties.
