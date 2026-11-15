# Practical 05: Regular Expression to DFA Conversion

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary RE File:** [`27_Krish_Lalwani_RE_14-11-2026.jff`](27_Krish_Lalwani_RE_14-11-2026.jff)  
**Generated DFA File:** [`27_Krish_Lalwani_DFA_from_RE_14-11-2026.jff`](27_Krish_Lalwani_DFA_from_RE_14-11-2026.jff)

---

## 1. Aim
To specify a Regular Expression $R = (a+b)^*abb$ in JFLAP, convert it systematically into an equivalent Deterministic Finite Automaton (DFA), and verify language recognition.

---

## 2. Regular Expression & Language
- Alphabet: $\Sigma = \{a, b\}$
- Regular Expression:
  $$R = (a+b)^*abb$$
- Language Defined: The set of all strings ending in the specific sequence `abb`.

---

## 3. State Suffix Tracking in Resulting DFA
The converted DFA maintains 4 deterministic states corresponding to the longest matching suffix of the pattern `abb`:
- **$q_0$:** Suffix match $\epsilon$ (or last symbol read was `b` not following `a`).
- **$q_1$:** Last symbol read was `a` (matches prefix `a` of `abb`).
- **$q_2$:** Last symbols read were `ab` (matches prefix `ab` of `abb`).
- **$q_3$:** Last symbols read were `abb` (Full pattern match; **Final Accepting State**).

---

## 4. Transition Table
| State | Tracked Suffix | On Input `a` | On Input `b` | Accepting? |
|:---:|:---:|:---:|:---:|:---:|
| **$q_0$** | $\epsilon$ | $q_1$ | $q_0$ | No |
| **$q_1$** | `a` | $q_1$ | $q_2$ | No |
| **$q_2$** | `ab` | $q_1$ | $q_3$ | No |
| **$q_3$** | `abb` | $q_1$ | $q_0$ | **YES** |

---

## 5. Test Suite
- `abb`: **Accepted**
- `aabb`: **Accepted**
- `babb`: **Accepted**
- `abababb`: **Accepted**
- `ab`: **Rejected**
- `abba`: **Rejected**
- `abbb`: **Rejected**
- `bba`: **Rejected**
