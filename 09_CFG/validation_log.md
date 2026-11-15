# Test Validation Log - Practical 09 (CFG a^n b^2n)

**Student:** Krish Lalwani (Roll: 27)  
**Grammar:** $S \to aSbb \mid abb$  

| Input String | Expected Result | Derivation Length | JFLAP Derivation | Pass/Fail |
|:---:|:---:|:---:|:---:|:---:|
| `abb` | Accept | 1 step | Successful | **PASS** |
| `aabbbb` | Accept | 2 steps | Successful | **PASS** |
| `aaabbbbbb` | Accept | 3 steps | Successful | **PASS** |
| `ab` | Reject | N/A | Syntax Error / Failed | **PASS** |
| `aabb` | Reject | N/A | Syntax Error / Failed | **PASS** |
| `abbb` | Reject | N/A | Syntax Error / Failed | **PASS** |
| `baabb` | Reject | N/A | Syntax Error / Failed | **PASS** |

**Conclusion:** CFG successfully derives all valid context-free strings while rejecting invalid ratios.
