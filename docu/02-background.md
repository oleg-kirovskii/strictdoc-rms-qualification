# Background
## Functional Safety
Functional Safety is the ability of a system to keep harm caused by potential system failure at a reasonable level.

Similarly to other quality attributes (think performance, expandability, portability), achieving functional safety is not straightforward. To guide the developer, multiple functional safety standards were created (the list is by no means complete):
* IEC 61508, the mother of all functional safety standards,
* ISO 13849 for machinery,
* ARP 4751 for avionics (and its daugher, DO-178 for avionics software),
* ISO 26262 for automotive,
* etc.

## ISO 26262
**ISO 26262** "Functional Safety. Road vehicles" is the standard used in automotive industry, which we will focus on here.

This standard breaks down all system whose fault may be harmful into four "classes" depending on the extend of the harm and its probability. Those "classes" are called *Automotive Safety Integrity Levels*, or *ASILs*. They are ranged from **ASIL A**, the minimal, "least risky" class, to **ASIL D**, the maximal, or "most risky" class.

ASILs are assigned to safety requirements, i.e. requirements aimed at risk minimization and human protection functionality.

## Confidence in use of Software Tools
### What confidence?
The idea behind any safety work is to minimize risks related to the use of the system. To do that, one needs to look at all potential sources of harm, including HW glitches and design errors, SW bugs, mistakes during manufacturing etc.

Errors of software tooling used in system development is clearly one of the potential sources of harm. By safety logic, we need to analyze this source of harm, establish requirements on its minimization, and take action to implement those requirements.

According to ISO 26262-8:11 "Confidence in use of software tools", minimizing risks related to the tools is achieved via two steps:
* **tool classification** for understanding how bad wrong behavior of the tool cold be, and
* **tool qualification** for doing something about it.

**NOTE**: The designation "ISO 26262-8:11" means "ISO 26262, Part 8, Chapter 11". Yes, this is somehow similar to how the Bible is referenced.

### Tool classification
Just as with any other faults, not all tool faults are equal. Faults of system components are assessed based on the ASIL of the safety requirement that is violated by this fault, i.e. a fault of a component that is violating a requirement rated with ASIL A brings much less risk into the system than a fault violating an ASIL D requirement.

Faults of the tools cannot be traced to a specific required, so they have another base for assessment: *Tool Confidence Levels* or *TCLs*. There are three TCLs: TCL1, TCL2, and, as you may have guessed, TCL3.

TCL of a tool is determined based on two parameters:
* *Tool Impact*, or *TI*:
  * TI1 &mdash; no error of the tool has any effect that may result in violation of a safety requirement, and
  * TI2 &mdash; there is an error of the tool that may result in violation of a safety requirement
* *Tool error Detection*, or *TD*:
  * TD1 &mdash; there is a **high** degree of confidence that an error of the tool will be detected or prevented,
  * TD2 &mdash; there is a **medium** degree of confidence that an error of the tool will be detected or prevented
  * TD3 is selected otherwise.

TCL is defined based on the following table (ISO 26262-8, Table 3):

|     | TD1  | TD2  | TD3  |
|-----|------|------|------|
| TI1 | TCL1 | TCL1 | TCL1 |
| TI2 | TCL1 | TCL2 | TCL3 |

### Tool qualification
The action we need to take against the risks related to the errors of the tool is determined based on TCL and the maximum ASIL of the project where the tool is used.

For TCL1, no action is needed.

For TCL2 or TCL3, we need to establish one of four methods for risk minimization:

1. *Increased confidence from use* &mdash; the tool has been used many times in many projects and no risks traceable to tool errors were found.
1. *Evaluation of tool development process* &mdash; the tool has been created according to a standardized software development process model (e.g. SPICE/ASPICE, CMMI, or similar), which guarantees minimization of the probability of errors via state-of-the-art design, coding, and testing processes.
1. *Validation of software tool* &mdash; the tool functionality has been extensively tested and the probability of residual bugs is low.
1. *Development in accordance with a safety standard* &mdash; same method as the evaluation of development process, but stronger.


The table below shows the suitable method depending on TCL of the tool and max. ASIL of the project (ISO 26262-8, tables 4 & 5):

|      |                             | **ASIL A** | **ASIL B** | **ASIL C** | **ASIL D** |
|----------|---------------------------------|------------|------------|------------|------------|
| **TCL2** | *Increased confidence*            | ++         | ++         | ++         | +          |
| **TCL2** | *Process evaluation*              | ++         | ++         | ++         | +          |
| **TCL2** | *Tool validation*                 | +          | +          | +          | ++         |
| **TCL2** | *Development per safety standard* | +          | +          | +          | +          |
| **TCL3** | *Increased confidence*            | ++         | ++         | +          | +          |
| **TCL3** | *Process evaluation*              | ++         | ++         | +          | +          |
| **TCL3** | *Tool validation*                 | +          | +          | ++         | ++         |
| **TCL3** | *Development per safety standard* | +          | +          | ++         | ++         |