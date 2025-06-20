# RISC-V Assembler & Simulator

This project is a two-phase C++ implementation of a **RISC-V toolchain**:  
- **Phase 1:** Converts RISC-V Assembly (`input.asm`) to Machine Code (`output.mc`)  
- **Phase 2:** Simulates execution of Machine Code using a 5-stage pipeline model and logs register & memory states.

---

## 👥 Team Members
- **Aadit Mahajan (2023CSB1091)**
- **Aksh Sihag (2023CSB1097)**
- **Rahul Goyal (2023CSB1150)**

---

## 📚 Table of Contents
- [Installation & Compilation](#installation--compilation)
- [Phase 1: Assembler](#phase-1-assembler)
- [Phase 2: Simulator](#phase-2-simulator)
- [Supported Instructions](#supported-instructions)
- [Assembler Directives](#assembler-directives)
- [Label Definition Rules](#label-definition-rules)
- [Output Format](#output-format)
- [Conclusion](#conclusion)

---

## 💻 Installation & Compilation

### For Assembler (Phase 1)
```bash
g++ phase1.cpp -o assembler
./assembler input.asm
```

### For Simulator (Phase 2)
```bash
g++ phase2.cpp -o simulator
./simulator
```

### Optional: Run GUI Simulator
```bash
cd gui_simulator
npm install
npm run dev
```

---

## 🔧 Phase 1: Assembler

### Overview
The assembler reads `input.asm`, parses valid RISC-V instructions, handles labels and directives, and outputs corresponding machine code into `output.mc`.

### Usage
1. Write valid RISC-V code in `input.asm`
2. Run the assembler
3. Machine code will be stored in `output.mc`

### Notes
- Full-line comments allowed.
- Inline comments allowed only if **not attached** to instruction.
- Each register or immediate must be **space-separated and comma-separated**.
- Labels must be on a line **separate** from the instruction/data.

---

## 🧪 Phase 2: Simulator

### Overview
Reads `input.mc` from Phase 1 and simulates its execution using the **5-stage pipeline** model:
1. **IF** - Fetch from memory using PC  
2. **ID** - Decode instruction and operands  
3. **EX** - ALU execution / Branch calculation  
4. **MEM** - Perform memory access if needed  
5. **WB** - Write back to registers  

### Key Features
- 32 registers (`x0` hardwired to 0)
- Supports all major RISC-V instruction types
- Efficient memory allocation (only modified addresses logged)
- Final state written to `output.mc`
- Clock cycles tracked for performance analysis

---

## ✅ Supported Instructions

### R-Type
```bash
add, and, or, sll, slt, sra, srl, sub, xor, mul, div, rem
```

### I-Type
```bash
addi, andi, ori, lb, ld, lh, lw, jalr
```

### S-Type
```bash
sb, sw, sd, sh
```

### SB-Type
```bash
beq, bne, bge, blt
```

### U-Type
```bash
auipc, lui
```

### UJ-Type
```bash
jal
```

---

## 📁 Assembler Directives

The assembler supports the following directives:
- `.text` – Code segment
- `.data` – Data segment
- `.byte .half .word .dword` – Reserve memory
- `.asciiz` – Null-terminated string

---

## 🏷️ Label Definition Rules

**✅ Correct (Preferred):**
```asm
loop:
    add x1, x2, x3

arr:
.word 1 2 3
```

**❌ Incorrect (Avoid):**
```asm
loop: add x1, x2, x3
arr: .word 1 2 3
```

---

## 🧾 Output Format

### input.mc
```bash
0x0 0x00000093
# Data segment
0x10000000 0x0000000A
```

### output.mc (after simulation)
```bash
Final Registers:
Reg[0]: 0x00000000
Reg[1]: 0x0000000A
...

Final Memory State:
Mem[0x1000] = 0x0A
...

Final Clock Cycles: 42
```

---

## ✅ Conclusion

The RISC-V Assembler & Simulator provides a full pipeline from Assembly to Execution. Ideal for understanding instruction formats, CPU architecture, and systems programming.  
For any issues, refer to documentation or contact the project contributors.
