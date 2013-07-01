Digital Geiger Counter with PIC16F628A
======================================

Geiger Counter with UART Communication and LCD
Copyright (c) 2012 RadioHobbyStore Electronics http://radiohobbystore.com
Version: 1.01
Author: Alexey Boguslavsky
Compiler: MikroElectronica MicroBasic free version

This program is used with Geiger Counter DIY Kit from RadioHobbyStore. You can purchase DIY Kit with flashed PIC16F628A on http://radiohobbystore.com

------------------------------------------

' MCU: PIC16F628A
' 4.0000 MHz
' SBM20 or STS5 GM Tube
' 5 or 10 seconds measuring period, selected with jumper on RB5
' Conversion Factor is 0.0057 (57 = 0.0057 x 10000 to avoid float)
' Alarm Indication
' Interrupt on RB0/INT pin
' Restart button on MCLR - press after changing time period
' LCD HD44780 16 x 2
' CPM Maximum Counting Ability: 175000 cpm
'******************************************************************************
' TMR1 Settings:
' TMR1 = 65536 - Fin/Fout
' Fin = (F(crystal) / 4) / prescaler) / Fout
' Fout = 10Hz
'******************************************************************************
' UART Communication:
' Baud Rate 2400; RX, TX enabled; frame size 8 bits; 1 STOP bit;
' parity disabled; asynchronous operation
'******************************************************************************

