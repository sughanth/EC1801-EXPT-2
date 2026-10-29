# EXPT 2 - Verification of Logic Gates
### SIMULATION AND VERIFICATION OF NAND, XOR, NOR GATES
## Aim
To design, implement, and verify the functionality of basic NAND, XOR, and NOR logic gates using Verilog HDL, and verify the functionality using Synopsys VCS and DVE.
# Software Required
•	Synopsys VCS
•	Synopsys DVE
•	Linux Terminal
•	Verilog HDL
# Boolean Function
The basic logic gates realize the following Boolean functions:

•	AND: Y_NAND = `(a & b)
•	OR: Y_NOR = `(a | b)
•	NOT: Y_XOR = a ^ b

# Theory / Synopsis
Logic gates are the basic building blocks of digital systems. NAND and NOR are universal gates. XOR produces 1 when its inputs differ, while XNOR produces 1 when its inputs are equal.
# Files to be Created
File name	Purpose
logic_gates.v	Logic-gate RTL
logic_gates_tb.v	All input combinations and VCD generation
 # Verilog  Program
module basic_gates (
    input  wire a,
    input  wire b,
    output wire y_nand,
    output wire y_nor,
    output wire y_xor
);
    assign y_nand = ~(a & b);
    assign y_nor  = ~(a | b);
    assign y_xor  =  a ^ b;
endmodule
# **Test Bench Program**
module tb2;
    reg  a, b;
    wire y_nand, y_nor, y_xor;

    basic_gates uut (
        .a(a),
        .b(b),
        .y_nand(y_nand),
        .y_nor(y_nor),
        .y_xor(y_xor)
    );

    initial begin
        $dumpfile("basic_gates.vcd");
        $dumpvars(0, tb2);

        $monitor("Time=%0t a=%b b=%b | NAND=%b NOR=%b XOR=%b",
                 $time, a, b, y_nand, y_nor, y_xor);

        a = 0; b = 0; #10;
        a = 0; b = 1; #10;
        a = 1; b = 0; #10;
        a = 1; b = 1; #10;

        $finish;
    end
endmodule




 <img width="1237" height="497" alt="WhatsApp Image 2026-10-29 at 6 41 24 PM" src="https://github.com/user-attachments/assets/4731fcbf-8b88-4912-a84c-6588978a55fe" />





# Simulation Procedure
STEP 1 – Open Terminal
Open a terminal in the experiment folder.
bash

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs logic_gates.v logic_gates_tb.v -full64
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the input combinations and corresponding output F.
A VCD waveform file is also generated:
exp1_boolean_min.vcd

STEP 5 – Open DVE
dve -full64
Other option
dve -full64 &
A DVE environment will open.


DVE Waveform Verification
In DVE:
Open the testbench hierarchy.
Locate the signals: 
a
b
y_NAND
y_NOR
y_XOR
Add the signals to the waveform window.
Run/inspect the waveform.
Verify that y_nand = 1 only when a=1 AND b=1 — the single combination where both inputs are high.
Verify that y_nor = 1 whenever a=1 OR b=1 (any input high forces the output high).
Verify that y_xor is always the exact complement of a, regardless of b.
The waveform should agree with the truth table.
# Expected Result
The basic logic gates — AND, OR, and NOT — were realized using Verilog HDL:
y_nand = ~(a & b);
y_nor  = ~(a | b);
y_xor  =  a ^ b;
The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected truth table.
Output




<img width="1920" height="232" alt="EX 2" src="https://github.com/user-attachments/assets/17428014-ca38-4608-9505-ee95f491c2fc" />

# OUTPUT

<img width="1920" height="1080" alt="Screenshot 2026-10-29 182555" src="https://github.com/user-attachments/assets/992c2b73-c3e5-4172-bc23-3b0438cdaeac" />

 
