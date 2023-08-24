---
title: Buffer Overflow
---
In this example the buffer is filled with 0x41 values (65 decimal,  or ASCII 'A')
![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315193531.png)

# Execution

```
gcc -o vuln vuln.c               //compiles
gdb ./vuln                       //runs the program vuln inside gdb
run $(repeat 511 printf 'A')     //puts 511 'A' in argv[1] + terminator \0
```
```C
#include <stdio.h>
#include <string.h>

int main (int argc, char** argv)
{
	char buffer[512];
	strcpy(buffer, argv[1]);
	
	return 0;
}
```

The 511 'A' will be copied into the buffer

![|650](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315195239.png)

![|650](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315195412.png)

![|650](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315195502.png)

![|650](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315195714.png)

## Overflowing the Buffer

When writing **539** bytes there is a segmentation fault

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315195826.png)

Half of the return register is now filled with 0x41 bytes that make it point to a non-permitted memory space

```
gdb ./vuln                        //runs the program vuln inside gdb
run $(repeat 539 printf 'A')      //puts 539 'A' in argv[1] + \0
```
```C
#include <stdio.h>
#include <string.h>

int main (int argc, char** argv)
{
	char buffer[512];
	strcpy(buffer, argv[1]);

	return 0;
}
```

The 531 'A' will be copied into the buffer

The 'A' chars overflowing the buffer will go to `RBP` (when it is popped) and cover half of `RIP` upon return

![|650](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315201027.png)

**Checking the Registers**
![|300](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315201156.png)

---

When writing **544** bytes there is another segmentation fault

![|500](notes/Uni%20Content/Software%20Security/Images/Pasted%20image%2020230315202315.png)

All of the return address is now filled with `0x41` bytes that make it point to a non-permitted memory space

```
gdb ./vuln                        //runs the program vuln inside gdb
run $(repeat 544 printf 'A')      //puts 544 'A' in argv[1] + \0
```
```C
#include <stdio.h>
#include <string.h>

int main (int argc, char** argv)
{
	char buffer[512];
	strcpy(buffer, argv[1]);

	return 0;
}
```

The 544 'A' will be copied into the buffer
The 'A' chars overflowing the buffer will go to `RBP` (when popped) and to `RIP` upon executing return 0