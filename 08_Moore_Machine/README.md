# Practical 08: Moore Machine (Residue Modulo 3)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_Moore_14-11-2026.jff`](27_Krish_Lalwani_Moore_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Moore Machine in JFLAP that continuously outputs the **residue modulo 3** ($0, 1, \text{ or } 2$) of an incoming stream of binary digits read from left to right.

---

## 2. Architecture & Characteristics of Moore Machine
- In a Moore machine, the output symbol depends **solely on the current state** $\lambda : Q \to \Delta$.
- For an input string of length $n$, a Moore machine produces an output string of length $n+1$ because it prints the initial state's output symbol before consuming any input.

---

## 3. Formal Definition (6-Tuple)
$M = (Q, \Sigma, \Delta, \delta, \lambda, q_0)$:
1. $Q = \{q_0, q_1, q_2\}$
2. $\Sigma = \{0, 1\}$
3. $\Delta = \{0, 1, 2\}$
4. Start State $q_0$
5. State Output Function $\lambda$:
   - $\lambda(q_0) = 0$
   - $\lambda(q_1) = 1$
   - $\lambda(q_2) = 2$
6. Transition Function $\delta$:
   - $\delta(q_0, 0) = q_0$; $\delta(q_0, 1) = q_1$
   - $\delta(q_1, 0) = q_2$; $\delta(q_1, 1) = q_0$
   - $\delta(q_2, 0) = q_1$; $\delta(q_2, 1) = q_2$

---

## 4. Test Suite and Execution Traces
| Input Stream | Decimal Equivalent | States Visited | Complete Moore Output (Length $n+1$) | Final Remainder |
|:---:|:---:|:---|:---:|:---:|
| `0` | 0 | $q_0 \to q_0$ | `00` | 0 |
| `1` | 1 | $q_0 \to q_1$ | `01` | 1 |
| `10` | 2 | $q_0 \to q_1 \to q_2$ | `012` | 2 |
| `11` | 3 | $q_0 \to q_1 \to q_0$ | `010` | 0 |
| `100` | 4 | $q_0 \to q_1 \to q_2 \to q_1$ | `0121` | 1 |
| `101` | 5 | $q_0 \to q_1 \to q_2 \to q_2$ | `0122` | 2 |
| `110` | 6 | $q_0 \to q_1 \to q_0 \to q_0$ | `0100` | 0 |
| `111` | 7 | $q_0 \to q_1 \to q_0 \to q_1$ | `0101` | 1 |
