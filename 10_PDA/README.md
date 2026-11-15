# Practical 10: Deterministic Pushdown Automaton (PDA) for $w c w^R$

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_PDA_14-11-2026.jff`](27_Krish_Lalwani_PDA_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Deterministic Pushdown Automaton (DPDA) in JFLAP that recognizes the marked palindrome language $L = \{ w c w^R \mid w \in \{a, b\}^* \}$ using a two-phase push-match stack architecture and verify acceptance by final state.

---

## 2. Problem / Language Statement
Let the input alphabet be $\Sigma = \{a, b, c\}$.  
The language is formally specified as:
$$L = \{ w c w^R \mid w \in \{a, b\}^* \}$$
where:
- $w$ is any arbitrary string over $\{a, b\}^*$.
- $w^R$ denotes the reversal of $w$.
- The symbol `c` acts as a unique center marker separating the prefix from its reflection.
- For $w = \epsilon$, the minimal valid string is `c`.

Because the center is explicitly marked by `c`, the machine does not require non-deterministic guessing and operates as a **Deterministic Context-Free Language (DCFL)** recognizer.

---

## 3. Formal Definition (7-Tuple)
The DPDA is formally specified by $M = (Q, \Sigma, \Gamma, \delta, q_0, Z, F)$:
1. **$Q = \{q_0, q_1, q_2\}$ (Set of States):**
   - $q_0$: Push phase (reads and pushes symbols of $w$ onto stack).
   - $q_1$: Match phase (compares remaining input with popped stack symbols).
   - $q_2$: Final accepting state (stack exhausted and input completely consumed).
2. **$\Sigma = \{a, b, c\}$** (Input Alphabet)
3. **$\Gamma = \{a, b, Z\}$** (Stack Alphabet, where $Z$ is bottom-of-stack marker)
4. **$q_0 \in Q$** (Start State)
5. **$Z \in \Gamma$** (Initial Stack Symbol)
6. **$F = \{q_2\}$** (Accepting State)
7. **$\delta$** (Transition Function):

| State | Input | Stack Pop | Next State | Stack Push | Operational Semantics |
|:---:|:---:|:---:|:---:|:---:|:---|
| $q_0$ | `a` | $Z$ | $q_0$ | $aZ$ | Push first `a` |
| $q_0$ | `b` | $Z$ | $q_0$ | $bZ$ | Push first `b` |
| $q_0$ | `a` | $a$ | $q_0$ | $aa$ | Push `a` over `a` |
| $q_0$ | `b` | $a$ | $q_0$ | $ba$ | Push `b` over `a` |
| $q_0$ | `a` | $b$ | $q_0$ | $ab$ | Push `a` over `b` |
| $q_0$ | `b` | $b$ | $q_0$ | $bb$ | Push `b` over `b` |
| $q_0$ | `c` | $Z$ | $q_1$ | $Z$ | Center marker seen ($w = \epsilon$), switch to match phase |
| $q_0$ | `c` | $a$ | $q_1$ | $a$ | Center marker seen, preserve stack top `a`, switch to $q_1$ |
| $q_0$ | `c` | $b$ | $q_1$ | $b$ | Center marker seen, preserve stack top `b`, switch to $q_1$ |
| $q_1$ | `a` | $a$ | $q_1$ | $\epsilon$ | Match `a`: Pop from stack |
| $q_1$ | `b` | $b$ | $q_1$ | $\epsilon$ | Match `b`: Pop from stack |
| $q_1$ | $\epsilon$ | $Z$ | $q_2$ | $Z$ | Input finished and bottom marker exposed: Accept! |

---

## 4. Stack Reversal Property (LIFO)
When pushing string $w = c_1 c_2 \dots c_k$ onto the stack, the stack stores symbols in top-down order $[c_k, c_{k-1}, \dots, c_1, Z]$. Thus, as symbols are popped in Phase 2, they naturally emerge in reverse order $w^R$.

---

## 5. Instantaneous Description (ID) Trace for `abcba`
$$(q_0, abcba, Z) \vdash (q_0, bcba, aZ) \vdash (q_0, cba, baZ) \vdash (q_1, ba, baZ) \vdash (q_1, a, aZ) \vdash (q_1, \epsilon, Z) \vdash (q_2, \epsilon, Z) \quad \text{[ACCEPTED]}$$

---

## 6. Comprehensive Test Suite
| Test String | $w$ | $w^R$ | Trace Sequence | Outcome |
|:---:|:---:|:---:|:---|:---:|
| `c` | $\epsilon$ | $\epsilon$ | $(q_0, c, Z) \to (q_1, \epsilon, Z) \to (q_2, \epsilon, Z)$ | **Accepted** |
| `aca` | `a` | `a` | Push `a` $\to$ read `c` $\to$ pop `a` $\to$ reach $q_2$ | **Accepted** |
| `bcb` | `b` | `b` | Push `b` $\to$ read `c` $\to$ pop `b` $\to$ reach $q_2$ | **Accepted** |
| `abcba` | `ab` | `ba` | Push `ab` $\to$ read `c` $\to$ pop `b, a` $\to$ reach $q_2$ | **Accepted** |
| `abbcbba` | `abb` | `bba` | Push `abb` $\to$ read `c` $\to$ pop `b, b, a` $\to$ reach $q_2$ | **Accepted** |
| `ab` | No `c` marker | - | Stuck in $q_0$ (no accepting transition) | **Rejected** |
| `abcca` | `ab` | `ca` | Mismatch at stack top during match | **Rejected** |
| `abcb` | `ab` | `b` | Premature input termination (stack has `aZ`) | **Rejected** |
| `abcbaa` | `ab` | `baa` | Input left over when stack empty | **Rejected** |
