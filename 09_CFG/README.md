# Practical 09: Context-Free Grammar (CFG)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_CFG_14-11-2026.jff`](27_Krish_Lalwani_CFG_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Context-Free Grammar (CFG) in JFLAP that generates the non-regular language $L = \{ a^n b^{2n} \mid n \ge 1 \}$, and verify derivations via parse trees.

---

## 2. Language Definition
Let $\Sigma = \{a, b\}$. The context-free language is defined as:
$$L = \{ a^n b^{2n} \mid n \ge 1 \} = \{ abb, aabbbb, aaabbbbbb, \dots \}$$
Every single `a` must strictly be balanced by exactly **two `b`s**. Since this requires unbounded counting and memory, this language cannot be recognized by any finite automaton (by the Pumping Lemma for Regular Languages) and strictly requires a Context-Free Grammar.

---

## 3. Formal Definition (4-Tuple)
$G = (V, \Sigma, R, S)$:
1. $V = \{S\}$ (Non-terminal variable)
2. $\Sigma = \{a, b\}$ (Terminal alphabet)
3. $S \in V$ (Start symbol)
4. Production rules $R$:
   - $S \to aSbb$ *(Recursive inductive rule: adds one `a` on the left and two `b`s on the right)*
   - $S \to abb$ *(Base case rule: $n = 1$)*

---

## 4. Derivation Examples & Parse Trees
### Example 1: $n = 1 \implies w = abb$
$$S \implies abb$$

### Example 2: $n = 2 \implies w = aabbbb$
$$S \implies aSbb \implies a(abb)bb = aabbbb$$

### Example 3: $n = 3 \implies w = aaabbbbbb$
$$S \implies aSbb \implies a(aSbb)bb \implies aa(abb)bbbb = aaabbbbbb$$

---

## 5. Verification Suite
| String | $n$ | Mathematical Form ($a^n b^{2n}$) | JFLAP Grammar Parser | Status |
|:---:|:---:|:---:|:---:|:---:|
| `abb` | 1 | $a^1 b^2$ | Derived | **Accepted** |
| `aabbbb` | 2 | $a^2 b^4$ | Derived | **Accepted** |
| `aaabbbbbb` | 3 | $a^3 b^6$ | Derived | **Accepted** |
| `ab` | - | Unbalanced ratio (1:1) | Not Derived | **Rejected** |
| `abbb` | - | Unbalanced ratio (1:3) | Not Derived | **Rejected** |
| `aabb` | - | Unbalanced ratio (2:2) | Not Derived | **Rejected** |
| `bba` | - | Invalid order | Not Derived | **Rejected** |
