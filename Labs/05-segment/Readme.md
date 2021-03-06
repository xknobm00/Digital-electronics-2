   | **Digit** | **A** | **B** | **C** | **D** | **E** | **F** | **G** | **DP** |
   | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
   | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 |
   | 1 |  1 |  0 |  0 |  1 |  1 |  1 |  1 |  1 |
   | 2 |  0 |  0 |  1 |  0 |  0 |  1 |  0 |  1 |
   | 3 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 1 |
   | 4 | 1  |  0 |  0 |  1 |  1 | 0  | 0  |  1 |
   | 5 | 0  |  1 |  0 |  0 |  1 | 0  |  0 | 1  |
   | 6 |  0 |  1 | 0  |   0|0   |  0 | 0 | 1  |
   | 7 |  0 | 0  | 0  |  1 |  1 |  1 |  1 | 1  |
   | 8 | 0  | 0  |  0 |  0 | 0  | 0  |  0 |  1 |
   | 9 |  0 | 0  | 0 |  0 | 1  |  0 |  0 | 1  |

# Lab 5: Martin Knob

Link to your `Digital-electronics-2` GitHub repository:

   [https://github.com/xknobm00/Digital-electronics-2](https://github.com/xknobm00/Digital-electronics-2)


### 7-segment library

1. In your words, describe the difference between Common Cathode and Common Anode 7-segment display.
   * CC SSD - mají společnou katodu a ovládají se vysokou úrovní
   * CA SSD - mají společnou anodu a ovládají se nízkou úrovní

2. Code listing with syntax highlighting of two interrupt service routines (`TIMER0_OVF_vect`, `TIMER0_OVF_vect`) from counter application with at least two digits, ie. values from 00 to 59:

```c
ISR(TIMER1_OVF_vect)
{
	// WRITE YOUR CODE HERE
	cnt0++;
	if (cnt0 > 9)
	{
		cnt0 = 0;
		cnt1++;
		if (cnt1 > 5)
		(cnt1 = 0);
	}
}

ISR(TIMER0_OVF_vect)
{
	static uint8_t pos = 0;  // This line will only run the first time
	cnt0++;
	if (cnt0 > 9)
	cnt0 = 0;
	
	SEG_update_shift_regs(cnt0, 0);
	SEG_update_shift_regs(cnt1, 0);
}
```

3. Flowchart figure for function `SEG_clk_2us()` which generates one clock period on `SEG_CLK` pin with a duration of 2&nbsp;us. The image can be drawn on a computer or by hand. Use clear descriptions of the individual steps of the algorithms.

   ![your figure](Images/diagram.jpg)


### Kitchen alarm

Consider a kitchen alarm with a 7-segment display, one LED and three push buttons: start, +1 minute, -1 minute. Use the +1/-1 minute buttons to increment/decrement the timer value. After pressing the Start button, the countdown starts. The countdown value is shown on the display in the form of mm.ss (minutes.seconds). At the end of the countdown, the LED will start blinking.

1. Scheme of kitchen alarm; do not forget the supply voltage. The image can be drawn on a computer or by hand. Always name all components and their values.

   ![your figure](Images/alarm.png)
