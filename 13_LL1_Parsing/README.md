# Practical 13: LL(1) Predictive Parsing

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP Grammar File:** [`27_Krish_Lalwani_LL1_Grammar_14-11-2026.jff`](27_Krish_Lalwani_LL1_Grammar_14-11-2026.jff)

---

## 1. Aim
To design an unambiguous context-free grammar for arithmetic expressions, eliminate left recursion, compute **FIRST** and **FOLLOW** sets, construct the **LL(1) Parsing Table**, and simulate top-down predictive parsing in JFLAP.

---

## 2. Grammar Transformations
Standard arithmetic grammar with left recursion:
$$\begin{aligned}
E &\to E + T \mid T \\
T &\to T * F \mid F \\
F &\to ( E ) \mid i \quad (\text{where } i = \text{identifier / integer})
\end{aligned}$$

Eliminating immediate left recursion using auxiliary variables $A$ (representing $E'$) and $B$ (representing $T'$):
$$\begin{aligned}
E &\to TA \\
A &\to +TA \mid \epsilon \\
T &\to FB \\
B &\to *FB \mid \epsilon \\
F &\to (E) \mid i
\end{aligned}$$

---

## 3. FIRST and FOLLOW Sets
| Non-Terminal Variable | FIRST Set | FOLLOW Set |
|:---:|:---:|:---:|
| **$E$** | $\{ (, i \}$ | $\{ ), \$ \}$ |
| **$A$** ($E'$) | $\{ +, \epsilon \}$ | $\{ ), \$ \}$ |
| **$T$** | $\{ (, i \}$ | $\{ +, ), \$ \}$ |
| **$B$** ($T'$) | $\{ *, \epsilon \}$ | $\{ +, ), \$ \}$ |
| **$F$** | $\{ (, i \}$ | $\{ *, +, ), \$ \}$ |

---

## 4. LL(1) Parsing Table
| Variable | Terminal `i` | Terminal `+` | Terminal `*` | Terminal `(` | Terminal `)` | Endmarker `$` |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **$E$** | $E \to TA$ | | | $E \to TA$ | | |
| **$A$** | | $A \to +TA$ | | | $A \to \epsilon$ | $A \to \epsilon$ |
| **$T$** | $T \to FB$ | | | $T \to FB$ | | |
| **$B$** | | $B \to \epsilon$ | $B \to *FB$ | | $B \to \epsilon$ | $B \to \epsilon$ |
| **$F$** | $F \to i$ | | | $F \to (E)$ | | |

*Notice: Each cell contains at most one production rule; hence there are **no FIRST/FOLLOW or FIRST/FIRST conflicts**, proving the grammar is strictly LL(1)!*

---

## 5. Parser Stack Simulation for `i+i*i$`
| Step | Parser Stack | Input Buffer | Production Applied | Action |
|:---:|:---|:---|:---:|:---|
| 1 | `$E` | `i+i*i$` | $E \to TA$ | Expand |
| 2 | `$AT` | `i+i*i$` | $T \to FB$ | Expand |
| 3 | `$ABF` | `i+i*i$` | $F \to i$ | Expand |
| 4 | `$ABi` | `i+i*i$` | - | Match terminal `i` |
| 5 | `$AB` | `+i*i$` | $B \to \epsilon$ | Pop $\epsilon$ |
| 6 | `$A` | `+i*i$` | $A \to +TA$ | Expand |
| 7 | `$AT+` | `+i*i$` | - | Match terminal `+` |
| 8 | `$AT` | `i*i$` | $T \to FB$ | Expand |
| 9 | `$ABF` | `i*i$` | $F \to i$ | Match terminal `i` |
| 10 | `$AB` | `*i$` | $B \to *FB$ | Expand |
| 11 | `$ABF*` | `*i$` | - | Match terminal `*` |
| 12 | `$ABF` | `i$` | $F \to i$ | Match terminal `i` |
| 13 | `$AB` | `$` | $B \to \epsilon$ | Pop $\epsilon$ |
| 14 | `$A` | `$` | $A \to \epsilon$ | Pop $\epsilon$ |
| 15 | `$` | `$` | - | **ACCEPT (Parse Complete)** |
