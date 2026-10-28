# Practical 1: Display a Name Using 8086 Assembly (MASM)

## Aim

To write and execute an 8086 assembly language program that displays a name-related message using DOS interrupt `21H`.

## Requirements

- DOSBox (or another DOS environment)
- MASM assembler and LINK utility
- A text editor for creating the `.ASM` source file

## Program

Save the following as **`PRAC1.ASM`**. GitHub automatically shows a **Copy** button on this code block.

```asm
.MODEL SMALL
.STACK 100H

.DATA
msg DB 'Name: $'

.CODE
MAIN:
    MOV AX, @DATA
    MOV DS, AX

    MOV AH, 09H
    LEA DX, msg
    INT 21H

    MOV AH, 4CH
    INT 21H

END MAIN
```

> **Note:** The original program prints `Name:` only. To display your actual name, replace the message with something like `msg DB 'Name: Rahul$'`.

## How to Run in DOSBox

1. Put `PRAC1.ASM`, `MASM.EXE`, and `LINK.EXE` in a folder such as `C:\8086` on Windows.
2. Open DOSBox and enter:

```dos
MOUNT C C:\8086
C:
MASM PRAC1.ASM;
LINK PRAC1.OBJ;
PRAC1.EXE
```

3. The program displays its message and returns to the DOS prompt.

**Tip:** If you mounted a different folder, change `C:\8086` accordingly. The semicolon at the end of the MASM and LINK commands accepts their default prompts.

## Output

```text
Name:
```

## Theory

The program uses the **small memory model**, which allows one code segment and one data segment. The `DS` register is initialized so the program can access the string in memory. DOS interrupt `21H` with `AH = 09H` displays characters until it reaches the `$` terminator. DOS function `4CH` ends the program.

## Conclusion

The program successfully displays the text `Name:` using 8086 assembly language and DOS interrupt `21H`. The displayed text can be changed by modifying the string stored in the data segment.
