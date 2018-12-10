# Chapter 0.3 - Source Code And Machine Code

## Grammar - 'Code'

Before I say anything else I want to make something clear.  
'Code' in the context of programming is primarily an _uncountable_ noun.  

Being _uncountable_ means this:  

* You cannot have '1 code' or '2 codes', or even 'a code'. (Code cannot be counted.)
* You can have 'some code' or 'lots of code' or 'a bit of code' or 'a piece of code'.

It drives me batty every time I see someone ask "can I have a code to do this?".  
Saying 'a code' is not just grammatically incorrect, it screams "I have no clue how to program" and frankly makes you look stupid.  

The relevant definition of 'code' taken from wiktionary:

> (programming, uncountable) Instructions for a computer, written in a programming language; the input of a translator, an interpreter or a browser, namely: source code, machine code, bytecode. 

Some usage examples taken from Wiktionary:

> Object-oriented C++ code is easier to understand for a human than C code. 
> I wrote some code to reformat text documents. 
> This HTML code may be placed on your web page. 

The other primary use case of 'code' is as a verb, 'to code', which can be summed up as 'to write code' or 'to program'.  
There's no special treatment here.  

## Source Code Versus Machine Code

To put it simply (and slightly naively), source code is what a human writes and machine code is what a computer reads.  

### Machine Code

All computers have a thing called a processor.  
In a desktop or laptop computer it's usually called a 'Central Processing Unit' (CPU), and on an embedded system (e.g. the Arduboy) it's often referred to as a microprocessor or a 'MicroController Unit' (MCU).  
Honestly I don't know why there are so many different terms for what essentially performs the same role.  
I'm going to stick to calling it a CPU or processor for the sake of simplicity.  

The CPU has a set of different operations that it can perform.  
Each of these operations is refered to as an 'instruction' and the set of all instructions that a CPU can perform is (conviniently) called its instruction set.  

These instructions are what people are referring to when they say 'machine code'.  
I won't go into detail about how these work, but essentially they are really tiny operations.  
Most of the time they do tiny things like move data around and add numbers together.  

Programs are formed by combining hundreds of these tiny little instructions together to create much larger sets of instructions that are capable of performing complex tasks.  

But these operations are so tiny and so tedious that it's difficult to write programs using them.  
You certainly could write a program in pure machine code if you wanted to, it's actually not that difficult to understand machine code, but the real reason nobody does it is because it is monumentally tedious to do so.  

**Terminology**

Note that a computer or CPU can be said to either 'run' code or 'execute' code.  
E.g. 
* "While an intel CPU is executing code, it can get quite hot, which is why desktops have large fans."  
* "And then you run the code to see what it does."  

You will see both of these words used a lot so it's important that you're familiar with them.  

### Source Code

That is where assembly comes in.  
Assembly is a human-readable language that can be translated into machine code.  

Often the assembly language will have a near 1 to 1 correlation between assembly instructions and machine code instructions.  
Sometimes an assembly instruction will compile to different machine code instructions depending on the syntax used, or two assembly instructions will actually compile to the same machine code instruction.  
Overall assembly is very close to machine code and is only a minor step up in the sense that it's easier to read and understand.  

By the dictionary definition of 'source code', assembly is a kind of 'source code' because it's a human readable language that can be translated into machine code.  

Often though, when people say 'source code' they're thinking of languages that are further abstracted from the machine language.  
In practice, 'source code' is reserved for languages that can be translated into different kinds of machine code, which usually discounts assembly.  

After assembly, you reach the next level of language, which is something like C or C++.  
It is human readable and can be translated into machine code for lots of different kinds of processors,  
but the way it's formatted is quite far removed from how the machine code actually works.  
Often you end up describing a more abstract process rather than the tiny details.  
This is the kind of language that people typically label as 'source code'.  

## Compiling

Compiling is the process by which source code is translated into machine code.  
It is a long and complicated one that I won't discuss in detail until a later chapter, so don't worry about the details.  
Also the thing that does the compiling is a program called a compiler, in case that wasn't obvious.  

**Fun facts**

Most modern compilers were in fact compiled on a compiler.  
Sometimes a compiler is used to compile its own source code, producing the same compiler - this is called 'bootstrapping' the compiler.

The compiler was invented by rear admiral Grace Brewster Murray Hopper in the 1950s.  
She wanted to be able to write programs in plain English despite her coworkers telling her that computers could only do arithmetic and couldn't understand English.  
Eventually she proved them wrong.  

Unfortunately one of the languages she helped to create was the dreaded COBOL.  
To quote Edsger Dijkstra:  
> The use of COBOL cripples the mind; its teaching should, therefore, be regarded as a criminal offense.

## Grammar - 'Assembly'

Lastly, I'd like to take this opportunity to state that the language is explicitly _not_ 'assembler'.  
I don't know why so many people try to call the language 'assembler', but it is technically incorrect to do so (in English).  

The language is 'assembly' and the program that translates 'assembly' into machine code is called an 'assembler'.  
The process itself is often called 'assembling' a program or the 'assembly' of a program.

The only excuse for getting these mixed up is if you're Swedish.  