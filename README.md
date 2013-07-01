Digital-Geiger-Counter-with-PIC16F628A
======================================

' *****************************************************************************
' Geiger Counter with UART Communication and LCD
' Copyright (c) 2012 RadioHobbyStore Electronics http://radiohobbystore.com
' Version: 1.01
' Author: Alexey Boguslavsky
' Compiler: MikroElectronica MicroBasic free version
' Contact: support <at> radiohobbystore.com
'******************************************************************************
' This program is used with Geiger Counter DIY Kit from RadioHobbyStore. You can
' purchase DIY Kit with flashed PIC16F628A on http://radiohobbystore.com
'******************************************************************************
' MCU: PIC16F628A
' 4.0000 MHz
' SBM20 or STS5 GM Tube
' 5 or 10 seconds measuring period, selected with jumper on RB5
' Conversion Factor is 0.0057 (57 = 0.0057 x 10000 to avoid float)
' Alarm Indication
' Interrupt on RB0/INT pin
' Restart button on MCLR - press after changing time period
' LCD HD44780 16 x 2
' CPM Maximum Counting Ability: 65535 cpm
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
' !!COPYRIGHTS!!
' This code is free for EDUCATIONAL AND NON-COMMERCIAL PURPOSES only!
' The author of this code allow to use this program with any non-commercial
' dosimeters projects, but WITHOUT ANY WARRANTY from his side! Please post
' link to RadioHobbyStore if you are going to use this code, or part of this code,
' in your own educational projects.
' You can't use this source code or hex/asm file for producing DIY kits for sale!
'
' HOW IT WORKS?
' MCU counts high-low-high interrupts from GM Tube during presettable measuring
' period of 5 or 10 seconds. Then it calculate CPM (counts per minute). The
' maximum CPM reading that can be displayed is 65535.
' To convert CPM to uSv/h we use Conversion Factor of 0.0057 for SBM20. You can
' use your own value, but remember to avoid floating calculation.
' After each measuring period is done, the MCU send CPM data via UART.
'
' !!RADIATION DOSE WARNING!!
' Take note: this is amateur and educational purpose project. That's why the dose
' calculation may be not accurate! Avoid using this device in high radiation
' area where you can be exposed to dangerous levels of ionizing radiation.
' Why radiation dose calculation maybe not accurate? There is several reasons for it.
' First and main reason is necessity to use beta-filter during measuring gamma
' radiation sources. Lack of proper beta-filter can lead to a significant increase
' in readings. The second reason is +-20% GM Tube tolerance. In fact there are
' many more reasons why dose calculation can be not accurate, details can be
' found in educational sources for dosimetrist.
'
' SOFTWARE CALCULATION LIMITATION
' The software has limitation to 65535 cpm maximum readings, i.e. for SBM20 and
' conversion factor of 0.0057 we can get about 370uSv/h maximum
' dose on the display. Due to SBM20 datasheet the tube can detect 144mR/h, or
' about 3000cps. 65535/60 = 1092.25 cps. As you can see we did not get to
' the upper limit of SBM20 with the software, but in real life condition you
' probably not expect to see that radiation level! Anyway if you get readings
' close to 65535 cpm just leave the danger area as soon as it possible!
'******************************************************************************
