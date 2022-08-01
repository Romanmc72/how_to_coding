# Variables and Strings

So, next we will learn a super important lesson about **variables**. A variable is a great way to only have to write something once, then you get to reuse it in a bunch of different places. **Strings** are just "text" or "words", which can be pretty much anything you could write. Let's get started with them!

## Hello {}

Create a `main.py` python file here in this directory like we did for the last lesson.

### Step 1

Let's copy what we had from last time and paste it into our new file. Then after our "Hello World" let's say "Goodbye World". So far it should just be:

```python3
print("Hello World!")
print("Goodbye World!")
```

Run it and check it out. Cool, right? Maybe not that cool yet, but bear with me. It is important to understand that programs will always execute from the first instruction all the way down to the last one.

### Step 2

Now, let's take the word `World` our of the `print` statements and add it on it's own line above the print statements in quotes, then call it something. What we call it doesn't really matter, but since we'll say hello/goodbye to this word, we'll call it `greeting` for now. So this next part should look like this:

```python3
greeting = "World"
print("Hello  !")
print("Goodbye  !")
```

Notice that we surround the word `World` with double quotes `"`. This tells the program to treat `World` as a "string" or as a piece of text, and not a command or a variable.

The word `greeting` on the other hand, we do not give it any quotes, but we do say:

```python3
greeting = "World"
```

So essentially we are telling the program that `greeting` is a variable, and the value of `greeting` is the string `"World"`. I hope that makes sense.

Try running the program where it says `print(greeting)` at the end. What do you think this will print? Try it out and see!

### Step 3

If you run this program now, it'll just be:

```
Hello !
Goodbye !
```

so we actually have to place the word "World" back into the `print()`. Here is how we will do that.

On the lines where it says `print` we will place the lowercase letter `f` right before the double quotes `"`. Then we will add curly braces `{}` where the word `World` used to be. So it should look like this:

```python3
greeting = "World"
print(f"Hello {}!")
print(f"Goodbye {}!")
```

then inside of those curly braces, put the variable `greeting` that we declared on line 1.

So finally it will look like this:

```python3
greeting = "World"
print(f"Hello {greeting}!")
print(f"Goodbye {greeting}!")
```

So what is this `f` and `{}` curly brace nonsense?

So we said things in quotes are strings. This is still true. But if you put a small `f` before the quotes, then it is called an f-string (f is for format). The f-string allows you to write your strings out like sentences then place your variable values into those sentences wherever you want using the curly braces.

Run the program now and it should say:

```
Hello World!
Goodbye World!
```

An f-string is just one of several ways we can "format" a string. Another option is getting rid of the `f` and using the curly braces so you can fill in the blank later with the `format()` command.

That would look like:

```python3
greeting = "World"
hello = "Hello {greeting}!"
goodbye = "Goodbye {greeting}!"
print(hello.format(greeting=greeting))
print(goodbye.format(greeting=greeting))
```

This will output the exact same thing as using the f-string does, but is just a different way to write it.

#### Other good things to know.

Strings can be anything between two single quotes, or between 2 double quotes, and cen even span across multiple lines if you use 3 single/double quotes in a row.

Example

```python3
'This is a string'

"This is also a string"

'''This string
goes across
three lines'''

"""This string
goes across
four
lines!"""
```

All of them can be f-strings if you put the `f` before the first quote.

### Done

So why would we do this, isn't it easier to just write hello world and goodbye world instead of all of this variable nonsense? Well, maybe, but not when you have programs longer than 2 lines. Programmers usually hate repeating themselves, and using variables lets you not have to repeat. You define the `greeting` just one time, then you can use it again all over the program whenever you want!
