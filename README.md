# 50 ms DELAY USING TIMER 0 IN MODE 2

## AIM
To generate a 50 ms delay using Timer 0 in Mode 2 (8-bit timer mode) in 8051.

---
## APPARATUS REQUIRED
- Personal Computer  
- Keil µVision software

---
## Algorithm
1. Start the program.
2. Initialize Timer 0 in Mode 2 (8-bit auto-reload) by loading the value 02H into the TMOD register.
3. Load the reload value into the THO and TL0 registers to get the required time delay (for 50 ms delay, use THO = 38H).
4. Start Timer 0 by setting the TRO bit in the TCON register.
5. Call the delay subroutine:
Clear the timer overflow flag (TF0).
Wait until TFO becomes 1 (indicating timer overflow).
Repeat this for the required number of overflows to obtain 50 ms total delay.
6. Toggle the LED connected to Port 3.0 using the CPL P3.0 instruction.
7. Repeat the process continuously to blink the LED on and off with a 50 ms delay.
8. Stop.
---
## PROGRAM

```ORG 0000H
MAIN: MOV TMOD, #02H
      MOV TH0, #38H
      MOV TL0, #38H
      SETB TR0
LOOP: ACALL DELAY
      CPL P3.0
      SJMP LOOP

DELAY: MOV R2, #250
WAIT:  JNB TF0, WAIT
       CLR TF0
       DJNZ R2, WAIT
       RET
END

```
---
## OUTPUT:
![WhatsApp Image 2025-10-24 at 17 41 11_1126a188](https://github.com/user-attachments/assets/0e57fa73-2ff9-496e-ab66-ba12c6a92966)

---

## RESULT:
Thus, 50 ms delay using Timer 0 in Mode 2 is generated successfully.
