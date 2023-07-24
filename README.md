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

# Commands to be run to setup the Codespace

> This will install all the necessary requirements

```text
source setup.h
```

## Challenge Level 1
Run <code> make </code> command

### Challenge 1 - Logical
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/ff366ae5-d71d-40cd-9d60-189dd9c565fe)

##### Issue: 
1. z4: register not part of RISC-V standard specification
2. addi: incorrect instruction

##### Fix:

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/44ff6210-3a92-4e27-ac98-d70c57f246b7)
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/6f9c928a-3a02-491d-9b30-5bb63a12aa82)

### Challenge 2 - Loop
##### Issue: 
<code> make </code> command was not terminating because there was no condition as such to come out of loop statment.

##### Fix:

<code> t5 </code> register is initialised to 3 in the code, so having a condition to decrement by 1 for each incoming input would make sure all the test cases are covered.

![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/308898c5-fdfb-4a62-a9ff-554eb71f6bbe)

### Challenge 3 - Illegal
##### Issue: 
<code> make </code> command was not exiting the spike because the interrupt service routine was not getting terminated.

##### Fix:
![image](https://github.com/vyomasystems-lab/riscv-ctb-challenge-gagana-05/assets/82756709/61105e2b-f0f6-424b-b706-8a106559079c)

## Challenge Level 2

### Challenge 1 - Instructions
##### Issue: 
Some of the instructions were not included as part of rv32 Instruction Set Architecture (ISA), so made changes to <code> Makefile </code>.

##### Fix:

These variables need to reassigned as mentioned below
```text
--arch rv64
-march=rv64im
-mabi=lp64
--isa=rv64im
```

### Challenge 2 - Exceptions

## Challenge Level 3





## Challenge Level 3

