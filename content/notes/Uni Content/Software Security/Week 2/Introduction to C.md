---
title: Introduction to C
---
# Memory Structure

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221185052.png)
As data is added to the stack, the memory addresses decrease
As data is added to the heap, the memory addresses increase

![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221185232.png)
![|400](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230221185315.png)
After overflowing the buffer, on re-entry, the code will try to jump back to a possibly illegal address causing a Segmentation Fault and a crash