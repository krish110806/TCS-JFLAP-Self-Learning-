# Practical 12: Cocke-Younger-Kasami (CYK) Parsing Algorithm

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP Grammar File:** [`27_Krish_Lalwani_CYK_14-11-2026.jff`](27_Krish_Lalwani_CYK_14-11-2026.jff)

---

## 1. Aim
To execute and formally demonstrate membership verification using the **Cocke-Younger-Kasami (CYK) Dynamic Programming Parsing Algorithm** in JFLAP for strings $w = aabb \in L$ and $w = abab \notin L$.

---

## 2. CNF Grammar Formulation
$$\begin{aligned}
S &\to AX \mid AB \\
X &\to SB \\
A &\to a \\
B &\to b
\end{aligned}$$

---

## 3. CYK Algorithm Formulation
For an input string $w = w_1 w_2 \dots w_n$ of length $n$:
1. **Base Case (Substrings of length 1):**  
   $$V[i, 1] = \{ V \mid V \to w_i \in R \}$$
2. **Recursive Step (Substrings of length $j > 1$ starting at $i$):**  
   $$V[i, j] = \bigcup_{k=1}^{j-1} \{ V \mid V \to YZ \in R, \text{ where } Y \in V[i, k] \text{ and } Z \in V[i+k, j-k] \}$$
3. **Acceptance Criterion:**  
   $w \in L(G) \iff S \in V[1, n]$.

---

## 4. Execution Trace: Parsing $w = aabb$ ($n=4$)
Let $w_1 = a, w_2 = a, w_3 = b, w_4 = b$.

### Row 1 (Length 1):
- $V[1, 1] = \{A\}$ (since $A \to a$)
- $V[2, 1] = \{A\}$ (since $A \to a$)
- $V[3, 1] = \{B\}$ (since $B \to b$)
- $V[4, 1] = \{B\}$ (since $B \to b$)

### Row 2 (Length 2):
- $V[1, 2]: V[1,1] \times V[2,1] = \{A\} \times \{A\} = \{AA\} \implies \emptyset$
- $V[2, 2]: V[2,1] \times V[3,1] = \{A\} \times \{B\} = \{AB\} \implies \{S\}$ (since $S \to AB$)
- $V[3, 2]: V[3,1] \times V[4,1] = \{B\} \times \{B\} = \{BB\} \implies \emptyset$

### Row 3 (Length 3):
- $V[1, 3]: (V[1,1] \times V[2,2]) \cup (V[1,2] \times V[3,1]) = (\{A\} \times \{S\}) \cup (\emptyset \times \{B\}) = \{AS\} \implies \emptyset$
- $V[2, 3]: (V[2,1] \times V[3,2]) \cup (V[2,2] \times V[4,1]) = (\{A\} \times \emptyset) \cup (\{S\} \times \{B\}) = \{SB\} \implies \{X\}$ (since $X \to SB$)

### Row 4 (Length 4 - Top of Pyramid):
- $V[1, 4]:$
  - $k=1: V[1,1] \times V[2,3] = \{A\} \times \{X\} = \{AX\} \implies \{S\}$ (since $S \to AX$)
  - $k=2: V[1,2] \times V[3,2] = \emptyset \times \emptyset = \emptyset$
  - $k=3: V[1,3] \times V[4,1] = \emptyset \times \{B\} = \emptyset$
  $$\implies V[1, 4] = \{S\}$$

**Conclusion:** Since $S \in V[1, 4]$, the string `aabb` is **ACCEPTED**!

---

## 5. CYK Triangular Table
| $j$ (len) \ $i$ (pos) | $i=1$ ($a$) | $i=2$ ($a$) | $i=3$ ($b$) | $i=4$ ($b$) |
|:---:|:---:|:---:|:---:|:---:|
| **$j=4$** | **$\{S\}$** | | | |
| **$j=3$** | $\emptyset$ | $\{X\}$ | | |
| **$j=2$** | $\emptyset$ | $\{S\}$ | $\emptyset$ | |
| **$j=1$** | $\{A\}$ | $\{A\}$ | $\{B\}$ | $\{B\}$ |
