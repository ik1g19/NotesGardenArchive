A **system** may be defined as a device that performs a an operation on a signal

Analogue to digital is an example of continuous to discrete conversion

Compressor is an example of non-linear system
- Changes the slope

Time variant system - E.g. loudspeaker

Typically assume things are time invariant and linear

Mathematical operations are time invariant

SISO - Single Input Single Output
SIMO - Single Input Multiple Output
MIMO - Multiple Input Multiple Output

**HRTF**

Causality - 

Non-causality - Can look ahead further into the input to the function, responding before the signal has arrived

Makes sense to think about non-causal systems, but when implementing you need to implement a causal system

System stability - Bounded input should have a bounded output i.e. Input up to a certain threshold should have output up to a (different) threshold

System has memory if its output depends on the past
- A non-causal system will 'remember' the future

Static system - A system without memory

A one pixel kernel is an example of a static system as the output depends solely on that one pixel input

Classification of Systems
- Continuous time and discrete time
- Linear
- Time variant or time invariant
- With and without memory
- Causality
- Stability

# Impulse Response

![[notes/System Theory/Images/Pasted image 20230714145042.png|400]]

If the frequency changes then the system is non-linear

Distorting system - Non-linear


![[notes/System Theory/Images/Pasted image 20230714150604.png|400]]

Stable system as the signal decays
System has memory as 1 second after the initial signal it is still going so it remembers

Loss of acoustic propagation from signal processing to physics - energy is lost through heat conversions

All IIRF have a feedback path

The impulse response is the representation of the system memory

Quick decay tells us how quickly it forgets

# Convolution

![[notes/System Theory/Images/Pasted image 20230714151831.png|400]]

# Convolutional Theorem

![[notes/System Theory/Images/Pasted image 20230714153035.png|400]]

# Circular Convolution

![[notes/System Theory/Images/Pasted image 20230714154240.png|400]]

# Digital Filters

![[notes/System Theory/Images/Pasted image 20230714160931.png|400]]

FIR are always stable - IIR always have a big risk of instability

## FIR Filters

![[notes/System Theory/Images/Pasted image 20230714161307.png|400]]

## IIR Filters

![[notes/System Theory/Images/Pasted image 20230714161429.png|400]]

