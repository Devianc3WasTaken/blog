**[Home](https://devianc3wastaken.github.io/blog/)**

## Microcorruption Level - Sydney

The second level on the Microcorruption CTF is the Sydney level.

This one is super easy but also easy to miss if you're new.
The main function is rhe "check_password" function. So we break to that and step through it.

The function has multiple cmp's (compares) inside of it so let's analyse it one by one.

The first one checks if the first 2 bytes are equal to 2f54 (which is /T in ASCII), so that's the first 2 characters of the password. So let's reset the program and enter that in to see if we pass through that cmp.

Aaaand we don't pass. This can be extremely frustrating if you don't know what to look out for. But this is why I'm here =)

The processor of this system is a MSP430. 

Which is Little Endian (which is the opposite of what we use on our PC's which is Big Endian) so the bits are going in opposite way that we are used to. And if you think about it, that must mean that the cmp isn't seeing if you entered "/T", it's actually the other way round "T/" or 542f in hex.

Entering that grants us past that cmp and we go to the next one. Since each cmp is essentially the same process as the previous, we just do the same thing over and over again until we have done them all which we end up with:

		542f 402a 415a 635c

Which is the correct answer! And we have solved this level, the only catch of this level and the only thing that could mess you up is not realising that the CPU is Little Endian so everything needs to be reversed.