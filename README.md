# HW4

A working model of a 16-bit processor. This project can be opened and run with [Logisim](http://www.cburch.com/logisim/), which itself requires Java 5 or later. The processor has 8 registers, `$r0`-`$r7`, but `$r0` is fixed at 0.

There are three types of instructions: R-type, I-type, and J-type. Each instruction starts with 4 bits of opcode, which uniquely indicates the operation to perform. These are listed in order below, i.e. `add` is 0000, `addi` is 0001, and so on. R-type instructions then have 3 bits each for `$rd`, `$rs`, and `$rt` in that order, which are generally understood to be the destination register and the two source registers. This is followed by 3 bits of `shamt` which stands for shift amount. If any of the fields is not used it should be set to zero by convention. I-type (immediate-type) instructions instead have bits only for `$rs` and `$rt` and then 6 bits for the `immed` value. Lastly, J-type instructions use all 12 bits for the `addr`. You can determine which type an instruction is by the number of registers and fields it uses.

The processor uses the following instructions:
* `add $rd, $rs, $rt`: adds `$rs` and `rt` and puts the result in `$rd`.
* `addi $rt, $rs, immed`: adds `$rs` and `immed` and puts the result in `$rt`.
* `sub $rd, $rs, $rt`: subtracts `$rt` from `$rs` and puts the result in `$rd`.
* `not $rd, $rs`: puts the bitwise inversion of `$rs` in `$rd`.
* `xor $rd, $rs, $rt`: puts the bitwise exclusive or of `$rs` and `$rt` and puts it in `$rd`.
* `sll $rd, $rs, shamt`: shifts `$rs` left by `shamt` bits and puts it in `$rd`.
* `srl $rd, $rs, shamt`: logically shifts `$rs` right by `shamt` bits and puts it in `$rd`.
* `lw $rt, immed($rs)`: load word at `$rs+immed` from memory and place in `$rd`.
* `sw $rt, immed($rs)`: store word in `$rd` at `$rs+immed` in memory.
* `bne $rt, $rs, immed`: branch if `$rs` does not equal `$rt`. Branches are caculated by adding 1+`immed` to the program counter. If the branch is not taken then the program counter is simply incremented as usual.
* `blt $rt, $rs, immed`: branch if `$rs` is less than `$rt`.
* `j addr`: jump to `addr` (i.e. set the program counter to `addr`).
* `jr $rs`: jump to the value stored in `$rs`.
* `jal addr`: store the program counter in `$r7` and jump to `addr` (jump and link).
* `input $rt`: take the input from the keyboard and store in `$rt` (uses ASCII values).
* `output $rs`: output the value at `$rs` as a character (uses ASCII values).