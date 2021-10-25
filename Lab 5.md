# Lab 5: Dogancan Gurbuz



   [https://github.com/...](https://github.com/...)


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
    //static uint8_t val0 = 0;  // This line will only run the first time
    // WRITE YOUR CODE HERE
   // static uint8_t val1=0;  
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





### Kitchen alarm

![WhatsApp Image 2021-10-25 at 23 55 44](https://user-images.githubusercontent.com/91128817/138776671-2eda179b-e240-4c4c-929a-7c3c974e81b4.jpeg)

