# Chapter 1.2 - Making decisions

## Introduction

Normally it's customary to introduce people to variables or simple arithmetic first, but I'm going to be doing things a bit differently.  
I have decided that it's far more fun to be able to interact with your Arduboy from the start, so the first thing I will be demonstrating is how to get your code to react to button input.  

## A Code Example

Before I get to the explaining part, I'll try to grab your interest with a bit of code.  
Take this code, compile it, and run it on your Arduboy.  

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
	
	if(arduboy.pressed(A_BUTTON))
	{
		arduboy.println(F("A Pressed"));
	}
	else
	{
		arduboy.println(F("A Released"));
	}
	
	arduboy.display();
}
```

The majority of this code is exactly the same as the hello world example, so hopefully it doesn't look too scary.  
Before I explain what's going on, try running this code and pressing the A button on your Arduboy.  
Now look at the code. Hopefully you'll be able to figure out what's going on yourself.  
If you can't, don't worry, I'll explain anyway, but I urge you to have a think about it first.  

## Explanation

So, we've already established that 95% of this is the same as the hello world example, let's focus on the other 5%.  

```cpp
if(arduboy.pressed(A_BUTTON))
{
	arduboy.println(F("A Pressed"));
}
else
{
	arduboy.println(F("A Released"));
}
```

When running the program you should have noticed that:  
* If you press the A button, you get the message "A Pressed"
* If you don't press the A button, you get the message "A Released"

This is exactly what this piece of code is telling the Arduboy to do.  

The part `if(arduboy.pressed(A_BUTTON))` effectively says 'if the A button is pressed', the next part (`arduboy.println(F("A Pressed"));`) says what to do - which is to print the message "A Pressed".  
The `else` then says 'otherwise (if the A button isn't pressed)', and the part after that (`arduboy.println(F("A Released"));`) says to print the message "A Released".  

This hopefully illustrates exactly how the `if` statement and the `else` statement behave.  
If the expression inside the brackets of an `if` statement evaluates to `true` then the following statement is executed, otherwise it is not executed.  
An `else` statement is essentially bound to the previous `if` statement and it specifies what to do if the `if` statement's condition is `false`.  
Essentially it does what it says on the tin 'if (some condition) do this; else do this;'.  

## The Significance Of `if` And `else`

The main reason I wanted to cover `if` and `else` first is because this tutorial will be a lot more fun if you're able to make the Arduboy change behaviour based on button presses.  
However, there's another important reason why I've decided to bring this up early on.  

If all computers could do was maths then frankly they wouldn't be any more useful than compotmeters (historical mechanical calculators).  
The ablitity to make decisions is what makes computers truly useful.  
Without that ability, many advanced programs would be impossible.  
In fact I'd go so far as to say that it is possibly the very foundation of programming.  

## Syntax: Omission Of The Braces

The last thing I'd like to mention is when it's acceptable to omit the braces from an `if` statement or an `else` statement.  
You may or may not have noticed this, but in an earlier example of the `if` statement, there are no curly braces:  
```cpp
if(!arduboy.nextFrame())
	return;
```

In this case I could have left the curly braces in, like so:  
```cpp
if(!arduboy.nextFrame())
{
	return;
}
```

And in the case of the buttons, I could have omitted the curly braces, like so:  
```cpp
if(arduboy.pressed(A_BUTTON))
	arduboy.println(F("A Pressed"));
else
	arduboy.println(F("A Released"));
```

So the question is "Exactly when are you allowed to omit the curly braces, and why do you need them in the first place?".  

It's quite simple really. You can omit the curly braces when there's only one statement after the `if` (or the `else`).  
In all of these examples, there's only one thing happening if the `if` condition is `true` and only one thing happening if the `if` condition is `false`.  

So what happens if we have two things?  
Let me show you:  
```cpp
if(arduboy.pressed(A_BUTTON))
	arduboy.println(F("The A button"));
	arduboy.println(F("is Pressed"));
```

What happens here is that when the A button is pressed the words "The A button is pressed" are printed,  
_but_ if the A button is not pressed, what you end up with is the words "is pressed" being printed.  

This is because when you omit the braces, only the first statement is coupled to the `if` statement.  
So essentially this:  
```cpp
if(arduboy.pressed(A_BUTTON))
	arduboy.println(F("The A button"));
	arduboy.println(F("is Pressed"));
```
Is equivalent to this:  
```cpp
if(arduboy.pressed(A_BUTTON))
{
	arduboy.println(F("The A button"));
}

arduboy.println(F("is Pressed"));
```

The remedy to this would be to manually use braces to group the statements that you want to execute:  
```cpp
if(arduboy.pressed(A_BUTTON))
{
	arduboy.println(F("The A button"));
	arduboy.println(F("is Pressed"));
}
```

Because of this, many people argue about whether it's a bad idea to omit the braces.  
Personally I often omit the braces because I know the rule about them like the back of my hand.  
But if you're still a bit inexperienced then I'd recommend that you always use braces because it's one less thing for you to have to worry about.  
When you've been programming for quite a while (let's say a couple of weeks or so) then feel free to experiment with omitting the braces.  
One of the best ways to learn the rules is to test them to breaking point.  