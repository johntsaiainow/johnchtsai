# Case Study 01 — DaVinci: When Firmware Meets the Physical World

> **Industrial embedded control · C++ · hardware/software integration · product engineering**
>
> **Source:** [DaVinci controller firmware](https://github.com/johntsaiainow/davinciarduino2025) · **Related:** [ESP32 communication PCB](https://github.com/johntsaiainow/ESP32-Communication-Module-PCB) · [AquaMesh firmware bridge](https://github.com/johntsaiainow/AquaMesh-Basic-Bootloader-Bridge)

[← Return to the engineering portfolio](../README.md)

## The engineering question

**What does it take to make software behave predictably when its outputs become physical actions?**

A beverage dispensing controller is not simply an application running on a microcontroller. Its logic has to interact with sensors, actuators, timing constraints, electrical interfaces, and the operational realities of a manufactured machine. A line of code can become a pump activation, a valve transition, or a response to a changing sensor state.

That is the engineering territory represented by **DaVinci 20 Plus**, a beverage dispensing control system associated with my industrial embedded systems work.

## Context and scope

The public repository, [`davinciarduino2025`](https://github.com/johntsaiainow/davinciarduino2025), is described as the **main controller firmware for the DrinkStation DaVinci 20 Plus beverage dispensing system** and is primarily written in **C++**. My broader professional work has included STM32/ESP32 embedded control, sensor and communication integration, hardware/software debugging, validation, and production troubleshooting.

This case study deliberately separates those broader professional capabilities from what has been independently established about this particular public repository. A detailed line-by-line code audit has **not** yet been completed for this portfolio edition.

## The system boundary is the real challenge

In a physical control product, failures can originate in several layers:

| Layer | Engineering question | What an engineer must investigate |
| --- | --- | --- |
| Electrical hardware | Is the signal electrically valid? | Power, wiring, noise, interface behavior |
| Firmware | Is the state transition correct? | Timing, control flow, initialization, error paths |
| Device interfaces | Are sensors and actuators interpreted correctly? | Protocols, readings, output sequencing |
| System integration | Do components behave correctly together? | Reproducibility, diagnostics, integration tests |
| Manufacturing and field use | Does the behavior remain supportable outside the lab? | Fault isolation, serviceability, validation evidence |

This table is an **engineering analysis framework**, not a claim that every listed mechanism or test is implemented in the repository.

## My engineering approach

I approach this class of system by following a problem across boundaries rather than assuming that the symptom identifies the responsible discipline:

1. **Establish expected behavior.** Define what the controller and connected hardware should do in a specific state.
2. **Observe the physical result.** Compare actual sensor, actuator, and communication behavior with the expectation.
3. **Isolate the layer.** Distinguish firmware logic errors from electrical, interface, or system-level causes.
4. **Make the fault reproducible.** Capture a minimal scenario and useful diagnostics.
5. **Validate the correction.** Check the intended behavior and look for regressions in related paths.

These are the principles I bring to embedded engineering; they should not be read as a fabricated incident report or as proof of a specific measured improvement in DaVinci.

## Evidence and technical entry points

- **[DaVinci controller firmware](https://github.com/johntsaiainow/davinciarduino2025):** public C++ firmware project and the primary starting point for code review.
- **[ESP32 Communication Module PCB](https://github.com/johntsaiainow/ESP32-Communication-Module-PCB):** related communication/control hardware design for AquaMesh / DrinkStation systems.
- **[AquaMesh Basic Bootloader Bridge](https://github.com/johntsaiainow/AquaMesh-Basic-Bootloader-Bridge):** separately published ESP32-to-STM32 firmware update bridge; useful evidence of cross-device firmware integration, **not** automatically a component of DaVinci.
- **[KiCad PCB collection](https://github.com/johntsaiainow/small-pcb-design-collection):** additional electronics design artifacts.

## What this case study demonstrates

The strongest story here is not a specific microcontroller or programming language. It is the ability to reason about a product where **software decisions have physical consequences**, and where debugging must connect circuit behavior, embedded code, integration, and product support.

For a firmware, systems, or hardware-in-the-loop engineering manager, the relevant discussion is how to make physical behavior observable, repeatable, and testable.

## Evidence still to add

To make this a fully verified technical case study, I plan to attach or link, where disclosure is authorized:

- A sanitized block diagram identifying the controller, sensors, actuators, and communications paths.
- One concrete, anonymized failure investigation with symptom, root cause, fix, and regression check.
- A representative test procedure or test log and the corresponding firmware location.
- Quantified outcomes **only if documented and approved for publication**.

**Disclosure note:** This portfolio does not publish confidential customer information, proprietary schematics, or unapproved production metrics.

---

**Engineering principle:** *A design is not finished when the code compiles. It must make sense in the physical world.*

[← Portfolio](../README.md) · [Next: Local AI Chatbot →](02-local-ai-chatbot.md)
