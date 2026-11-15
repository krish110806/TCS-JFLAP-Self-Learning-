# Test Validation Log - Practical 06 (DFA to Grammar)

**Student:** Krish Lalwani (Roll: 27)  
**Grammar Type:** Right-Linear Regular Grammar ($G = (V, \Sigma, R, S)$)  

| Input String | Expected | DFA Simulation | Grammar Parser | Result |
|:---:|:---:|:---:|:---:|:---:|
| `01` | Accept | Accept | Derived | **PASS** |
| `001` | Accept | Accept | Derived | **PASS** |
| `0101` | Accept | Accept | Derived | **PASS** |
| `0111` | Accept | Accept | Derived | **PASS** |
| `101` | Reject | Reject | Not Derived | **PASS** |
| `000` | Reject | Reject | Not Derived | **PASS** |
| `111` | Reject | Reject | Not Derived | **PASS** |
| `0` | Reject | Reject | Not Derived | **PASS** |

**Conclusion:** Exact formal equivalence established between DFA states and right-linear productions.
