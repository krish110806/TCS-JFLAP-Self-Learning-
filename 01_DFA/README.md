# Practical 01: Deterministic Finite Automaton (DFA)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_DFA_14-11-2026.jff`](27_Krish_Lalwani_DFA_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Deterministic Finite Automaton (DFA) in JFLAP that recognizes the language of binary strings whose decimal value is divisible by 3.

---

## 2. Problem / Language Statement
Let the input alphabet be $\Sigma = \{0, 1\}$.  
The language $L$ is formally specified as:
$$L = \{ w \in \{0, 1\}^* \mid \text{val}_2(w) \equiv 0 \pmod 3 \}$$
where $\text{val}_2(w)$ represents the standard numerical integer value represented by binary numeral $w$ processed from left to right (most significant bit to least significant bit).

---

## 3. Mathematical Recurrence & State Logic
When reading a new incoming bit $b \in \{0, 1\}$ from left to right, the new numerical value is given by:
$$\text{val}_{\text{new}} = 2 \times \text{val}_{\text{old}} + b$$
Taking this equation modulo 3:
$$\text{rem}_{\text{new}} = (2 \times \text{rem}_{\text{old}} + b) \pmod 3$$

Hence, only 3 distinct states are required corresponding to the remainder classes $\mathbb{Z}_3 = \{0, 1, 2\}$:
- **$q_0$:** Remainder $0$ (Accepting / Initial State).
- **$q_1$:** Remainder $1$.
- **$q_2$:** Remainder $2$.

---

## 4. Formal Definition (5-Tuple)
The automaton is formally defined by $M = (Q, \Sigma, \delta, q_0, F)$:
1. $Q = \{ q_0, q_1, q_2 \}$
2. $\Sigma = \{ 0, 1 \}$
3. $q_0 \in Q$ (Start State)
4. $F = \{ q_0 \}$ (Accepting State)
5. Transition function $\delta : Q \times \Sigma \to Q$ defined as:

| Current State | Input `0` | Input `1` | Transition Reason |
|:---:|:---:|:---:|:---|
| **$q_0$** (Rem 0) | $q_0$ | $q_1$ | $(2 \times 0 + 0) \pmod 3 = 0$; $(2 \times 0 + 1) \pmod 3 = 1$ |
| **$q_1$** (Rem 1) | $q_2$ | $q_0$ | $(2 \times 1 + 0) \pmod 3 = 2$; $(2 \times 1 + 1) \pmod 3 = 0$ |
| **$q_2$** (Rem 2) | $q_1$ | $q_2$ | $(2 \times 2 + 0) \pmod 3 = 1$; $(2 \times 2 + 1) \pmod 3 = 2$ |

---

## 5. Test Suite & Trace Verification

### Positive Test Cases (Accepted, $\text{val}_2(w) \equiv 0 \pmod 3$):
| Test String | Decimal Value | State Trace Sequence | End State | Status |
|:---:|:---:|:---|:---:|:---:|
| `0` | 0 | $q_0 \xrightarrow{0} q_0$ | $q_0$ | **Accepted** |
| `11` | 3 | $q_0 \xrightarrow{1} q_1 \xrightarrow{1} q_0$ | $q_0$ | **Accepted** |
| `110` | 6 | $q_0 \xrightarrow{1} q_1 \xrightarrow{1} q_0 \xrightarrow{0} q_0$ | $q_0$ | **Accepted** |
| `1001` | 9 | $q_0 \xrightarrow{1} q_1 \xrightarrow{0} q_2 \xrightarrow{0} q_1 \xrightarrow{1} q_0$ | $q_0$ | **Accepted** |
| `1100` | 12 | $q_0 \xrightarrow{1} q_1 \xrightarrow{1} q_0 \xrightarrow{0} q_0 \xrightarrow{0} q_0$ | $q_0$ | **Accepted** |
| `1111` | 15 | $q_0 \xrightarrow{1} q_1 \xrightarrow{1} q_0 \xrightarrow{1} q_1 \xrightarrow{1} q_0$ | $q_0$ | **Accepted** |

### Negative Test Cases (Rejected, $\text{val}_2(w) \not\equiv 0 \pmod 3$):
| Test String | Decimal Value | Remainder | End State | Status |
|:---:|:---:|:---:|:---:|:---:|
| `1` | 1 | 1 | $q_1$ | **Rejected** |
| `10` | 2 | 2 | $q_2$ | **Rejected** |
| `100` | 4 | 1 | $q_1$ | **Rejected** |
| `101` | 5 | 2 | $q_2$ | **Rejected** |
| `111` | 7 | 1 | $q_1$ | **Rejected** |
| `1010` | 10 | 1 | $q_1$ | **Rejected** |

---

## 6. How to Open and Execute in JFLAP
1. Launch JFLAP (`java -jar JFLAP.jar`).
2. Select **File -> Open** and load `27_Krish_Lalwani_DFA_14-11-2026.jff`.
3. Navigate to **Input -> Multiple Run**.
4. Enter the test strings above and click **Run Inputs** to verify complete correctness.
