# Lab 7:  Dogancan Gurbuz

Link to this file in your GitHub repository:

https://github.com/DogancanG/Digital-electronics-2/new/main/Labs/07-uart/adc

### Analog-to-Digital Conversion

1. Complete table with voltage divider, calculated, and measured ADC values for all five push buttons.

   | **Push button** | **PC0[A0] voltage** | **ADC value (calculated)** | **ADC value (measured)** |
   | :-: | :-: | :-: | :-: |
   | Right  | 0&nbsp;V | 0   | 0 |
   | Up     | 0.495&nbsp;V | 101 | 100 |
   | Down   |   1.203V    |   246  |256  |
   | Left   |   1.970V    |  403   | 410 |
   | Select |    3.182V  |  651   |640  |
   | none   |    5V   |   1023  | 1023 |
2. Code listing of ACD interrupt service routine for sending data to the LCD/UART and identification of the pressed button. Always use syntax highlighting and meaningful comments:

```c
/**********************************************************************
 * Function: ADC complete interrupt
 * Purpose:  Display value on LCD and send it to UART.
 **********************************************************************/
ISR(ADC_vect)
{
    uint16_t value = 0;
    char lcd_string[4] = "0000";

    value = ADC;                  // Copy ADC result to 16-bit variable
    itoa(value, lcd_string, 10);  // Convert decimal value to string

    // WRITE YOUR CODE HERE
  //Clear previous value
    lcd_gotoxy(8,0);
    lcd_puts("    ");
    //Put new value TO LCD
    itoa(value, lcd_string, 10);  // Convert decimal value to string
    lcd_gotoxy(8,0);
    lcd_puts(lcd_string);
    // send the same value to UART
     uart_puts(lcd_string);
     uart_puts(" ");
     
     
    //Clear previous value
    lcd_gotoxy(13,0);
    lcd_puts("    ");
    //Put new value to LCD
    
    //display value in hexa
    itoa(value, lcd_string, 16);  // Convert decimal value to string
    lcd_gotoxy(13,0);
    lcd_puts(lcd_string);
    
    //display what button was pressed
     lcd_gotoxy(8,1);
     lcd_puts("    ");
     lcd_gotoxy(12,1);
     lcd_puts("    ");
    
    
     lcd_gotoxy(8, 1);
     itoa(value, lcd_string, 10);
     if (value>1000) { lcd_puts("none");}
         if ((value>600)&&(value<1000)) { lcd_puts("select");}
              if ((value>350)&&(value<450)) { lcd_puts("left");}
                   if ((value>200)&&(value<270)) { lcd_puts("down");}
                        if ((value>5)&&(value<120)) { lcd_puts("up");}
                             if (value==0) { lcd_puts("right");}
             
     // lcd_puts(lcd_string);
;
}
```

### UART communication

1. (Hand-drawn) picture of UART signal when transmitting three character data `De2` in 4800 7O2 mode (7 data bits, odd parity, 2 stop bits, 4800&nbsp;Bd).

![WhatsApp Image 2021-11-09 at 00 40 14](https://user-images.githubusercontent.com/91128817/140835668-b4e38e42-0be9-4024-b6c4-454fa1a00149.jpeg)




2. Flowchart figure for function `uint8_t get_parity(uint8_t data, uint8_t type)` which calculates a parity bit of input 8-bit `data` according to parameter `type`. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

![WhatsApp Image 2021-11-09 at 00 40 13(1)](https://user-images.githubusercontent.com/91128817/140836511-d56f9c33-7384-4b1f-b618-faf0435513cf.jpeg)





### Temperature meter

Consider an application for temperature measurement and display. Use temperature sensor [TC1046](http://ww1.microchip.com/downloads/en/DeviceDoc/21496C.pdf), LCD, one LED and a push button. After pressing the button, the temperature is measured, its value is displayed on the LCD and data is sent to the UART. When the temperature is too high, the LED will start blinking.

1. Scheme of temperature meter. The image can be drawn on a computer or by hand. Always name all components and their values.


![WhatsApp Image 2021-11-09 at 00 40 13](https://user-images.githubusercontent.com/91128817/140836855-8c78a22d-9725-42e3-9307-36d56ac10066.jpeg)






