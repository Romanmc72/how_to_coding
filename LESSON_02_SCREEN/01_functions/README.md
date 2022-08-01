# Curses!

No, not like when you stub your toe and yell words that make your mom mad at you. Curses is actually one of those libraries that are a part of the python standard library. Curses is meant to be able to take your terminal over completely and in it's place draw a program on the screen containing whatever you need it to. I think it's called "curses" because wherever you type is the "cursor" and it's basically just typing things all across the screen. So the cursor is spitting out curses I guess? idk.

## screen

Okay, so at this point we have been running our main program using the terminal and the command `python3 main.py` and we will do much the same here. We just must beware that our program is written correctly to handle the terminal screen, otherwise it might bork up the screen and we need to restart it to use it again. Also this far we have really been working with standard library functions, but we will now be working with some things called objects. Certain objects have their own functions that only they can use. Let's take a look at the basic few needed to manipulate the screen.

### Step 1

Create a function.

#### Create a What?

A function! We haven't covered functions yet? Sheesh! Let's back up and save the curses for the next lesson actually.

What's a function you say? Well it's kind of like a mini program within a program. There are sometimes a few variables, sometimes no variables. Think of it kind of like how a variable saves a value for later so you can use it over and over again. Functions are kind of like that, but they save blocks of code so you can run it over and over without having to repeat yourself and type out the same thing a buncha times. Let's do an example.

Simplest function is the first lesson we had. "Hello World!"

That would look like this:

```python3
def hello():
    print("Hello World!")
```

Pretty easy, right? So what is going on here? The keyword `def` tells python that this next "block" will be a function. `hello` is the name of the function. `()` is where our we defined our "arguments" (aka variables that only live as long as the function is running) and here we have no arguments. The `:` then says that the next line we will start spelling out what the actual function does. In this case it just does `print("Hello World!")`.

If you put this in your file, and run it. Nothing will happen.

Why?

Well, we only *defined* the function. Next we have to *call* the function.

So to make it a complete program we need to do:

```
def hello():
    print("Hello World!")

hello()
```

Then we can run it. Try it out!

### Step 2

Let's add some arguments now. Remember last time we did the input for the name and said hello _____ fill in the blank? Let's do that with the function. Like so!

instead of this:

```python3
def hello():
    print("Hello World!")
```

Let's do this

```python3
def hello(greeting):
    print(f"Hello {greeting}!")
```

Look familiar? Like I said, the arguments are just like variables, so if we make one it is there when the function is called and when the block finishes, it is gone!

Let's greet our whole family now using the above function:

```python3
def hello(greeting):
    print(f"Hello {greeting}!")

hello("Mom")
hello("Dom")
hello("Brothers")
hello("Sisters")
```

Now what happens when you run it?

Now add the goodbye part, but just into the function.

```python3
def hello(greeting):
    print(f"Hello {greeting}!")
    print(f"Goodbye {greeting}!")
```

Then rerun the whole thing.

Swag.

### Step 3

Function-ception.

If step 2 didn't blow your mind, this probably will. What if we create a function, and that function's argument is another function?

Whoa whoa whoa, slow down there cowboy, can we even do that?

Sure!

Look at dis:

```python3
def hello(greeting):
    print(f"Hello {greeting}!")
    print(f"Goodbye {greeting}!")


def wrap_that_bad_boy(other_function, arg):
    print(f"Hey, wait, is that {arg}?")
    other_function(arg)
    print(f"And that is all I have to say to you {arg}")


wrap_that_bad_boy(hello, "World")
```

Let's step through the above to understand what's happening here.

first we define some functions, that's nice, but we don't actually call any code until we do this:

```python3
wrap_that_bad_boy(hello, "World")
```

So now we have to look up at the `def` for `wrap_that_bad_boy`. There we find:

```
def wrap_that_bad_boy(other_function, arg):
    print(f"Hey, wait, is that {arg}?")
    other_function(arg)
    print(f"And that is all I have to say to you {arg}")
```

and in this case we can look at it like its own little mini-program:

```python3
other_function = hello
arg = "World"
print(f"Hey, wait, is that {arg}?")
other_function(arg)
print(f"And that is all I have to say to you {arg}")
```

the first the we actually "do" is `print(f"Hey, wait, is that {arg}?")` then we end up calling `other_function` which we know is actually just `hello`. So let's sub that out in the above:

```python3
def hello(greeting):
    print(f"Hello {greeting}!")
    print(f"Goodbye {greeting}!")

other_function = hello
arg = "World"
print(f"Hey, wait, is that {arg}?")
other_function(arg)
print(f"And that is all I have to say to you {arg}")
```

which is really just the same as:

```python3
arg = "World"
print(f"Hey, wait, is that {arg}?")
print(f"Hello {arg}!")
print(f"Goodbye {arg}!")
print(f"And that is all I have to say to you {arg}")
```

I hope that makes sense.

The name of the function and the names of the arguments don't really matter as usual. This was just to illustrate how in Python you can just pass things around.

Why would you need this?

Well, maybe if it is anybody except "Travis" you want to say hello and goodbye. But if it's Travis? Oooh, best not hope you're Travis. We will tell Travis to go away and never come back.

So look at this:

```python3
def go_away_man(greeting):
    print(f"Go away {greeting}")
    print("and don't ever come back!!!")


def hello(greeting):
    print(f"Hello {greeting}!")
    print(f"Goodbye {greeting}!")


def wrap_that_bad_boy(other_function, arg):
    print(f"Hey, wait, is that {arg}?")
    other_function(arg)
    print(f"And that is all I have to say to you {arg}")

greeting = input("What is your name?: ")

if greeting == "Travis":
    wrap_that_bad_boy(go_away_man, greeting)
else:
    wrap_that_bad_boy(hello, greeting)
```

Try being "Travis". Tough right?

## Done

Trust me, if we didn't cover functions here then the next part would feel weird.
