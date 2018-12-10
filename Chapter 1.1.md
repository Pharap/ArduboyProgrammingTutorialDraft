# Chapter 1.1 - Hello World

## What Is 'Hello World'?

A "hello world" program is a simple program for putting text onto a screen.  
The purpose of a "hello world" program is to act as a simple demonstration of what the language looks like.  

## The Program

Here is 'hello world' for Arduboy.

```cpp
#include <Arduboy2.h>

Arduboy2 arduboy;

void setup(void)
{
	arduboy.begin();
}

void loop(void)
{
	if(!arduboy.nextFrame())
		return;
	
	arduboy.pollButtons();
	
	arduboy.clear();
	
	arduboy.print(F("Hello world"));
	
	arduboy.display();
}
```

I have purposely not provided the simplest version of 'hello world', because the simplest possible 'hello world' looks nothing like an Arduboy game.
Instead I have written a 'hello world' that follows the basic structure that most good Arduboy games follow.

At the moment you will probably not understand much of this, but you will do eventually.

## Compiling

Before you understand the code, you must first be able to compile, upload and run code.
If you cannot compile a program then you won't know whether it works or not.

## Explaining The Program

I will now explain, line by line, what each part of the program does.  

For the moment I expect that much of this will be confusing, but that's ok.  
Later on you will be able to refer back to this code and understand it better, so it doesn't matter if bits don't make sense yet.  
The most important thing to take away from this is that every line of code has a purpose and a meaning.  

One of the hardest things about programming is that there's a lot of interdependence between different concepts.  
Sometimes you'll end up with just a vague idea of what each thing is and you'll have to slowly refine that idea by watching how the different concepts interract.  

```cpp
#include <Arduboy2.h>
```

This line includes the `Arduboy2` library.

Arduboy2 is what's called a 'library' (more formally a 'programming library' or a 'software library').  
A 'library' is a collection of pre-written code that serves a specific purpose.  

In this case the Arduboy2 library provides much of the functionality needed to interact with the hardware of the Arduboy without having to worry about the intricate details of the hardware.  
Obviously you still need to know the limitations of the hardware, but you don't have to worry things like what kind of commands the screen responds to or which output pins are connected to which individual piece of hardware.  

To be able to use a library you often need to 'include' it. Usually there are one or two 'header' files (typically with a `.h` suffix) that you must include to get access to that library's features.  
Don't worry too much about how including works for now, just remember that libraries need to be included to be usable.  

```cpp
Arduboy2 arduboy;
```

This line creates an object of the `Arduboy2` class.

For now do not worry too much about what an object is or what a class is.  
The important thing to take away from this part is that the `arduboy` object will be the thing that we use to interact with the Arduboy.  
It is through this object that we will manipulate the Arduboy by giving it instructions.  

```cpp
void setup(void)
{
	arduboy.begin();
}
```

These lines declare and define a function called `setup`.  
It doesn't take any argument and it doesn't return any values.  

The `setup` function is important for Arduino programs.  
The `setup` function contains a set of instructions that the Arduboy will run precisely once when the Arduboy starts up.  
This is why it's called `setup` - it's designed to set up the rest of the program.

`setup` almost always contains either the line `arduboy.begin()` or `arduboy.boot()` (the difference will be discussed in depth in a later chapter).  
`arduboy.begin()` takes the `arduboy` object and calls the `begin` function on it.  
This tells the Arduboy2 library to initialise the Arduboy.  
Initialising the Arduboy includes things like setting up the screen connection, activating the screen and saving power by disabling certain components.  
`begin` also handles 'flashlight' mode, the button combo for adjusting the volume and displaying the boot logo (whereas `boot` does not do these).  

```cpp
void loop(void)
{
	if(!arduboy.nextFrame())
		return;
	
	arduboy.pollButtons();
	
	arduboy.clear();
	
	arduboy.print(F("Hello world"));
	
	arduboy.display();
}
```

These lines declare and define the `loop` function.  
It doesn't take any argument and it doesn't return any values.  

The `loop` function is another important function for Arduino programs.  
After the `setup` function has completed, the `loop` function is called.  
When the `loop` function ends, it's called again, starting from the beginning.  
This is why it's called `loop` - it loops continuously until the Arduboy is turned off.  

There's quite a lot of things going on here, so I will address these one by one.  

```cpp
if(!arduboy.nextFrame())
	return;
```

By default, the Arduboy2 library has some frame rate limiting functionality to try to keep the frame rate steady.  
To use this functionality properly, the `nextFrame` function has to be called.
I will explain what's going on here, but it probably won't make much sense until you've read the chapters that discuss conditions and functions.  
(It's worth noting that this pattern is so standard that it's unusual to see anything else at the top of the `loop` function.)  

Firstly the `arduboy.nextFrame` function is called.  
If the library has deduced that it is not time to start the next frame then the function will pause the whole Arduboy for a really small amount of time before returning `false`.  
If the library has deduced that it is time to start the next frame then the function will return `true` without any pause.  
The `!` inverts the condition so that `true` becomes `false` and `false` becomes `true`.  

If it is not time for the next frame, then the `!` will invert the `false` and the `return` statement will be executed, which causes the `loop` function to end early and begin the next `loop`.  
If it is time for the next frame then the `!` will invert the `true` and the `return` statement will be skipped, thus allowing the rest of the function to continue as normal.  

```cpp
arduboy.pollButtons();
```

The hello world program doesn't use the buttons, so strictly calling `pollButtons` isn't necessary, but I've put it in here because it's part of the cmmon pattern that most Arduboy games follow.  

This function is what reads the state of the buttons and updates the `arduboy` object's information about the current state of the buttons.  
This allows the `pressed`, `justPressed` and `justReleased` functions to work properly.  
If you forget to call `pollButtons` when trying to use the button functions then your code almost certainly won't work properly.  

```cpp
arduboy.clear();
```

This function clears the screen, or more specifically the 'screen buffer'. 

Anything to be drawn to the screen is first stored in what's called a 'screen buffer', which is a block of memory that holds the information that is destined to be drawn to the screen.  
The reason it isn't drawn directly to the screen is because updating the screen is (relatively speaking) quite slow, and drawing small bits at a time can cause screen to flicker.  

If the buffer wasn't cleared before drawing, then anything drawn in the last frame would still be there, which would end up creating a sort of imperfect 'motion blur' effect, which generally doesn't look very good and isn't desirable for most games.  

It also has the effect of resetting the cursor for printing text to its default position at the top left hand side of the screen.  

```cpp
arduboy.print(F("Hello world"));
```

This function does the actual printing.  
(The reason for the `F` will be covered in a later chapter about 'progmem' ('program memory').)  

This function is pretty straight forward - you give it text and the text gets printed onto the screen buffer.  
There's also a variant called `println` which prints the text and then moves the cursor to the next line.  

(Don't worry about how it actually does the printing, that gets complicated quite quickly.)

```cpp
arduboy.display();
```

Finally the `display` function is what copies the screen buffer's contents to the screen.  
There's nothing more to it than that.  