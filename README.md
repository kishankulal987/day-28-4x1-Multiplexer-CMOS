# 4x1 Multiplexer CMOS in Verilog

##  Overview

In this project, I implemented a **4x1 multiplexer** in Verilog using **CMOS transmission gates** to demonstrate switch-level design.

The circuit selects one of four input bits (`i3`, `i2`, `i1`, `i0`) based on two select lines (`sel1`, `sel0`) to produce the output `y`.

**Example:**

- Inputs: `i3 = 1, i2 = 0, i1 = 1, i0 = 0`
- Select: `sel1 = 0`, `sel0 = 1`
- Output: `y = i1 = 1`

---

## 🔧 Module: `mux4X1_cmos`

### ✅ What I Did
Designed a 4x1 multiplexer using **CMOS transmission gates** modeled with `tranif0` and `tranif1`.

### 📥 Inputs
- `i3`, `i2`, `i1`, `i0`: Four input bits  
- `sel1`, `sel0`: Two select lines  

### 📤 Output
- `y`: Multiplexer output  

### ⚙️ How It Works

I used 8 transmission gates to connect inputs to the output based on select lines:

| Input | Path                         | Selection Condition         |
|-------|------------------------------|-----------------------------|
| i0    | `tranif0(sel0)` + `tranif0(sel1)` | `sel1=0`, `sel0=0`        |
| i1    | `tranif1(sel0)` + `tranif0(sel1)` | `sel1=0`, `sel0=1`        |
| i2    | `tranif0(sel0)` + `tranif1(sel1)` | `sel1=1`, `sel0=0`        |
| i3    | `tranif1(sel0)` + `tranif1(sel1)` | `sel1=1`, `sel0=1`        |

### 🧬 Logic Expression

```
y = (sel1, sel0) == 00 ? i0 :
    (sel1, sel0) == 01 ? i1 :
    (sel1, sel0) == 10 ? i2 :
                         i3;
```

### 💡 Style
Switch-level modeling using **transmission gate primitives** (`tranif0`, `tranif1`).

---

## 🧪 Testbench: `mux4X1_tb` (Comprehensive)

### ✅ What I Did
Wrote a comprehensive testbench to simulate all possible select and input combinations.

### 🔍 How It Works
- Nested loops to generate all 4×16 = **64 combinations**
- Each test case runs for 10 ns → **Total = 640 ns**
- VCD dumping enabled for waveform analysis
- Results printed using `$display`
- Ends with `$finish`

```verilog
$dumpfile("mux4x1.vcd");
$dumpvars(0, mux4X1_tb);
```

### 🕒 Time Scale
```
`timescale 1ns / 1ps
```

---

## 🧪 Testbench: `mux4X1_tb_simple.v` (Simplified)

### ✅ What I Did
A minimal testbench for basic verification.

### 🔍 How It Works
- Select lines loop from `00` to `01`
- Input vectors loop from `0000` to `0011`
- Each case: 10ns → **Total = 80 ns**
- Outputs printed via `$display`
- Ends with `$finish`

---

## 📁 Files

- `mux4X1_cmos.v`: Verilog module for the 4x1 CMOS multiplexer  
- `mux4X1_tb.v`: Comprehensive testbench  
- `mux4X1_tb_simple.v`: Simplified testbench  

---



## 📊 Simulation Waveform

This image displays the simulation waveform output. It shows the correct selection of inputs based on all `sel1:sel0` combinations over 640ns.

![Screenshot 2025-06-29 194853](https://github.com/user-attachments/assets/8587bd34-d78c-4751-80e7-fcf8bc7aa257)


## 🖥️ Console Output

Console log from `$display` showing test results:

![Screenshot 2025-06-29 195207](https://github.com/user-attachments/assets/7a79da5c-bbaf-4a08-a6d6-4b32272c601e)



