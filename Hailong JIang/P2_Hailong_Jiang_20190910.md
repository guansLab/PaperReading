Title: ZOFI: Zero-overhead Fault Injection Tool for Fast Transient Fault Coverage Analysis
Publication: not pulished yet
Author：Vasileios Porpodas, Intel Corporation 
Paper Review
Research Background

Type of Fault-injection Tools
 Source Code Editing: modify instructions in the source code or in the compiler intermediate representation
 Simulator and Emulator: modify a processor simulator: F-SEFI
 Binary, Source or Compiler-IR Instrumentation: build a custom binary-instrumentation tool using a framework like Pin.
 Timing based tool: use a random time instead of a random dynamic instruction.

Problem to Solve

Achieving good accuracy, we need to run Fault Injection in application hundreds and thousands of time, so overhead is a big concern.

Key Design and Algorithm Proposed

Timing based tool: use a random time instead of a random dynamic instruction.

Major Contribution

Major limitation

Something you don’t understand

Your view on the research domain/topic/approach/data/solution (positive or negative)
