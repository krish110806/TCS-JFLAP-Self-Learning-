# Practical 15: Multi-Tape Turing Machine (Binary String Duplication)

**Course:** Theory of Computer Science (TCS) – 26CMPC51  
**Student Name:** Krish Lalwani  
**Roll No:** 27  
**Division:** D12A  
**Institution:** Vivekanand Education Society's Institute of Technology (VESIT)  
**Faculty In-Charge:** Mr. Sanjay Mirchandani  
**Primary JFLAP File:** [`27_Krish_Lalwani_Multi_Tape_TM_14-11-2026.jff`](27_Krish_Lalwani_Multi_Tape_TM_14-11-2026.jff)

---

## 1. Aim
To design, implement, and formally analyze a 2-Tape Turing Machine in JFLAP that computes the string copy function $f(w) = ww$ for binary strings over $\Sigma = \{0, 1\}$.

---

## 2. Problem Statement
Let the input string $w \in \{0, 1\}^*$ reside on Tape 1, with Tape 2 initially blank.
The machine must execute in $O(n)$ time to duplicate $w$, ending with $ww$ on Tape 1 and halting in accepting state $q_{\text{halt}}$:
$$(q_0, [w, \epsilon]) \vdash^* (q_{\text{halt}}, [ww, w])$$

---

## 3. Operational Phases (3-Phase Pipeline)
1. **Phase 1: Copy to Auxiliary Tape (`q_copy`):**  
   Read symbol from Tape 1, write identical symbol to Tape 2, advance both heads right ($R$). Continue until Tape 1 encounters blank $\square$.
2. **Phase 2: Rewind Auxiliary Tape (`q_rewind`):**  
   Keep Tape 1 stationary ($S$) at the blank cell immediately following $w$. Move Tape 2 head left ($L$) until the blank before the start of $w$ is reached, then step one cell right ($R$) onto the first character of $w$.
3. **Phase 3: Append onto Tape 1 (`q_append`):**  
   Read character from Tape 2, write it into the blank space of Tape 1, and advance both heads right ($R$).
4. **Phase 4: Halt (`q_halt`):**  
   When Tape 2 hits blank, all of $w$ has been appended. Both heads stop ($S$), and the machine enters the accepting final state $q_{\text{halt}}$. Tape 1 now contains $ww$!

---

## 4. Multi-Tape Transition Table
| State | Tape 1 Read | Tape 1 Write | Tape 1 Move | Tape 2 Read | Tape 2 Write | Tape 2 Move | Next State | Action Description |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---|
| `q_copy` | `0` | `0` | R | $\square$ | `0` | R | `q_copy` | Copy bit `0` to Tape 2 |
| `q_copy` | `1` | `1` | R | $\square$ | `1` | R | `q_copy` | Copy bit `1` to Tape 2 |
| `q_copy` | $\square$ | $\square$ | S | $\square$ | $\square$ | L | `q_rewind` | Tape 1 exhausted; begin rewind |
| `q_rewind` | $\square$ | $\square$ | S | `0` | `0` | L | `q_rewind` | Rewind over `0` on Tape 2 |
| `q_rewind` | $\square$ | $\square$ | S | `1` | `1` | L | `q_rewind` | Rewind over `1` on Tape 2 |
| `q_rewind` | $\square$ | $\square$ | S | $\square$ | $\square$ | R | `q_append` | Reached front of Tape 2; begin append |
| `q_append` | $\square$ | `0` | R | `0` | `0` | R | `q_append` | Append `0` onto Tape 1 |
| `q_append` | $\square$ | `1` | R | `1` | `1` | R | `q_append` | Append `1` onto Tape 1 |
| `q_append` | $\square$ | $\square$ | S | $\square$ | $\square$ | S | `q_halt` | Finished append; HALT in acceptance |

---

## 5. Test Suite Verification
| Input Tape 1 ($w$) | Initial Tape 2 | Final Tape 1 ($ww$) | Final Tape 2 ($w$) | Complexity Steps | Status |
|:---:|:---:|:---:|:---:|:---:|:---:|
| `0` | $\square$ | `00` | `0` | 5 | **Accepted** |
| `1` | $\square$ | `11` | `1` | 5 | **Accepted** |
| `01` | $\square$ | `0101` | `01` | 8 | **Accepted** |
| `10` | $\square$ | `1010` | `10` | 8 | **Accepted** |
| `101` | $\square$ | `101101` | `101` | 11 | **Accepted** |
| `1100` | $\square$ | `11001100` | `1100` | 14 | **Accepted** |
