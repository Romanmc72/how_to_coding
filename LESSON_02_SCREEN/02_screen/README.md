# Screen

Okay, okay, now I promise we will put things on the screen with the curses.

## Starter Pack

Here is the initial code ot run a curses program:

### Step 1

New file with new code, need a clean slate here.

First, import curses. We will use it, A LOT.

```python3
import curses
```

Then, create a function. You can call it whatever you want. I am calling mine `main`. Make sure that function takes one argument called `screen`.

```
def main(screen):
```

Then toss all of this garbage in there:

```python3
def main(screen):
    screen.clear()
    screen.addstr(0, 0, 'Hello World from Curses!')
    screen.refresh()
    screen.getkey()
```

What's goin on here?

The first line is the function definition, and this function takes only one argument: `screen`.

Then we just use that screen a bunch. We do `clear()`, `addstr()`, `refresh()` and `getkey()`. woof that is a lot. Let's look at each of those.

First off, `screen` is an "object". Objects have certain properties (think of them as variables tied to the object) and methods (basically functions that only the object can call). Screen we expect to have some methods available for us to call, and we call them in this specific order.

- `clear()` will take whatever is on your terminal and wipe it away.
- `addstr()` will add a string onto the screen you just cleared in the position you declare
    - In our case we declare the position as 0, 0 (aka the top left corner)
        - 0, 0 is top left because when you read, you read top left to bottom right
    - Then we give it the string to add to the screen which is `'Hello World from Curses!'`
- `refresh()` will cause the cleared screen to "show" all of the `str`s that we `add`ed since the last `clear()` with `addstr` (hint: we can add a whole lot more than 1 string)
- `getkey()` lastly makes the program wait for you to press a key, then if you do it will `return` (a topic we have not covered) the pressed key

BUT! As you probably can tell, we have not yet declared a `screen` variable, and we have not yet called our function. We will do that lastly like so:

```
curses.wrapper(main)
```

Remember when we passed one function as the argument to another? That is what we are doing here. We use the `curses.wrapper()` to make sure that when we start with curses and when our program ends that our terminal always goes back to where it is still working. You can technically use `curses` without the wrapper, but it is not recommended because you can goof up your screen if you do it wrong.

all in, it should look kind like this:


```python3
import curses


def main(screen):
    screen.clear()
    screen.addstr(0, 0, 'Hello World from Curses!')
    screen.refresh()
    screen.getkey()


curses.wrapper(main)
```

Run it! (press any key to exit)

### Done

Tada! We are done. Not super exciting yet, but we are just getting started here. Hopefully what we covered so far makes sense. If not, ask some questions and google some things to try and find answers.
