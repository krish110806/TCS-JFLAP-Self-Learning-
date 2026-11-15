# Test Validation Log - Practical 13 (LL1 Parsing)

**Student:** Krish Lalwani (Roll: 27)  
**Grammar Type:** LL(1) Deterministic Top-Down Grammar  

| Expression String | Tokenized Input | Expected Result | JFLAP LL(1) Parser | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|
| `i+i` | `i+i$` | Accept | Successfully Parsed | **PASS** |
| `i*i` | `i*i$` | Accept | Successfully Parsed | **PASS** |
| `i+i*i` | `i+i*i$` | Accept | Successfully Parsed | **PASS** |
| `(i+i)*i` | `(i+i)*i$` | Accept | Successfully Parsed | **PASS** |
| `+i` | `+i$` | Reject | Parsing Error | **PASS** |
| `i+` | `i+$` | Reject | Incomplete Expression | **PASS** |
| `(i+i` | `(i+i$` | Reject | Missing Parenthesis | **PASS** |

**Conclusion:** Conflict-free LL(1) parse table verified in JFLAP.
