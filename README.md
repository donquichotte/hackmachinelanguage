# hackmachinelanguage

Description of the Hack Machine Language from the Coursera course nand2tetris.

## Introduction

There are two types of instrunctions, A instrunctions and C instructions.

The first bit of a 16 bit instruction is always the op code.

| Op Code        | Instruction Type           |
| ------------- |:-------------:|
| 0      | A instruction |
| 1      | C instruction      |

## Registers

There are three register. The A register contains the address. The M register contains the data of the RAM at address A, RAM[A]. The D register is a data register to perform arithmetic or logic operations.

## The A instruction
`@value`
value is a 15 bit address.

Instruction encoding:

| Bit Range       	| Meaning		|
| ------------- 	|-------------|
| i[15]     			| Op Code		|
| i[0..14]      		| value	    |

Loads `value` into the A register and RAM[`value`] into the M register.


## The C Instruction
`dest = comp ; jump`

Instruction encoding:

| Bit Range       	| Meaning		|
| ------------- 	|-------------|
| i[15]     			| Op Code		|
| i[14..13]      		| unused, 1 by default	    |
| i[12]      		| a			    |
| i[11..6]      		| comp	    	|
| i[5..3]    		| dest addr    	|
| i[2..0]    		| jmp	    	|


dest encoding:

| dest 			  	| Code			| effect		|
| ------------- 	|-------------|-------------|
|null				|	000			|	the value is not stored			|
|M					|	001			|	RAM[A]			|
|D					|	010			|	D register			|
|MD					|	011			|	RAM[A] and D register			|
|A					|	100			|	A register			|
|AM					|	101			|	A register and RAM[A]			|
|AD					|	110			|	A register an D register			|
|AMD				|	111			|	A register, D register, RAM[A]			|


comp encoding:

| comp with a = 0   | comp with a = 1	| Code		|
| ------------- 	|------------|-------------|
|0				|				|	101010			|
|1				|				|	111111			|
|-1				|				|	111010			|
|D				|				|	001100			|
|A				|M				|	110000			|
|!D				|				|	001101			|
|!A				|!M				|	110001			|
|-D				|				|	001111			|
|-A				|-M				|	110011			|
|D+1			|				|	011111			|
|A+1			|M+1			|	110111			|
|D-1			|				|	001110			|
|A-1			|M-1			|	110010			|
|D+A			|D+M			|	000010			|
|D-A			|D-M			|	010011			|
|A-D			|M-D			|	000111			|
|D&A			|D&M			|	000000			|
|D\|A			|D\|M			|	010101			|

jump encoding:

| jump 			  	| Code			| effect		|
| ------------- 	|-------------|-------------|
|null					|	000			|	no jump			|
|JGT					|	001			|	if out>0 jump			|
|JEQ					|	010			|	if out=0 jump			|
|JGE					|	011			|	if out>=0 jump			|
|JLT					|	100			|	if out<0 jump			|
|JNE					|	101			|	if out!=0 jump			|
|JLE					|	110			|	if out<=0 jump			|
|JMP					|	111			|	unconditional jump			|
