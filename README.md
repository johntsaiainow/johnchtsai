<div align="center">

# I Engineer the Present. Explore the Future. Rebuild the Past.

### John Cheng-Hung Tsai

**Electrical & Embedded Systems Engineer · Firmware · Linux · Hardware–Software Integration**

*Three flagship projects. Three dimensions of engineering. One lifelong pursuit.*

[Explore Applied Engineering](https://github.com/johntsaiainow) · [Enter the FPGA Museum](https://github.com/retrofpga-computer-museum) · [Explore Engineering Education](https://github.com/johnschoolworks)

</div>

---

## Engineering Is More Than a Job Title

A computer begins long before a screen lights up. It begins with electrons, circuits, timing, and logic. It becomes firmware, a network, a machine, and eventually a tool that someone trusts with a real task.

I have spent more than twenty years working across those boundaries: IT infrastructure, consumer electronics, manufacturing, industrial control, embedded firmware, and systems integration. Along the way, I learned that the most interesting engineering problems rarely respect the lines between disciplines.

A sensor does not care whether its failure belongs to hardware or software. A production machine does not care which team owns the bug. A computer architecture cannot be understood by reading an instruction set alone.

**To build reliable systems, I believe an engineer must be willing to follow a problem all the way down—and all the way through.**

My GitHub is a record of that pursuit. If you have only a few minutes, start with three projects. Each has a dedicated engineering case study: the context, design questions, evidence, and the work still to be verified.

---

# I. DaVinci — Engineering the Physical World

### *When software must answer to reality.*

[**Read the DaVinci Engineering Case Study →**](case-studies/01-davinci.md)  
[View source code](https://github.com/johntsaiainow/davinciarduino2025)

In an industrial control system, code does not stay inside a computer. It becomes the action of a pump, the state of a valve, a response to a sensor, or a decision made under imperfect physical conditions.

The **DaVinci 20 Plus beverage dispensing controller** represents the part of my engineering career where hardware, firmware, and the practical realities of a manufactured product meet.

Its public repository provides a starting point for examining embedded C++ controller firmware. The wider engineering questions are the ones I care about most: How do we connect software decisions to physical behavior? How do we diagnose failures that cross electrical and software boundaries? How do we make a system understandable enough to test, maintain, and improve?

**Explore the surrounding engineering work:** [ESP32 Communication Module PCB](https://github.com/johntsaiainow/ESP32-Communication-Module-PCB) · [AquaMesh ESP32-to-STM32 Bootloader Bridge](https://github.com/johntsaiainow/AquaMesh-Basic-Bootloader-Bridge) · [KiCad PCB Collection](https://github.com/johntsaiainow/small-pcb-design-collection)

**Engineering lens:** Embedded C/C++ · Control systems · Device interfaces · Hardware/firmware debugging · Product integration

> **My first principle:** A design is not finished when the code compiles. It must make sense in the physical world.

---

# II. Local AI Chatbot — Engineering the Next Interface

### *When small machines begin to listen, respond, and collaborate.*

[**Read the Local AI Chatbot Engineering Case Study →**](case-studies/02-local-ai-chatbot.md)  
[View source code](https://github.com/johntsaiainow/ESP32-Local-Ai-Chatbot)

For decades, embedded devices have measured, controlled, and reported. The next challenge is to make interaction with those devices more natural—without losing the engineering discipline that makes them dependable.

The **ESP32 Local AI Chatbot** explores the intersection of microcontrollers, connectivity, voice-oriented interaction, and AI software. It is not merely an experiment in attaching a model to a board. It is an exploration of the entire path between a human request and an embedded system's response.

That path raises practical questions: How should hardware and software divide responsibilities? What happens when connectivity becomes unreliable? How do we design, test, and debug an interaction that crosses device firmware and higher-level services?

The project also extends into physical design through the [AI-Now Local ESP32 Chatbots PCB family](https://github.com/johntsaiainow/AI-Now-Local-ESP32-Chatbots-PCB).

**Engineering lens:** ESP32 · Embedded integration · Python · Connectivity · AI-enabled device architecture · PCB development

> **My second principle:** The future of AI is not only in data centers. It is also at the edge, where computation meets the everyday world.

---

# III. RetroFPGA Computer Museum — Engineering Across Time

### *Rebuild the past. Understand the present. Inspire the future.*

[**Read the RetroFPGA Engineering Case Study →**](case-studies/03-retrofpga-museum.md)  
[Enter the museum](https://github.com/retrofpga-computer-museum)

A modern computer hides an extraordinary history beneath its abstractions: gates, registers, buses, clocks, memory, instruction sets, and the ingenuity of engineers who made every layer possible.

I created the **RetroFPGA Computer Museum** to explore a different kind of preservation. Instead of keeping historic computing concepts only in books or behind glass, I want to reconstruct them as working, inspectable digital systems that students and engineers can study.

The [**RetroFPGA-Basys3**](https://github.com/retrofpga-computer-museum/RetroFPGA-Basys3) project uses SystemVerilog and the Digilent Basys 3 FPGA platform as a foundation for digital logic, video output, control interfaces, and a growing collection of computer architectures. My separate [**SAP1-Basys3**](https://github.com/johntsaiainow/SAP1-Basys3) repository explores a simple computer architecture and calculator-oriented applications.

**This is an evolving engineering and educational effort, not a claim that every planned computer has already been implemented.** The repositories and their tests are the source of truth for what currently works.

**Engineering lens:** SystemVerilog · FPGA · Digital logic · CPU architecture · Simulation and regression testing · Engineering education

> **My third principle:** The best way to preserve engineering knowledge is to make it possible for the next generation to rebuild it.

---

## Three Projects. One Engineering Philosophy.

**DaVinci asks:** Can I make software work reliably with real hardware?

**Local AI Chatbot asks:** Can I connect that hardware to a new generation of intelligent interfaces?

**RetroFPGA asks:** Do I understand computing deeply enough to reconstruct and teach its foundations?

These are not three unrelated hobbies. They are three views of the same discipline—**engineering the present, exploring what comes next, and keeping the knowledge of the past alive.**

---

## For Engineering Managers and Technical Interviewers

I am interested in engineering roles where firmware, electronics, testing, Linux, and system integration intersect—especially where reliability and clear technical reasoning matter.

If you are evaluating my work for a specific role, here is a faster route into the code:

| Your engineering challenge | Where to start |
| --- | --- |
| Embedded firmware and physical control | [DaVinci](https://github.com/johntsaiainow/davinciarduino2025) · [AquaMesh Bootloader Bridge](https://github.com/johntsaiainow/AquaMesh-Basic-Bootloader-Bridge) |
| Hardware/software test and validation | [DaVinci](https://github.com/johntsaiainow/davinciarduino2025) · [RetroFPGA-Basys3](https://github.com/retrofpga-computer-museum/RetroFPGA-Basys3) |
| Connected embedded devices and AI | [ESP32 Local AI Chatbot](https://github.com/johntsaiainow/ESP32-Local-Ai-Chatbot) · [AI Chatbot PCB](https://github.com/johntsaiainow/AI-Now-Local-ESP32-Chatbots-PCB) |
| FPGA and computer architecture | [RetroFPGA-Basys3](https://github.com/retrofpga-computer-museum/RetroFPGA-Basys3) · [SAP1-Basys3](https://github.com/johntsaiainow/SAP1-Basys3) |
| Embedded Linux and development tools | [Raspberry Pi Agent MP3 Player](https://github.com/johntsaiainow/pi-agent-mp3-player) · [eZ8 Linux Native Toolchain](https://github.com/johnschoolworks/ez8-linux-native) |

*Project links show public work, not claims of proprietary platform expertise, production certifications, or unverified performance metrics. Implementation maturity varies by repository.*

---

## Beyond the Three Pillars: Engineering as a Shared Inheritance

My career has also been a continuing education. I study, experiment, document, and publish because I believe knowledge grows more valuable when someone else can learn from it.

That commitment appears in the [Mt. SAC Electronics 74 materials](https://github.com/johntsaiainow/MtSAC-Electronics-74), the [Berkeley Scheme interpreter project](https://github.com/johnschoolworks/berkeley-scheme), and [SOSCSRPG MonoGame](https://github.com/johnschoolworks/SOSCSRPGMonoGame).

These projects are not substitutes for professional engineering experience. They are evidence of something I intend to keep doing throughout my career: learning in public and leaving useful work behind.

### Four Doors Into My GitHub

- **[Applied Engineering — johntsaiainow](https://github.com/johntsaiainow)** — Embedded systems, electronics, Linux, AI devices, and practical engineering tools.
- **[RetroFPGA Computer Museum](https://github.com/retrofpga-computer-museum)** — FPGA-based reconstruction, computer architecture, and computing history.
- **[John Schoolworks](https://github.com/johnschoolworks)** · **[Repository Index](https://github.com/orgs/johnschoolworks/repositories)** — Interpreters, software development, and educational experiments.
- **[This Professional Portfolio — johnchtsai](https://github.com/johntsaiainow/johnchtsai)** — The starting point for this engineering journey.

---

<div align="center">

### Let's Build Something That Matters.

**John Cheng-Hung Tsai**  
[GitHub](https://github.com/johntsaiainow) · [Email](mailto:john@johntsai.online)

*Technology moves forward. Knowledge should not be left behind.*

</div>
