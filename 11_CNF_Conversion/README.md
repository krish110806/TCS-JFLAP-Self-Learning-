# Practical 11: Chomsky Normal Form (CNF) Transformation

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Original CFG File:** [`27_Krish_Lalwani_CFG_Original_14-11-2026.jff`](27_Krish_Lalwani_CFG_Original_14-11-2026.jff)  
**CNF Converted File:** [`27_Krish_Lalwani_CNF_Converted_14-11-2026.jff`](27_Krish_Lalwani_CNF_Converted_14-11-2026.jff)

---

## 1. Aim
To systematically convert a given Context-Free Grammar generating $L = \{ a^n b^n \mid n \ge 1 \}$ into **Chomsky Normal Form (CNF)** in JFLAP through the formal reduction pipeline.

---

## 2. CNF Formal Requirements
A Context-Free Grammar is in Chomsky Normal Form if every production is strictly of one of the two forms:
1. $A \to BC$ (where $A, B, C$ are non-terminal variables and $B, C \neq S$)
2. $A \to a$ (where $A$ is a variable and $a$ is a single terminal)

---

## 3. Step-by-Step Conversion Algorithm
**Initial Grammar:**
- $S \to aSb \mid ab$

### Step 1: Eliminate $\epsilon$-productions
There are no null productions ($A \to \epsilon$) since $n \ge 1$.

### Step 2: Eliminate Unit Productions
There are no unit productions ($A \to B$) in the grammar.

### Step 3: Eliminate Useless / Inaccessible Symbols
Both productions generate valid terminal strings; all symbols are generating and reachable.

### Step 4: Isolate Terminals in Composite Bodies
Introduce new non-terminals for terminal symbols:
- $A \to a$
- $B \to b$

Substituting $A$ and $B$ into the original rules gives:
- $S \to ASB \mid AB$

### Step 5: Binarize Productions of Length $> 2$
The body $ASB$ has length 3. We introduce a new non-terminal variable $X$:
- $X \to SB$
- $S \to AX$

### Final CNF Grammar:
$$\begin{aligned}
S &\to AX \mid AB \\
X &\to SB \\
A &\to a \\
B &\to b
\end{aligned}$$

---

## 4. Verification of Equivalency
String `aabb` ($n=2$):
- **Original CFG:** $S \implies aSb \implies a(ab)b = aabb$
- **CNF Grammar:** $S \implies AX \implies aX \implies aSB \implies a(AB)B \implies a(ab)B \implies a(ab)b = aabb$
Both grammars generate the identical language $L = \{ a^n b^n \mid n \ge 1 \}$.
