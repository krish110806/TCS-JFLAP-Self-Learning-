# Practical 07: Mealy Machine (Sequence Detector)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_Mealy_14-11-2026.jff`](27_Krish_Lalwani_Mealy_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Mealy Machine in JFLAP that acts as a sequence detector for the binary pattern `101`, emitting an output of `1` immediately upon the completion of the pattern and `0` otherwise (supporting overlapping sequences).

---

## 2. Problem Specification
- Input Alphabet: $\Sigma = \{0, 1\}$
- Output Alphabet: $\Delta = \{0, 1\}$
- Transducer Architecture: Output is associated with the **transition edge** $(\delta(q, \sigma), \lambda(q, \sigma))$.
- Target Pattern: `101`

---

## 3. Formal Definition (6-Tuple)
$M = (Q, \Sigma, \Delta, \delta, \lambda, q_0)$:
1. $Q = \{A, B, C\}$
2. $\Sigma = \{0, 1\}$
3. $\Delta = \{0, 1\}$
4. Start State $q_0 = A$
5. Transition & Output Functions (Combined Table):

| Current State | Input `0` / Output | Next State | Input `1` / Output | Next State | State Significance |
|:---:|:---:|:---:|:---:|:---:|:---|
| **$A$** | `0 / 0` | $A$ | `1 / 0` | $B$ | No prefix matched |
| **$B$** | `0 / 0` | $C$ | `1 / 0` | $B$ | Suffix `1` matched |
| **$C$** | `0 / 0` | $A$ | **`1 / 1`** | $B$ | Suffix `10` matched; on `1` completes `101`! |

Notice that from state $C$ on input `1`, the machine transitions to state $B$ (not $A$) because the terminal `1` of `101` can immediately serve as the initial `1` of the next overlapping `101` sequence!

---

## 4. Test Runs and Output Vectors
| Input Stream | Step-by-Step State Sequence | Generated Output Stream | Overlapping Match Detected |
|:---|:---|:---|:---:|
| `101` | $A \to B \to C \to B$ | `001` | At index 3 |
| `10101` | $A \to B \to C \to B \to C \to B$ | `00101` | At index 3 and index 5 (Overlapping!) |
| `00101` | $A \to A \to A \to B \to C \to B$ | `00001` | At index 5 |
| `1111` | $A \to B \to B \to B \to B$ | `0000` | None |
| `1001` | $A \to B \to C \to A \to B$ | `0000` | None |
