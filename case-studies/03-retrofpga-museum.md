# Case Study 03 — RetroFPGA Computer Museum: Rebuilding Computing Across Time

> **SystemVerilog · FPGA · digital logic · CPU architecture · simulation · engineering education**
>
> **Source:** [RetroFPGA-Basys3](https://github.com/retrofpga-computer-museum/RetroFPGA-Basys3) · **Museum:** [RetroFPGA Computer Museum](https://github.com/retrofpga-computer-museum) · **Related:** [SAP1-Basys3](https://github.com/johntsaiainow/SAP1-Basys3)

[← Return to the engineering portfolio](../README.md)

## The engineering question

**Can the history of computing be preserved as working, inspectable hardware rather than only as documentation or static exhibits?**

Computer history is often presented as a sequence of machines. Beneath those machines lies a sequence of ideas: clocks, registers, buses, instruction decoding, memory maps, display timing, and the relationship between software and digital logic.

The **RetroFPGA Computer Museum** is an attempt to preserve those ideas through reconstruction. The aim is not to place a historic machine behind glass, but to make its computational principles available for simulation, implementation, experimentation, and teaching.

## The platform and project boundaries

The primary development platform is the **Digilent Basys 3**, based on the **Xilinx Artix-7 XC7A35T** FPGA. The public [RetroFPGA-Basys3](https://github.com/retrofpga-computer-museum/RetroFPGA-Basys3) project uses **SystemVerilog**. The related [SAP1-Basys3](https://github.com/johntsaiainow/SAP1-Basys3) project explores a simple CPU and calculator-oriented applications.

The museum is an **active engineering and educational program**. The presence of an architecture on the roadmap does not mean its CPU core has been completed, synthesized, or demonstrated on hardware.

## Why start with the boot environment?

Before a museum can switch among computing architectures, it needs a common interface for selecting and observing them. The early tutorials therefore build foundational components:

```text
Clock / reset
     |
Button input and debounce
     |
Boot-menu controller ---- Core registry
     |                       |
     +---- VGA rendering ----+
                 |
          Basys 3 top level
```

**Conceptual subsystem view**, not a full netlist.

The early tutorial sequence has addressed reset/clock behavior, VGA timing and synchronization, pixel generation, font ROM, button debouncing, menu control, and top-level integration. The six-architecture menu design names these selectable targets:

| ID | Architecture | Status represented here |
| --- | --- | --- |
| 0 | SAP-1 | Menu target; related standalone CPU work exists |
| 1 | Hack (nand2tetris) | Registered menu target |
| 2 | MOS 6502 | Registered menu target |
| 3 | Z80 | Registered menu target |
| 4 | Motorola 68000 | Registered menu target |
| 5 | DCPU-16 | Registered menu target |

**Important:** A menu entry or registry ID is **not evidence of a complete CPU implementation**.

## Verification as part of the exhibit

An FPGA educational project should make correctness observable. In the documented development work, the menu/controller, VGA renderer, and top-level paths have been exercised with **Icarus Verilog** testbenches, with **Verilator** also used for linting and simulation workflows.

Examples of previously reported local regression results include:

- A six-architecture boot-menu controller simulation reaching `$finish`.
- A VGA renderer test with **14 pixel checks passing**.
- A top-level integration test reporting **PASS**.
- A SAP-1 calculator display-multiplexer test covering input phases, execution dashes, and the final CPU result.

These are **development-session reports**, not an independently reproduced CI run in this portfolio build. For a hiring-manager review, the corresponding source files and commands should be checked in the repository at the referenced revision.

## A concrete design problem: the calculator display

The Basys 3 onboard four-digit seven-segment display is more than decoration. It is a compact way to make CPU state visible while operating a calculator-style SAP-1 application.

The intended display contract is:

| Phase | Intended visible behavior |
| --- | --- |
| 0 — Operand A | Show live switch input |
| 1 — Operand B | Show live switch input |
| 2 — Ready | Show latched Operand B |
| 3 — Execute | Show dashes while busy or before result becomes valid |
| 3 — Complete | Show the CPU OUT result |

A key verification concern is preventing a **previous result** from overwriting a new operand-entry phase. The display-multiplexer logic was revised to prioritize the current phase, then distinguish busy/incomplete execution from a valid result.

This is a small example of a larger engineering idea: **hardware interfaces are part of the system's observable state machine**, and should be tested as such.

## What this case study demonstrates

RetroFPGA brings together several engineering disciplines:

- **RTL design:** sequential logic, state machines, and digital interfaces.
- **Verification:** simulation, regression tests, linting, and reproducible expectations.
- **System integration:** making display, input, core selection, and top-level modules cooperate.
- **Computer architecture:** treating instruction sets and CPUs as structures that can be reconstructed and studied.
- **Education:** converting engineering progress into tutorials that another learner can reproduce.

The long-term vision includes more historical machines and peripherals, but **Basys 3 remains the primary development path**. Other boards and platforms are exploratory, not replacements for the core roadmap.

## Evidence and technical entry points

- **[RetroFPGA-Basys3](https://github.com/retrofpga-computer-museum/RetroFPGA-Basys3):** primary museum RTL and tutorial project.
- **[SAP1-Basys3](https://github.com/johntsaiainow/SAP1-Basys3):** standalone SAP-1 experiments and calculator work.
- **[RetroFPGA Computer Museum organization](https://github.com/retrofpga-computer-museum):** museum mission and related repositories.

## Evidence still to add

To make this case study independently reproducible:

- Pin the exact commit hashes for the boot-menu and display-multiplexer regressions.
- Link the RTL modules and testbench paths directly, with copy-pasteable `iverilog` and `verilator` commands.
- Add a VGA screenshot or short board demonstration video.
- Publish a verified hardware-deployment checklist separately from simulation PASS results.
- Maintain a clear table of **implemented**, **simulated**, **tested on board**, and **planned** architectures.

---

**Engineering principle:** *Rebuild the past. Understand the present. Inspire the future.*

[← Local AI Chatbot](02-local-ai-chatbot.md) · [Portfolio](../README.md)
