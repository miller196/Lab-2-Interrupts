# Button Interrupt
Last lab you were introduced to the idea of "Polling" where in you would constantly check the status of the P1IN register to see if something has changed. While your code may have worked, it ends up spending a ton of time just checking something that has not changed. What we can do instead is use another two registers available to us from the GPIO peripheral, P1IE and P1IES, to allow our processor to just chill out and wait until something happens to act upon it. Without spending too much space on this README with explanations, what makes these interrupts tick is the following code:

```c
#pragma vector=PORT1_VECTOR
__interrupt void Port_1(void)
{
}
```

While you still need to initialize the Ports to be interrupt enabled and clear the flags, this "Pragma Vector" tells the compiler that when a particular interrupt occurs, run this code.

## Interrupts and Polling
### Polling
In the previous examples with the button, we have been using a technique called *polling* where you are constantly checking if the button is pressed or not. Polling works very well with the classic types of programing you have done in the past. For example, describing code as:
- Check the button state
- If button is pressed, do something
- Else if button is not pressed, do something else
- Do some other things and start over again
Every time we go through the loop, you are polling or checking the input pin state. This seems ok, but consider that you also have a _100ms delay_ in your loop for blinking the LEDs.

What happens if you press the button faster than 100ms, or something quick happens? You probably will miss the input, which is kinda the whole point of the code.

So then what can we do?

### Interrupts: "Tell me when the button is pressed"
Microcontrollers have the ability for the peripherals within them to generate an Interrupt Signal. Think of the processor as a teacher, and the peripherals as students. As the processor is teaching, it wants to know if anyone has a question it should stop and address. When *polling*, this is essentially as if the teacher points to each student and asks them if they have a question every so often. You could imagine that this is a lot of time possibly wasted, as there is a good chance at most, maybe a student might ask something.

*Interrupts* are like students raising their hands. Think about being in a classroom and having a question, what do you do? You raise your hand. The processor can then decide how it wants to _handle_ the interrupt. Should it stop immediately? Or do they need to finish a thought or sentence, then they can address the student. 
