
# Serial Transfer of Single Byte / Character using 8051 (Keil)

## AIM
To write and execute an Embedded C Program for Serial Transfer of Single Byte / Character using 8051 in Keil.

## APPARATUS REQUIRED
- Personal Computer  
- Keil µVision Software  

## PROGRAM

### (i) Serial Port Transfer a Single Character

```asm
ORG 00H 
MOV TMOD, #20H 
MOV TH1, #0FCH 
MOV SCON, #40H 
SETB TR1 
AG: MOV SBUF, #'B' 
 WAIT:JNB TI, WAIT
 CLR TI 
 SJMP AG
 END

```
```asm
#include<reg51.h>
void main(void)
{
TMOD=0X20; //TIMER 1, MODE 2
TH1=0XFC;
SCON=0X40;
TR1=1;
while(1)
{
SBUF='B';
while(TI==0);
T1=0;
}
}
```
### (ii) Serial Port to Transfer a Message

```asm
ORG 00H
MOV TMOD,#20H
MOV TH1,#0FCH
MOV SCON,#40H
SETB TR1
MOV B,30H
MOV DPTR,#4500H
AGAIN:MOVX A,@DPTR
MOV SBUF,A
WAIT:JNB TI,WAIT
CLR TI
INC DPTR
DJNZ B,AGAIN
END


```
```asm
#include<reg51.h>
#include<string.h>
void main(void)
{
unsigned char msg[]="Tamilselvan R";
unsigned char i;
int l = strlen(msg);
TMOD=0X20;//TIMER 1,MODE 2
TH1=0XFC;
SCON=0X40;
TR1=1;
for (i=0; i<l;i++)
{
SBUF= msg[i];
while(TI==0);
TI=0;
}
while(1);
}

```

### OUTPUT:
<img width="1653" height="715" alt="image" src="https://github.com/user-attachments/assets/5e01e306-51a7-4d8f-a2b7-a13a02ab86a5" />
<img width="1483" height="781" alt="image" src="https://github.com/user-attachments/assets/fe181459-ff8c-4281-b6cb-e80a27d2cb10" />


### RESULT:
Thus the Serial transfer of Single Byte / Character using 8051 KEIL was done and shown the output.
