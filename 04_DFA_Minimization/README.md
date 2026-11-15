# Practical 04: DFA Minimization

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Original DFA File:** [`27_Krish_Lalwani_DFA_Original_14-11-2026.jff`](27_Krish_Lalwani_DFA_Original_14-11-2026.jff)  
**Minimized DFA File:** [`27_Krish_Lalwani_DFA_Minimized_14-11-2026.jff`](27_Krish_Lalwani_DFA_Minimized_14-11-2026.jff)

---

## 1. Aim
To minimize a 5-state Deterministic Finite Automaton (DFA) recognizing binary strings ending with `01` using the **Equivalence Partitioning (Myhill-Nerode)** algorithm in JFLAP and obtain the unique minimal state automaton.

---

## 2. Partitioning Algorithm Derivation
Let the set of states be $Q = \{q_0, q_1, q_2, q_3, q_4\}$ where $F = \{q_2, q_4\}$ and non-accepting states $Q \setminus F = \{q_0, q_1, q_3\}$.

### Step 1: 0-Equivalence Partition ($P_0$)
Group accepting and non-accepting states separately:
$$P_0 = \{ \{q_0, q_1, q_3\}, \{q_2, q_4\} \}$$

### Step 2: 1-Equivalence Partition ($P_1$)
Examine transitions on inputs `0` and `1`:
- In group $\{q_0, q_1, q_3\}$:
  - $\delta(q_0, 0) = q_1$; $\delta(q_0, 1) = q_0$
  - $\delta(q_1, 0) = q_1$; $\delta(q_1, 1) = q_2 \in F$
  - $\delta(q_3, 0) = q_1$; $\delta(q_3, 1) = q_4 \in F$
  Notice that $q_0$ goes to a non-final state on `1`, whereas $q_1, q_3$ go to final states on `1`.
  Hence $q_0$ splits out!
  $$P_1 = \{ \{q_0\}, \{q_1, q_3\}, \{q_2, q_4\} \}$$

### Step 3: 2-Equivalence Partition ($P_2$)
- Testing group $\{q_1, q_3\}$:
  - On `0`: both go to $q_1 \in \{q_1, q_3\}$.
  - On `1`: $q_1 \to q_2 \in \{q_2, q_4\}$ and $q_3 \to q_4 \in \{q_2, q_4\}$. Identical!
- Testing group $\{q_2, q_4\}$:
  - On `0`: $q_2 \to q_3 \in \{q_1, q_3\}$ and $q_4 \to q_3 \in \{q_1, q_3\}$.
  - On `1`: both go to $q_0 \in \{q_0\}$. Identical!

Since $P_2 = P_1$, partitioning halts with **3 equivalence classes**:
1. State $[q_0]$ (Start State)
2. State $[q_1, q_3]$
3. State $[q_2, q_4]$ (Final Accepting State)

---

## 3. Minimal DFA Transition Table
| Merged State | Label | Input `0` | Input `1` | Status |
|:---:|:---:|:---:|:---:|:---:|
| **$[q_0]$** | No trailing `0` | $[q_1, q_3]$ | $[q_0]$ | Start |
| **$[q_1, q_3]$** | Trailing `0` | $[q_1, q_3]$ | $[q_2, q_4]$ | Non-final |
| **$[q_2, q_4]$** | Trailing `01` | $[q_1, q_3]$ | $[q_0]$ | **Accepting** |

---

## 4. Verification Suite
The 5-state original DFA and 3-state minimal DFA produce identical acceptance outcomes:
- `01`: Accept
- `001`: Accept
- `1101`: Accept
- `1001`: Accept
- `0`: Reject
- `010`: Reject
- `11`: Reject
- `011`: Reject
