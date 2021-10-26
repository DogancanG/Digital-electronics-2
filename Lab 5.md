# Lab 5: Dogancan Gurbuz



  https://github.com/DogancanG/Digital-electronics-2


### 7-segment library

1.It becomes a common anode in seven segment displays, when all the anodes are connected to one point. Common cathode means that all of a 7-segment display's seven cathodes are connected together 



![a](https://user-images.githubusercontent.com/91128817/138772391-4bbb4eb7-4b0d-40ca-8b38-c692fb858bd8.png)





A positive voltage should be supplied to the common anode in order to operate
and the common cathode should be grounded. The Cathode(-) side of led's are
connected to a, b , c, d , e, f, g pins of seven segment display in common Anode.
The anode(+) side's of Common Cathode led are connected to a, b , c, d , e, f, g pins
of seven segment display



2.
```c
static uint8_t pos = 0;
static uint8_t val0=0;
static uint8_t val1=0;
ISR(TIMER1_OVF_vect)
{
    
    val0++;
	
    if(val0 > 9){
		val0 = 0;
		val1++;
		if(val1>5){
			val1=0;
		}
	}
	SEG_update_shift_regs(val0, 0);
	
}
ISR(TIMER0_OVF_vect)
{
	pos++;
	if (pos>1){
		pos=0;
		SEG_update_shift_regs(val0,pos);
	}
	
	else {
		SEG_update_shift_regs(val1,pos);
	}
}

ISR(TIMER0_OVF_vect)
{
    static uint8_t pos = 0;

}
```
3.



![WhatsApp Image 2021-10-26 at 00 20 31](https://user-images.githubusercontent.com/91128817/138846914-f987e46c-c741-45b6-b355-ec40613051fb.jpeg)




### Kitchen alarm

![WhatsApp Image 2021-10-26 at 11 00 33](https://user-images.githubusercontent.com/91128817/138846940-9d03e5cb-927b-4f8a-8444-58cbc9908f31.jpeg)


