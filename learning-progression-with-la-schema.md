# CPE 1040 - Fall 2020

This is learning progression 004 for the Fall 2020 installment of the course CPE 1040: Introduction to Computer Engineering at MSU Denver.

Table of Contents
=================

* [CPE 1040 \- Fall 2020](#cpe-1040---fall-2020)
  * [Learning Progression 004: External LEDs](#learning-progression-004-external-leds)
    * [Step 1: Binary](#step-1-binary)
      * [1\. Study](#1-study)
        * [Positional numeral systems](#positional-numeral-systems)
        * [Unsigned integers](#unsigned-integers)
        * [Finite bit width](#finite-bit-width)
        * [Primitive data types revisited](#primitive-data-types-revisited)
        * [Signed integers](#signed-integers)
        * [IEEE 754 floating point](#ieee-754-floating-point)
      * [2\. Apply](#2-apply)
      * [3\. Present](#3-present)

## Learning Progression 004: External LEDs

This progression introduces fundamentals of computing, including the binary system of data representation as well as the basics of memory and processing. We introduce assembly language in the context of a minimal instruction set processor. This is where the lowest layer of the software stack and the highest layer of the hardware stack coexist, and where user programs are translated into machine code and executed by the processor one instruction at a time. This is also the level of computing which directly correpsonds to the simplest theoretical models of a computer. We also introduce the input-output capabilities of the micro:bit and build an external circuit to serve as an extension to the built-in 5x5 LED matrix to run our Screensavers program on.

### Step 1: Binary   
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### Positional numeral systems
[[toc](#table-of-contents)]

`[<lernact-rd>]`The most widely used number system is `[<cept>]`_decimal_. What does "decimal" actually mean? Let us list the obvious:
1. [Decimal](https://www.etymonline.com/word/decimal) means 10.  
2. The decimal system has 10 symbols, called `[<cept>]`_digits_: 0, 1, 2, 3, 4, 5, 6, 7, 8, 8, 9.  
3. It's popularity tends to be attributed to the fact that humans have 10 digits on their hands and they learned to count on them in prehistoric times.  

Some aspects that are less obvious (mostly because they have become deeply habitual) are:
1. The name "decimal" indicates the `[<cept>]`_base_ of the number system, which is 10. Note that the base is the _highest digit plus 1_, which has to do with the fact that 0 is the first digit.      
2. Every number expresses a sum of `[<cept>]`_powers_ of the base 10. For example, the number 359 unequivocally means _three-hundred-and-fifty-nine_, or <img src="https://render.githubusercontent.com/render/math?math=3 * 10^2 %2B 5 * 10^1 %2B 9 * 10^0">. Any decimal number can be expressed like this. Note that any number raised to the power 0 is, by definition, equal to 1.  
3. The powers of the base are equal to the indices of the digit positions, counting _from right to left starting at 0_. For example, 
   ```
   Digits     359
   Indices    210
   ```
   The position of a digit immediately tells us whether it represents _ones_. _tens_, _hundreds_, _thousands_, _ten-thousands_, etc.  

What all of this means is that the decimal number (aka `[<cept>]`_numeral_) system is just one example of `[<cept>]`_positional_ number systems. In contrast, the [Roman numeral system](https://en.wikipedia.org/wiki/Roman_numerals) is _not_ positional. For example, consider the numbers <img src="https://render.githubusercontent.com/render/math?math=IX"> (9 in decimal) and <img src="https://render.githubusercontent.com/render/math?math=XI"> (11 in decimal).

**Question 1.1.1:** Why are the Roman numerals not a positional number system?    

The `[<cept>]`[_binary_](https://en.wikipedia.org/wiki/Binary_number) number system (_binary_, for short) is another positional numeral system.

**Question 1.1.2:** What is the base of binary?  
**Question 1.1.3:** What are the symbols of binary? How are they called?     
**Question 1.1.4:** Express the binary number <img src="https://render.githubusercontent.com/render/math?math=10101"> as a sum of powers of the base.  
**Question 1.1.5:** What does <img src="https://render.githubusercontent.com/render/math?math=10"> represent in binary?  

##### Unsigned integers
[[toc](#table-of-contents)]

`[<lernact-rd>]`The simplest data type in computing is the `[<cept>]`_unsigned integer_. "Unsigned" means `[<cept>]`_non-negative_. "Integer" means `[<cept>]`_whole number_. Here are the first 16 unsigned integers, in both decimal and binary:
Decimal | Binary
-- | --
<img src="https://render.githubusercontent.com/render/math?math=0_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=0_{2}">
<img src="https://render.githubusercontent.com/render/math?math=1_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1_{2}">
<img src="https://render.githubusercontent.com/render/math?math=2_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=10_{2}">
<img src="https://render.githubusercontent.com/render/math?math=3_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=11_{2}">
<img src="https://render.githubusercontent.com/render/math?math=4_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=100_{2}">
<img src="https://render.githubusercontent.com/render/math?math=5_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=101_{2}">
<img src="https://render.githubusercontent.com/render/math?math=6_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=110_{2}">
<img src="https://render.githubusercontent.com/render/math?math=7_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=111_{2}">
<img src="https://render.githubusercontent.com/render/math?math=8_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1000_{2}">
<img src="https://render.githubusercontent.com/render/math?math=9_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1001_{2}">
<img src="https://render.githubusercontent.com/render/math?math=10_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1010_{2}">
<img src="https://render.githubusercontent.com/render/math?math=11_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1011_{2}">
<img src="https://render.githubusercontent.com/render/math?math=12_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1100_{2}">
<img src="https://render.githubusercontent.com/render/math?math=13_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1101_{2}">
<img src="https://render.githubusercontent.com/render/math?math=14_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1110_{2}">
<img src="https://render.githubusercontent.com/render/math?math=15_{10}"> | <img src="https://render.githubusercontent.com/render/math?math=1111_{2}">

In programming, a binary number is written with the prefix `0b`. For example, `0b1` and `0b0001` both represent <img src="https://render.githubusercontent.com/render/math?math=1_{2}">. 

**Question 1.1.6:** What are the `[<cept>]`_bit patterns_ for <img src="https://render.githubusercontent.com/render/math?math=333_{10}">, <img src="https://render.githubusercontent.com/render/math?math=1000000_{10}">, and <img src="https://render.githubusercontent.com/render/math?math=17181920_{10}">? Use the following function on the micro:bit simulator and/or device:
```javascript
// Example 1.1.1

/**
 * Converts an unsigned decimal integer to a binary bit pattern string.
 * 
 *           Quotient     Remainder   Condition          Result
 *   3 : 2 = 1.5  ------> 1           Q > floor(Q)       11
 *   1 : 2 = 0.5  ------> 1           floor(Q) == 0 
 *
 *   2 : 2 = 1.0  ------> 0           Q == floor(Q)      10
 *   1 : 2 = 0.5  ------> 1           floor(Q) == 0
 *
 * @param dec unsigned decimal integer
 */
function toUnsignedBinaryString(dec : number) : string {
    let bin_array : number[] = []
    let quotient : number = dec
    let no_fraction : number

    while (true) {
        quotient /= 2
        no_fraction = Math.floor(quotient)
        if (quotient > no_fraction)
            bin_array.insertAt(0, 1)
        else
            bin_array.insertAt(0, 0)
        if (no_fraction == 0) break
        quotient = no_fraction
    }

    return '0b' + 
           bin_array.map(
               (value: number, index: number) => 
               { return value.toString(); }
               ).join('')
}
```

##### Finite bit width   
[[toc](#table-of-contents)]

`[<lernact-rd>]`A bit pattern of _any length_ can represent an unsigned integer. However, computers represent unsigned integers of `[<cept>]`_fixed bit width_, which is a power of 2. The most widely used bit widths are 8, 16, 32, 64, and 128. For example, here is the number <img src="https://render.githubusercontent.com/render/math?math=172_{10}"> in 8 bits, 16 bits, and 32 bits:
Bit width | Bit pattern
-- | --
8 | `0b10101100`
16 | `0b0000000010101100`
32 | `0b00000000000000000000000010101100`

The micro:bit has 32-bit unsigned integers.

**Question 1.1.6:** What is the bit pattern of the largest unsigned integer that can be represented in the micro:bit?  

Finite bit-width means a limit on the largest number that can be represented. If a number is larger than the largest number that can be represented in the available number of bits, it `[<cept>]`_overflows_.

**Question 1.1.8:** Will <img src="https://render.githubusercontent.com/render/math?math=653_{10}"> overflow in 8-bit binary?   

##### Primitive data types revisited
[[toc](#table-of-contents)]

The unsigned integer is one of the `[<cept>]`_primitive_ data types, along with _signed integers_, _floating-point numbes_, and _booleans_. A data type is primitive if it is represented in a `[<cept>]`[_word_](https://en.wikipedia.org/wiki/Word_(computer_architecture)). More on this when we tackle memory addressing and processor arithmetic in later steps.

**Question 1.1.9:** What is the word size of the micro:bit? _Hint: There are three ways to tell: (i) Reread the last two sections carefully; (ii) In the Wikipedia page, look at the table and find ARMv6-M, the architecture of the micro:bit processor; and (iii) Skim-read the [hardware overview](https://tech.microbit.org/hardware/1-5-revision/) documentation page for the micro:bit._  

##### Signed integers
[[toc](#table-of-contents)]

`[<lernact-rd>]``[<cept>]`_Signed integers_ are integers that can be negative and non-negative.

**Question 1.1.10:** How many different numbers can we represent with 4-bit binary patterns?  

There are several [ways](https://en.wikipedia.org/wiki/Signed_number_representations) we can represent negative numbers. Here are examples with 4-bit numbers:
1. _Sign and value._ For example, if `0b0011` represents <img src="https://render.githubusercontent.com/render/math?math=%2B 3">, then  <img src="https://render.githubusercontent.com/render/math?math=- 3"> will be represented by `0b1011`. The leftmost bit is used as a sign, with 0 representing + and 1 representing -. The problem with this representation is that it complicates computer arithmetic in `[<cept>]`_hardware_.      

2. _One's complement_. For example, <img src="https://render.githubusercontent.com/render/math?math=- 3"> will be represented by `0b1100`. The bits are just flipped. The problem with this representation is that it ends up with two different zeros: `0b0000` represents <img src="https://render.githubusercontent.com/render/math?math=%2B 0"> and `0b1111` represents <img src="https://render.githubusercontent.com/render/math?math=- 0">.  
3. [_Two's complement_](https://en.wikipedia.org/wiki/Two%27s_complement). This is the representation of choice for modern computers because it eliminates the problems of the previous two. For example, <img src="https://render.githubusercontent.com/render/math?math=- 3"> is represented by `0b1101`.  

Here is a short table of 2-bit numbers in decimal and the three binary representations (note that with 2 bits we can represents only 4 different numbers):
Decimal | Sign and value | 1s complement | 2s complement
-- | -- | -- | --
<img src="https://render.githubusercontent.com/render/math?math=%2B 1"> | `0b01` | `0b01` | `0b01`
<img src="https://render.githubusercontent.com/render/math?math=%2B 0"> | `0b00` | `0b00` | `0b00`
<img src="https://render.githubusercontent.com/render/math?math=- 0"> | `0b10` | `0b11` | n/a
<img src="https://render.githubusercontent.com/render/math?math=- 1"> | `0b11` | `0b10` | `0b11`
<img src="https://render.githubusercontent.com/render/math?math=- 2"> | n/a | n/a | `0b10`

The signed integer is also a primitive type.

**Question 1.1.11:** If we can represent 32 different signed integer numbers, what is the largest (by absolute value) negative number that we can represent?  

##### IEEE 754 floating point  
[[toc](#table-of-contents)]

`[<lernact-rd>]`There are many different ways to represent `[<cept>]`_real_ numbers in binary, but the established standard is the [IEEE 754 format](https://en.wikipedia.org/wiki/Single-precision_floating-point_format). The full coverage of this standard is beyond the scope of this learning progression, so we will point out the most important elements:

1. The standard is based on the `[<cept>]`[_scientific notation_](https://www.mathsisfun.com/numbers/scientific-notation.html) for real numbers. For example:  
   1. The decimal real number <img src="https://render.githubusercontent.com/render/math?math=- 300.498"> will be written in scientific notation as <img src="https://render.githubusercontent.com/render/math?math=- 3.00489 * 10^2">. 
   2. For binary, analogously, the number <img src="https://render.githubusercontent.com/render/math?math=- 101.011"> will be written in scientific notation as <img src="https://render.githubusercontent.com/render/math?math=- 1.01011 * 2^2">. _Note that, for clarity, we follow the convention for writing the base and power in decimal!_   
   3. Finally, the number <img src="https://render.githubusercontent.com/render/math?math=0.00010101"> will be represented in scientic notation as <img src="https://render.githubusercontent.com/render/math?math=1.0101 * 2^{-4}">.  

2. The type is called "_floating_ point" precisely because the exponent can take a large range of signed integers, as shown in the examples above, which allows the fractional point to "float". In contrast, reals can be represented in `[<cept>]`_fixed-point_ format, as well, thought his format has narrower application.  

3. The `[<cept>]`_single-precision_ floating point is a primitive type represented in 32 bits. The `[<cept>]`_double-precision_ floating point is a primitive type represented in 64 bits.  

4. In either precision, the bit pattern is split in 3 sections, representing (with bit widths shown for single-precision) as follows:

   1. (1 bit) The sign, either 0 (+) or 1 (-). For the first binary example above, this bit woulb be 1.    

   2. (8 bits). The `[<cept>]`_exponent_ (that is, the power). The exponent is represented in an `[<cept>]`_offset_ form (aka `[<cept>]`_excess_, aka `[<cept>]`_bias_) where 127 is added to the actual exponent (aka _excess-127_). In the first binary example, the 8-bit exponent in our example above will be <img src="https://render.githubusercontent.com/render/math?math=127_{10} %2B 2_{10} = 129_{10} = 10000001_{2}">. This offset form converts the signed number representing the exponent (we saw that the exponent can be both negative and non-negative) into an unsigned number, which helps with `[<cept>]`_sorting_ floating-point numbers.  
   
   3. (23 bits) The `[<cept>]`_significand_ (aka `[<cept>]`_mantissa_), which consists of the bits _after_ the `[<cept>]`_binary point_ (aka fractional point). In the first binary example, the fractional bit pattern is going to be `01011000000000000000000`. Note that because in scientific notation a binary number always has a 1 bit to the left (aka in front) of the fractional point, it is omitted from the representation.    

5. Floating-point numbers are `[<cept>]`_inexact_. Because the significand has only 23 bits, any further precision is lost and rounded. Real numbers are `[<cept>]`_uncountably infinite_, but we can only represent a finite number of them.  

**Question 1.1.12:** Why would it be easier to sort binary floating-point numbers with the exponent represented as an _unsigned integer_ rather than a _signed integer_? _Hint: In an ascending order, 0 sorts above 1, but signed integers that start with 1 are all smaller than any signed integer that starts with 0._

#### 2. Apply
[[toc](#table-of-contents)]

1. `[<lernact-prac>]`Explain in detail (line by line) what the function in Example 1.1.1 does and why.    

2. `[<lernact-prac>]`Write a function that converts a _binary pattern string_, like `01011001`, to a decimal number (which will be 89 in this case).  _Hint: Sum of powers of the base, with a judicious choice of [string methods](https://www.tutorialspoint.com/typescript/typescript_strings.htm), which can be found under the **Text** bar in the **Advanced** section of the MakeCode menu._  

3. `[<lernact-prac>]`**[Optional challenge, max 10 extra step points]** Write a program with the following functions and types:
   1. Function `asUnsigned` to interpret an 8-bit binary pattern string as an unsigned integer and return the decimal equivalent.  
   2. Function `asOnesComp` to interpret an 8-bit binary pattern string as a 1s-complement signed integer and return the decimal equivalent.  
   3. Function `asTwosComp` to interpret an 8-bit binary pattern string as a 2s-complement signed integer and return the decimal equivalent.  
   4. Function `asUnsignedAny` to interpret a binary pattern string of arbitrary bit length as an unsigned integer and return the decimal equivalent.  
   5. Function `asOnesCompAny` to interpret a binary pattern string of arbitrary bit length as a 1s-complement signed integer and return the decimal equivalent. _Note: You will need to assume that the bit width is the smallest power of 2 larger or equal to the number of bits in the argument. You will need to read up on [sign extension](https://en.wikipedia.org/wiki/Sign_extension)._      
   6. Function `asTwosCompAny` to interpret a binary pattern string of arbitrary bit length as a 2s-complement signed integer and return the decimal equivalent. _See the note above._    
   7. Enumerated type `NumberRep` for the three different representations: `Unsigned`, `OnesComp`, and `TwosComp`.  
   8. Enumerated type `BitWidth` for the two cases of bit width in the above functions: `8` and `Any`.  
   9. Function `interpretBinary (pattern : string, repr : NumberRep, width : BitWidth)` to collect all functions in one.  

4. `[<lernact-prac>]`**[Optional challenge, max 3 extra step points]** Write a function `toScientific` that takes a real number and shows (that is, scrolls) it on the micro:bit screen in decimal scientific notation.  

5. `[<lernact-prac>]`**[Optional super challenge, max 16 extra step points]** Derive the 2s-complement representation of signed binary integers. Recommended progression:
   1. Realize that with any fixed number of bits, you can only represent so many different numbers.  
   2. Represent the unsigned integers for a bit width of your choice (4+ recommended, power of 2 recommended).  
   3. Now that you have all the patterns listed in a particular order, find one feature that splits the set in two, with all other features the same. _Hint: The two sets should easily convert from one to the other using a bitwise operation._    
   4. One of the sets would obviously remain to represent the same non-negative numbers as before the split. The other can now be used to represent the negative numbers.   
   5. How will you order the two sets so that they are symmetric through application of the bitwise opration from (3)?  
   6. At this point, you should have arrived at 1s-complement signed integers of the bit width you chose in (2). Point out the problem with it.  
   7. The foremost design principles for a number representation is that it is _arithmetically correct_ and _computationally cheap_. How would you fix the problem you pointed out in (6) in accordance to these principles. _Hint: Flipping a bit is cheap. Adding 1 to a number is cheap._  
   8. Show the sequence of _cheap_ operations that will _correctly_ compute 95<sub>10</sub> - 37<sub>10</sub>, in 2s-complement binary. _Hint: The silent overflow is a feature, not an error!_  

#### 3. Present
[[toc](#table-of-contents)]

In the [programs](programs) directory:
1. Add your program from 1.2.2 with filename `microbit-program-1-2-2.js`.  
2. Add your program from 1.2.3 with filename `microbit-program-1-2-3.js`.  
3. Add your program from 1.2.4 with filename `microbit-program-1-2-4.js`.  

In the [Lab Notebook](README.md):

1. Answer question 1.1.1.  
2. Answer question 1.1.2.  
3. Answer question 1.1.3.  
4. Answer question 1.1.4.  
5. Answer question 1.1.5.  
6. Answer question 1.1.6.  
7. Answer question 1.1.7.  
8. Answer question 1.1.8.  
9. Answer question 1.1.9.  
10. Answer question 1.1.10.  
11. Answer question 1.1.11.  
12. Answer question 1.1.12.  
13. Write you narrative for the program explanation from 1.2.1.  
14. Link to the program from 1.2.2.  
15. Link to a demo video showing the execution of the program from 1.2.2.  
16. Link to the program from 1.2.3.  
17. Link to a demo video showing the execution of the program from 1.2.3.  
18. Link to the program from 1.2.4.  
19. Link to a demo video showing the execution of the program from 1.2.4.  
20. Write you narrative for the derivation from 1.2.5.  
