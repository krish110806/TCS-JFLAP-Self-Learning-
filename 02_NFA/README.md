# Practical 02: Non-Deterministic Finite Automata (NFA)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_NFA_14-11-2026.jff`](27_Krish_Lalwani_NFA_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Non-Deterministic Finite Automaton (NFA) in JFLAP that recognizes binary strings containing the substring `101`.

---

## 2. Problem / Language Statement
Let the input alphabet be $\Sigma = \{0, 1\}$.  
The language $L$ is formally defined as:
$$L = \{ w \in \{0, 1\}^* \mid w \text{ contains the substring } 101 \} = (0+1)^*101(0+1)^*$$

---

## 3. Formal Definition (5-Tuple)
The NFA is defined by $M = (Q, \Sigma, \delta, q_0, F)$:
1. $Q = \{ q_0, q_1, q_2, q_3 \}$
2. $\Sigma = \{ 0, 1 \}$
3. $q_0 \in Q$ (Start State)
4. $F = \{ q_3 \}$ (Accepting State)
5. $\delta : Q \times \Sigma \to 2^Q$ defined by:
   - $\delta(q_0, 0) = \{ q_0 \}$
   - $\delta(q_0, 1) = \{ q_0, q_1 \}$ *(Non-deterministic decision branch)*
   - $\delta(q_1, 0) = \{ q_2 \}$
   - $\delta(q_1, 1) = \emptyset$
   - $\delta(q_2, 0) = \emptyset$
   - $\delta(q_2, 1) = \{ q_3 \}$
   - $\delta(q_3, 0) = \{ q_3 \}$
   - $\delta(q_3, 1) = \{ q_3 \}$

---

## 4. Non-Deterministic Branching & Design Explanation
- **State $q_0$:** Acts as an arbitrary prefix consumer. When seeing a `1`, it can either remain in $q_0$ (treating `1` as part of the prefix) or non-deterministically guess that this `1` is the start of the target pattern `101`.
- **States $q_1, q_2$:** Check if the subsequent symbols match `0` and `1`.
- **State $q_3$:** Once reached, the string is guaranteed to contain `101`. Any subsequent suffix symbols keep the machine in accepting state $q_3$.

---

## 5. Transition Table
| State | Input `0` | Input `1` | Functional Role |
|:---:|:---:|:---:|:---|
| **$q_0$** | $\{q_0\}$ | $\{q_0, q_1\}$ | Initial loop + non-deterministic branch |
| **$q_1$** | $\{q_2\}$ | $\emptyset$ | Verified first `1` |
| **$q_2$** | $\emptyset$ | $\{q_3\}$ | Verified `10` |
| **$q_3$** | $\{q_3\}$ | $\{q_3\}$ | Final accepting sink |

---

## 6. Test Suite & Verification
| Input String | Target Substring Present? | Set of Reached Final States | Acceptance Status |
|:---:|:---:|:---:|:---:|
| `101` | Yes | $\{q_0, q_3\}$ | **Accepted** |
| `00101` | Yes | $\{q_0, q_3\}$ | **Accepted** |
| `11010` | Yes | $\{q_0, q_3\}$ | **Accepted** |
| `010110` | Yes | $\{q_0, q_3\}$ | **Accepted** |
| `111000` | No | $\{q_0\}$ | **Rejected** |
| `0000` | No | $\{q_0\}$ | **Rejected** |
| `1001` | No | $\{q_0\}$ | **Rejected** |
| `01001` | No | $\{q_0\}$ | **Rejected** |
