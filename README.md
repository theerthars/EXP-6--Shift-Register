# EXP-6--Shift-Register
# Design and Verification of a 4-bit Serial-In Parallel-Out (SIPO) Shift Register
## Aim

To design and verify a 4-bit Serial-In Parallel-Out (SIPO) Shift Register using Verilog HDL, and to observe its behaviour using a testbench and VCD waveform.

## Theory / Synopsis 

A shift register is a group of flip-flops connected in cascade, sharing a common clock, in which data is shifted from one flip-flop to the next on every active clock edge. In a Serial-In Parallel-Out (SIPO) shift register, one bit of data (sin) is fed in serially at every clock edge, and after several clock pulses the accumulated bits are available simultaneously at the parallel output Q[3:0].

Each clock pulse shifts the existing contents one position (here, left) and inserts the new serial input bit into the vacated (LSB) position. The bit that was in the most significant position is shifted out and discarded (or may be taken as the serial output, sout). An active-high asynchronous reset clears the register to all zeros.

## Functional Description
On every rising edge of clk:

if (rst) Q <= 4'b0000;

else Q <= {Q[2:0], sin};   // shift left, sin enters at LSB

Serial output: sout = Q[3]   (the bit about to be shifted out)

## Design / RTL Program

Testbench Program




## Operation / Truth Table

Register contents after each active clock edge (sin sequence = 1, 0, 1, 1)
<img width="406" height="181" alt="image" src="https://github.com/user-attachments/assets/7a5c1c67-a5d5-4160-938b-3647f8630dd7" />

## Simulation Procedure

STEP 1 – Open Terminal
Open a terminal in the experiment folder.

STEP 2 – Load Synopsys Environment
source /synopsys/start.sh

STEP 3 – Compile Using VCS
vcs shift_reg.v tb.v -full64
If compilation is successful, VCS generates the simulation executable:
simv

STEP 4 – Run Simulation
./simv
The terminal displays the reset, clock, serial input and the resulting parallel output Q and serial output sout at every change (via $monitor). A VCD waveform file is also generated:
shift_reg.vcd

STEP 5 – Open DVE
dve -full64
Other option:
dve -full64 &
A DVE environment will open.

## DVE Waveform Verification
In DVE:
●	Open the testbench hierarchy.

●	Locate the signals: clk, rst, sin, Q[3:0], sout.

●	Add the signals to the waveform window.

●	Run / inspect the waveform.

●	Verify that on every rising edge of clk (with rst = 0), Q shifts left by one bit and sin enters at Q[0].

●	Verify that sout always equals Q[3], the bit that is about to be shifted out.

●	Confirm that Q resets to 4'b0000 immediately whenever rst = 1, independent of clk.

The waveform should agree with the operation table.

## Expected Result

The 4-bit SIPO Shift Register was realized using Verilog HDL, with the characteristic behaviour:

Q(next) = {Q[2:0], sin}

The design was compiled and simulated using Synopsys VCS, and the functionality was verified using DVE waveform analysis, matching the expected operation table.

## Output
<img width="1911" height="1020" alt="Screenshot 2026-11-25 123238" src="https://github.com/user-attachments/assets/b724dd2c-85c0-4cda-883d-7da2bd12dc79" />



## Viva-Voce Questions

●	What is a shift register, and what are its four basic types (SISO, SIPO, PISO, PIPO)?

●	How does a SIPO shift register differ from a PISO shift register?

●	How many clock pulses are required to fully load a 4-bit SIPO shift register with serial data?

●	How would you modify the design to shift right instead of left?

●	How would you convert this SIPO register into a Serial-In Serial-Out (SISO) register?

●	What is the purpose of the asynchronous reset in this design?

●	Why is a VCD file generated, and what does $dumpvars(0, tb) do?

●	How can a shift register be used to implement a ring counter or Johnson counter?

●	What is the difference between a shift register built from D flip-flops versus one described behaviourally in Verilog, in terms of simulation versus synthesis?

## Result

Thus, the 4-bit Serial-In Parallel-Out Shift Register was designed, implemented using Verilog HDL, successfully simulated using Synopsys VCS, and verified using Synopsys DVE.

