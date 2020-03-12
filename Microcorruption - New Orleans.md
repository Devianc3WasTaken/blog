## Microorruption Level - New Orleans

The first level on the Microcorruption CTF is the New Orleans level.

We need to find out the password in order to unlock the vault and solve the puzzle.
Lets start by looking at the main function which the program starts at:
![Screenshot from 2020-03-12 11-25-22.png]({{site.baseurl}}/Screenshot from 2020-03-12 11-25-22.png)

We can see a function called "check_password" which seems the most interesting one so should set a breakpoint for that function and step through it to see if we have anything interesting in the registers or memory (which in the best case scenario would have the password).

To get to that function, let's just enter a bogus password. I have entered "password" as my password to get to that function:![Screenshot from 2020-03-12 11-29-21.png]({{site.baseurl}}/Screenshot from 2020-03-12 11-29-21.png)

We can also see that in the register "R15", it contains the memory address for the password that I have entered
![Screenshot from 2020-03-12 11-30-11.png]({{site.baseurl}}/Screenshot from 2020-03-12 11-30-11.png)
![Screenshot from 2020-03-12 11-30-20.png]({{site.baseurl}}/Screenshot from 2020-03-12 11-30-20.png)

Stepping through the function, we move the memory address from r15 to r13 and we keep stepping until we come across a very interesting instruction 

		cmp.b	@r13, 0x2400(r14)

This instruction compares the first byte (hence the name cmp.b) between the value stored in r13 and the value of r14 + the offset of 0x2400. Because the memory address in r14 is 0x0000, the value of it will be 0x2400.

We run the command:

		r 2400

to see what is inside the memory address of 0x2400
