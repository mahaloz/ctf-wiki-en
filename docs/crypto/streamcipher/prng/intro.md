# pseudo random number generator introduction


## Overview


A pseudorandom number generator (PRNG), also known as a deterministic random bit generator (DRBG), is an algorithm used to generate a digital sequence** close to an absolute random number sequence. . In general, a PRNG relies on an initial value, also called a seed, to generate a corresponding pseudo-random number sequence. As long as the seed is determined, the random number generated by the PRNG is completely determined, so the sequence of random numbers it generates is not truly random.


For now, PRNG plays an important role in many applications, such as simulation (Monte Carlo method), e-sports, and password applications.


## Randomness of rigor


- Randomness: Random numbers should be free of statistical bias and are completely messy series.
- Unpredictability: The next occurrence cannot be inferred from the past sequence.
- Non-reproducibility: The same sequence cannot be reproduced unless the sequence is saved.


The stringency of these three properties increases in turn.


In general, random numbers can be divided into three categories.


| Category | Randomness | Unpredictability | Non-reproducibility |
| :--------: | :----: | :--------: | :--------: |

| Weak pseudo-random number | ✅ | ❌ | ❌ |
| Strong pseudo-random number | ✅ | ✅ | ❌ |
| Real random number | ✅ | ✅ | ✅ |


In general, the random number used in cryptography is the second.


## Cycle


As we said before, once the seed that the PRNG depends on is determined, the sequence of random numbers generated by the PRNG is basically determined. The period in which the PRNG is defined here is as follows: For all possible starting states of a PRNG**, the longest length of the sequence is not repeated. Obviously, for a PRNG, its period will not be greater than all its possible states. However, it should be noted that not when we encounter repeated output, we can consider it to be the period of the PRNG, because the state of the PRNG is generally greater than the number of bits of the output.


## evaluation standard


See Wikipedia, https://en.wikipedia.org/wiki/Pseudorandom_number_generator.


## Categories


Currently, the common pseudo-random number generator mainly has


- Linear Congruence Generator, LCG
- Linear regression generator
- [Mersenne Twister] (https://en.wikipedia.org/wiki/Mersenne_Twister)
-   [xorshift](https://en.wikipedia.org/wiki/Xorshift) generators

-   [WELL](https://en.wikipedia.org/wiki/Well_Equidistributed_Long-period_Linear) family of generators

- Linear feedback shift register, LFSR, linear feedback shift register


## problem


In general, pseudo-random number generators may have the following problems


- In the case of some seeds, the period of the generated random number sequence will be smaller.
- Uneven distribution when generating large numbers.
- The continuous values are closely related, and the subsequent values are known, and the previous values can be known.
- The value of the output sequence is very uneven.


## Reference


https://en.wikipedia.org/wiki/Pseudorandom_number_generator