 -RAM-DESIGN

COMPANY NAME : CODTECH IT SOLUTIONS

NAME : ANURAG KUMAR

INTERN ID : CT06DF628

DOMAIN : VLSI

DURATION : 6 WEEKS

MENTOR : NEELA SANTOSH

-----DESCRIPTION----

Objective:
The goal of this task was to design a simple synchronous RAM (Random Access Memory) module using Verilog HDL, which supports both read and write operations. The memory was to operate in sync with a clock signal, meaning all read and write actions should take place on the positive edge of the clock. Along with the RAM design, I was also required to write a testbench and simulate the design to verify that both read and write functionalities work correctly.

Introduction:
RAM is one of the most important elements in any digital system. It is a form of memory that stores data temporarily and allows both reading and writing. This project gave me a deeper understanding of how RAM works at the hardware level. Unlike theoretical understanding, this task pushed me to implement the memory behavior through code and visualize how data is written and read based on control signals and the clock.
Before this task, I had only a basic idea of what RAM is, but I didn’t really know how it's modeled in hardware. Through this task, I got a hands-on feel for designing it using Verilog and simulating its functionality — something that's essential in real-world digital systems.

Design Specifications:
To keep things simple and understandable, I designed a RAM module with the following specifications:
 Data width: 8 bits
 Address width: 4 bits (giving us 16 memory locations, since 2⁴ = 16)
 Control Signals:
  * `clk` (clock)
  * `we` (write enable)
  * `addr` (memory address)
  * `din` (data to be written)
  * `dout` (data to be read)

The RAM is synchronous, which means both reading and writing operations are only triggered at the positive edge of the clock. When `we` (write enable) is set to 1, the data at `din` is written into the memory at the specified address. When `we` is 0, the value stored at that address is read and assigned to `dout`.

Verilog Code:
Here’s the core RAM module I created:

```verilog
module RAM (
    input clk,
    input we,
    input [3:0] addr,
    input [7:0] din,
    output reg [7:0] dout
);

    reg [7:0] memory [0:15];

    always @(posedge clk) begin
        if (we)
            memory[addr] <= din;
        else
            dout <= memory[addr];
    end

endmodule
```
This design uses a simple `always` block triggered on the positive edge of the clock. I also used a `reg [7:0] memory [0:15];` to declare the memory space.

Testbench and Simulation:

To validate the RAM module, I created a testbench where I wrote two values into different memory addresses and then read them back. Here's the key part of the testbench:

```verilog
initial begin
    $dumpfile("ram_wave.vcd");
    $dumpvars(0, RAM_tb);

    clk = 0;
    we = 1; addr = 4'b0000; din = 8'hA5; #10;
    addr = 4'b0001; din = 8'h3C; #10;

    we = 0; addr = 4'b0000; #10;
    addr = 4'b0001; #10;

    $finish;
end
```

A clock signal was generated using an `always` block, and the memory was written to when `we = 1`. Later, `we` was set to 0 to read from those addresses. During the simulation, I verified that:

* Address 0 stored value `A5`
* Address 1 stored value `3C`
* Both were correctly retrieved during the read phase

Simulation Results:

I ran the simulation using EDA playground and viewed the waveform in EP Waveform. The `dout` values matched the expected outputs at each stage of the simulation. This confirmed that the RAM was working properly. The waveform clearly showed:

* Data being written on the clock edge when `we = 1`
* Data being read correctly when `we = 0`

This visual verification helped me understand the synchronization with the clock signal and the behavior of memory storage in digital systems.

OUTPUT(WAVEFORM) : 

   ![Image](https://github.com/user-attachments/assets/330a21a5-92c8-48f3-979a-165a20382e8e)

Conclusion:
This task gave me a clear understanding of how RAM works at a hardware level. Writing the Verilog code was straightforward once I understood the structure, but the most interesting part was seeing the simulation and watching the memory operate cycle by cycle. It was especially exciting to visualize data being written and read.
By completing this task, I feel much more confident about memory design and have a solid foundation to move forward to more advanced digital design tasks like register files, FIFO memory, or even designing a basic processor. Overall, this task was a very practical and valuable learning experience during my internship.



