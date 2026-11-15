# Practical 03: NFA to DFA Conversion

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Source NFA File:** [`27_Krish_Lalwani_NFA_Source_14-11-2026.jff`](27_Krish_Lalwani_NFA_Source_14-11-2026.jff)  
**Converted DFA File:** [`27_Krish_Lalwani_DFA_Converted_14-11-2026.jff`](27_Krish_Lalwani_DFA_Converted_14-11-2026.jff)

---

## 1. Aim
To convert a given Non-Deterministic Finite Automaton (NFA) recognizing strings ending with `ab` into an equivalent Deterministic Finite Automaton (DFA) using the standard **Subset (Powerset) Construction Algorithm** and verify both in JFLAP.

---

## 2. Problem Statement
Let $\Sigma = \{a, b\}$. The target language is:
$$L = \{ w \in \{a, b\}^* \mid w \text{ ends with } ab \} = (a+b)^*ab$$

---

## 3. Step-by-Step Subset Construction Method
Let the NFA states be $Q_{NFA} = \{ q_0, q_1, q_2 \}$.

1. **Initial DFA State $A$:**
   $$A = [q_0]$$
   - On input `a`: $\delta(q_0, a) = \{ q_0, q_1 \} = B$
   - On input `b`: $\delta(q_0, b) = \{ q_0 \} = A$

2. **DFA State $B = [q_0, q_1]$:**
   - On input `a`: $\delta(q_0, a) \cup \delta(q_1, a) = \{ q_0, q_1 \} \cup \emptyset = [q_0, q_1] = B$
   - On input `b`: $\delta(q_0, b) \cup \delta(q_1, b) = \{ q_0 \} \cup \{ q_2 \} = [q_0, q_2] = C$

3. **DFA State $C = [q_0, q_2]$:**
   *(Since $q_2 \in C$ and $q_2 \in F_{NFA}$, state $C$ is an accepting state!)*
   - On input `a`: $\delta(q_0, a) \cup \delta(q_2, a) = \{ q_0, q_1 \} \cup \emptyset = [q_0, q_1] = B$
   - On input `b`: $\delta(q_0, b) \cup \delta(q_2, b) = \{ q_0 \} \cup \emptyset = [q_0] = A$

---

## 4. Subset Transition Table
| DFA State Name | Composite NFA Subset | Input `a` | Input `b` | Accepting State? |
|:---:|:---:|:---:|:---:|:---:|
| **$A$** | $[q_0]$ | $B$ | $A$ | No |
| **$B$** | $[q_0, q_1]$ | $B$ | $C$ | No |
| **$C$** | $[q_0, q_2]$ | $B$ | $A$ | **YES (Final)** |

---

## 5. Dual Verification on Both Models
Both the source NFA and the converted DFA were subjected to identical test inputs in JFLAP:

| Test String | Ends in `ab`? | NFA Result | Converted DFA Result | Verification Match |
|:---:|:---:|:---:|:---:|:---:|
| `ab` | Yes | Accept | Accept | **MATCH** |
| `aab` | Yes | Accept | Accept | **MATCH** |
| `bab` | Yes | Accept | Accept | **MATCH** |
| `abbab` | Yes | Accept | Accept | **MATCH** |
| `a` | No | Reject | Reject | **MATCH** |
| `aba` | No | Reject | Reject | **MATCH** |
| `abb` | No | Reject | Reject | **MATCH** |
| `b` | No | Reject | Reject | **MATCH** |
