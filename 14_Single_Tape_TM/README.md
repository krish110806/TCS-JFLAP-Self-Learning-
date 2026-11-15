# Practical 14: Single-Tape Turing Machine (Binary Incrementer)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_Single_Tape_TM_14-11-2026.jff`](27_Krish_Lalwani_Single_Tape_TM_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a Single-Tape Deterministic Turing Machine (TM) in JFLAP that computes the **Binary Incrementer** function $f(w) = w + 1$ (arithmetic addition of 1 in binary notation) and halts in an accepting configuration.

---

## 2. Problem Statement
Given an initial tape containing a binary numeral $w \in \{0, 1\}^*$, the machine must compute $w+1$, overwrite the tape with the incremented result, and halt:
$$q_0 w \square^* \vdash^* q_f (w+1) \square^*$$

---

## 3. Operational Logic & Two-Phase Design
Addition of 1 in binary occurs at the least significant bit (LSB) on the far right.
1. **Phase 1: Scanning to LSB (`q_scan`):**
   - Head starts at the leftmost bit.
   - Moves right over all `0`s and `1`s until hitting the blank symbol $\square$.
   - Steps one cell left to place the head squarely on the LSB, switching to `q_carry`.
2. **Phase 2: Leftward Ripple Carry (`q_carry`):**
   - If current bit is `1`: $1 + 1 = 10_2$, so write `0`, retain carry 1, and move left ($L$).
   - If current bit is `0`: $0 + 1 = 1$, write `1`, carry terminates, move right ($R$) and halt in `q_halt`.
   - If current cell is $\square$ (overflow carry, e.g. input was `111`): write `1`, carry terminates, and halt in `q_halt` (resulting in `1000`).

---

## 4. Formal Definition (7-Tuple)
$M = (Q, \Sigma, \Gamma, \delta, q_0, \square, F)$:
1. $Q = \{q_{\text{scan}}, q_{\text{carry}}, q_{\text{halt}}\}$
2. $\Sigma = \{0, 1\}$
3. $\Gamma = \{0, 1, \square\}$
4. Start State $q_0 = q_{\text{scan}}$
5. Blank Symbol $B = \square$ (represented as empty `<read/>` in JFLAP)
6. Final Accepting State $F = \{q_{\text{halt}}\}$
7. Transition function $\delta$:

| Current State | Read Symbol | Write Symbol | Direction | Next State | Action |
|:---:|:---:|:---:|:---:|:---:|:---|
| `q_scan` | `0` | `0` | R | `q_scan` | Skip over bit |
| `q_scan` | `1` | `1` | R | `q_scan` | Skip over bit |
| `q_scan` | $\square$ | $\square$ | L | `q_carry` | Found right boundary; start carry |
| `q_carry` | `1` | `0` | L | `q_carry` | $1+1$: write 0, ripple carry left |
| `q_carry` | `0` | `1` | R | `q_halt` | $0+1$: write 1, carry absorbed |
| `q_carry` | $\square$ | `1` | R | `q_halt` | Overflow bit: write 1 |

---

## 5. Execution Traces
### Trace 1: Input `10` ($2_{10}$) $\implies 10 + 1 = 11$ ($3_{10}$)
$$q_{\text{scan}} 10\square \vdash 1 q_{\text{scan}} 0\square \vdash 10 q_{\text{scan}} \square \vdash 1 q_{\text{carry}} 0 \vdash 11 q_{\text{halt}} \square \quad \text{[HALT]}$$

### Trace 2: Input `11` ($3_{10}$) $\implies 11 + 1 = 100$ ($4_{10}$)
$$q_{\text{scan}} 11\square \vdash 1 q_{\text{scan}} 1\square \vdash 11 q_{\text{scan}} \square \vdash 1 q_{\text{carry}} 1 \vdash q_{\text{carry}} 10 \vdash q_{\text{carry}} \square 00 \vdash 1 q_{\text{halt}} 00 \quad \text{[HALT]}$$
