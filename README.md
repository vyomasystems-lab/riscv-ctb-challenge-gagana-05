# RISC-V CTB Submission

<br>
<details>
  <summary>Table of Contents</summary>
    <ol>
        <li>
            <a href="#challenge-level-1">Challenge Level 1</a>
        </li>
        <li> 
            <a href="#challenge-1-logical">Challenge 1 - Logical</a>
        </li>
        <li> 
            <a href="#challenge-2-loop">Challenge 2 - Loop</a>
        </li>
        <li>
            <a href="#challenge-3-illegal">Challenge 3 - Illegal</a>
        </li>
         <li>
            <a href="#challenge-level-2">Challenge Level 2</a>
        </li>
        <li>
            <a href="#challenge-1-instruction">Challenge 1 - Instructions</a> 
        </li>
        <li>
            <a href="#challenge-2-exceptions">Challenge 2 - Exceptions</a> 
        </li>
         <li>
            <a href="#challenge-level-3">Challenge Level 3</a> 
        </li>
    </ol>
</details>

# Commands to be run to set up the Codespace

> This will install all the necessary requirements

```text
source setup.h
```

## Challenge Level 1
Run <code>make</code> command

### Challenge 1 - Logical
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/ff366ae5-d71d-40cd-9d60-189dd9c565fe)

##### Issue: 
1. z4: register not part of RISC-V standard specification
2. addi: incorrect instruction

##### Fix:
```text
add s7, ra, s4 // replace z4 with s4
add s5, t1, s0 // replace addi with add instr
```

### Challenge 2 - Loop
##### Issue: 
<code>make</code> command was not terminating because there was no condition as such to come out of the loop statement.

##### Fix:

<code>t5</code> register is initialized to 3 in the code, so having a condition to decrement by 1 for each incoming input would ensure all the test cases are covered.

```text

loop:
	lw t1, (t0)
  lw t2, 4(t0)
  lw t3, 8(t0)
  add t4, t1, t2
  addi t0, t0, 12
  addi t5, t5, -1
  bne t3, t4, fail        # check if sum is correct
  bnez t5, loop
  j test_end
```

### Challenge 3 - Illegal
##### Issue: 
<code>make</code> command was not exiting the spike because the interrupt service routine was not getting terminated.

##### Fix:

```text
mtvec_handler:
  li t1, CAUSE_ILLEGAL_INSTRUCTION
  csrr t0, mcause
  beq t0, t1, pass
  csrr t0, mepc

  mret
```

## Challenge Level 2

### Challenge 1 - Instructions
Fix the AAPG Configuration file to generate the assembly test, compile, and run it successfully in Spike.

##### Issue: 
Some instructions were not included as part of the rv32 Instruction Set Architecture (ISA), so I made changes to Makefile.

##### Fix:

These variables need to be reassigned as mentioned below
```text
-march=rv64im
-mabi=lp64
--isa=rv64im
```

### Challenge 2 - Exceptions
Create an AAPG config file to generate a test with 10 illegal exceptions with the correct handler code. <br>
[Documentation Reference](https://gitlab.com/shaktiproject/tools/aapg/-/wikis/Wiki#exception-generation) <br>

rv32i.yaml 
```text
exception-generation:
  ecause00: 0
  ecause01: 0
  ecause02: 1 #illegal instruction
  ecause03: 10 #Breakpoint
  ecause04: 0
  ecause05: 0
```

Makefile changes
```text
# Defines at the start of Makefile
trap_illegal_instruction=800000e0

compile:
	@echo '[UpTickPro] Test Compilation ------'
	riscv32-unknown-elf-gcc -march=rv64im -mabi=lp64 -static -mcmodel=medany -fvisibility=hidden -nostdlib -nostartfiles -I$(PWD)/work/common -T$(PWD)/test.ld test.S $(PWD)/work/common/crt.S -o test.elf
disass: compile
	@echo '[UpTickPro] Test Disassembly ------'
	riscv32-unknown-elf-objdump -D test.elf > test.disass
spike: compile
	@echo '[UpTickPro] Spike Run ------'
	spike --isa=rv64im test.elf 
	spike --log-commits --log  test_spike.dump --isa=rv64im +signature=test_spike_signature.log test.elf
check: test_spike.dump
	@echo '[UpTickPro] Number of Exceptions'
	spike -l --isa=rv64im test.elf 2> spike.log
	grep $(trap_illegal_instruction) spike.log > exceptions.log
	cat exceptions.log
	wc -l exceptions.log

```
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/522ef20b-67ba-483f-9eab-85b0666e712a)


## Challenge Level 3





## Challenge Level 3

