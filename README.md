# 3-floor-elavator-control-logisim
Combinational 3-floor elevator control system designed with K-map minimization, implemented at both gate-level and IC-level (74153 MUX) in Logisim, and verified with a 100% pass rate across 192 test vectors.
# 3-Floor Elevator Control System (Combinational Logic)

A combinational digital logic design for a 3-floor elevator control system, developed as part of the **EE142 Digital Logic Design** course at Boğaziçi University. The system is designed from scratch using Karnaugh Map simplification and implemented in **Logisim** at both the **Gate-Level** and **IC-Level (74153 Multiplexers)**.

---

## Key Features & Logic Requirements

* **Input Optimization:** Cabin buttons ($B_1, B_2, B_3$) and floor call buttons ($F_1, F_2, F_3$) are combined via OR gates into unified floor call signals ($C_1, C_2, C_3$) to reduce truth table complexity.
* **Nearest Floor & Upward Priority:** Identifies the nearest requested floor; prioritizes upward movement when multiple requests are active simultaneously.
* **Safe Door Operation:** The door output ($DO = 1$) triggers only when the elevator is stationary at a floor with an active call.
* **Dual Implementation:**
  * **Gate-Level:** Sum-of-Products (SoP) implementation minimized via 5-variable Karnaugh Maps utilizing "don't care" conditions.
  * **IC-Level:** Hardware-optimized design using **SN74LS153 Dual 4-to-1 Multiplexers** (with current floor bits $E_1, E_0$ as select lines and Boolean expansion $X + X' = 1$ for missing select variables), alongside 74LS04, 74LS08, and 74LS32 ICs.

---

## System Architecture

* **Inputs:**
  * `E1, E0`: 2-bit current floor position (`00`: Floor 1, `01`: Floor 2, `10`: Floor 3)
  * `B1–B3`, `F1–F3`: Cabin and floor call buttons (combined into `C1, C2, C3`)
  * `D`: Door sensor (treated as don't care for next-state combinational logic)
* **Outputs:**
  * `NF1, NF0`: 2-bit target next floor address
  * `DO`: Door operation signal (`1`: Open, `0`: Closed)

![Gate-Level Circuit](<img width="1048" height="907" alt="image" src="https://github.com/user-attachments/assets/19831429-a42e-416d-8e70-1ed33dbcccf9" />
)
![IC-Level Circuit](<img width="935" height="482" alt="image" src="https://github.com/user-attachments/assets/676062b7-7809-4ff2-a96d-8aed6d6bc4f4" />
)

---

## Verification & Testing

Both the gate-level and IC-level implementations were exhaustively verified using Logisim's **Test Vector** feature:
* **Total Test Cases:** 192 realistic input combinations (`test_vector_for_all.txt`)
* **Result:** **100% pass rate** on both implementations, confirming identical functional behavior and error-free Boolean minimization.

---

## Repository Structure

```text
├── circuit/      # Logisim (.circ) files for gate-level and IC-level designs
├── report/       # Full technical report (PDF & LaTeX source)
├── tests/        # Logisim test vector file (192 combinations) & verification screenshots
└── images/       # High-resolution circuit schematics
