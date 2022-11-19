# Event Loop

The event loop is up next and is a crucial part to any type of game. Simply put, it is a loop of code that runs over and over again to process "events". What's an event you ask? An event is anything that happens within the game. Let's look at some examples.

- The player moved a space
- The player attacked with a weapon
- The enemy moved a space
- The enemy attacked with a weapon
- The Player hit the enemy with an attack
- The enemy died

And the list can go on an on and on. Like I said, any type of thing that can happen in the game. Some of these things are triggered when the player takes an action and some of them happen all on their own (like the enemies moving around).

Before we get to creating a character and enemies and weapons and all of that, we will first begin with creating our event loop. As our program stands from the last time we started, all we have is a way to take over the screen, wait for a button to be pressed, then the game is over. Instead now we will process button presses in a loop, so that every time you press a button something very simple happens, like a thing moves one space. Yeah let's do that actually. So from here

```python3
import curses


def main(screen):
    screen.clear()
    screen.addstr(0, 0, 'Hello World from Curses!')
    screen.refresh()
    screen.getkey()


curses.wrapper(main)
```

## Step 1

We will create a variable called `still_playing` and set it to `True` inside the `main()` function right at the very start. This will tell the game that we are still playing, and we can set it to False whenever we are done playing.

```
def main(screen):
    still_playing = True
    screen.clear()
    screen.addstr(0, 0, 'Hello World from Curses!')
    screen.refresh()
    screen.getkey()

```

Then, let's decide what button "ends" the game. Maybe "q" for quit? Why not! Let's capture what key is being pressed now like so:

```
def main(screen):
    still_playing = True
    screen.clear()
    screen.addstr(0, 0, 'Hello World from Curses!')
    screen.refresh()
    pressed_key = screen.getkey()
```

then after we detect what is pressed we can set `still_playing` accordingly.

```
def main(screen):
    still_playing = True
    screen.clear()
    screen.addstr(0, 0, 'Hello World from Curses!')
    screen.refresh()
    pressed_key = screen.getkey()
    if pressed_key == "q":
        still_playing = False
```

## Step 2

Then last but not least we wrap almost everything up in a `while` loop! We covered those already, right?

```
def main(screen):
    still_playing = True
    while still_playing:
        screen.clear()
        screen.addstr(0, 0, 'Hello World from Curses!')
        screen.refresh()
        pressed_key = screen.getkey()
        if pressed_key == "q":
            still_playing = False
```

## Step 3

So, now we have an event loop! The only event we are really listening for at this point is whether or not the letter "q" is pressed, but hey, we have an event loop! Let's also add in one more line on the screen so we can see that this code is actually doing something when we press other keys. Right after we get the `pressed_key` let's do a `screen.addstr` to display which key was pressed, like so:

```
def main(screen):
    still_playing = True
    while still_playing:
        screen.clear()
        screen.addstr(0, 0, 'Hello World from Curses!')
        screen.refresh()
        pressed_key = screen.getkey()
        screen.addstr(1, 0, pressed_key)
        if pressed_key == "q":
            still_playing = False
```

Great run it!

...

Oh...

Is the pressed key not showing up? Well now wait a minute, why would that be? I'll spoil this one for you actually. So our event loop is running as many times as fast as it possibly can EXCEPT there's one thing. The `screen.getkey()` command is actually "blocking" the loop every time that it gets to that point. As soon as the key gets pressed, the loop rushes all the way back around until it gets to the `screen.getkey()` part again and then it waits for you to press the key again. The downside here is that we don't add the key we pressed onto the screen until after we get the key. If we added it *before* then it would show up on the next loop. Let's do that, and while we're at it, let's put the `screen.refresh()` after both of the `screen.addstr` commands.

```
def main(screen):
    still_playing = True
    while still_playing:
        screen.clear()
        screen.addstr(0, 0, 'Hello World from Curses!')
        screen.addstr(1, 0, pressed_key)
        screen.refresh()
        pressed_key = screen.getkey()
        if pressed_key == "q":
            still_playing = False
```

Try it now!

```
UnboundLocalError: local variable 'pressed_key' referenced before assignment
```

Oh no! The code doesn't even run anymore! Thankfully this tells us exactly why.

It means we tried to use ("reference") the variable called `pressed_key` before we told python what it even was. Take a look at the code. Yep. We definitely did that. But then how do we set it so that we can actually see the pressed keys without having the program crash? Simple! We set a default value for it at the very start and then every time it runs and detects a new key, it will use the newly detected value instead of the initial default. So at the very start right after we declared `still_playing = True` we need to also declare `pressed_key = ''` or set it as an empty string (because we didn't press anything yet). Do that then try it out.

```
def main(screen):
    still_playing = True
    pressed_key = ''
    while still_playing:
        screen.clear()
        screen.addstr(0, 0, 'Hello World from Curses!')
        screen.addstr(1, 0, pressed_key)
        screen.refresh()
        pressed_key = screen.getkey()
        if pressed_key == "q":
            still_playing = False
```

## Done

WOO HOO it works!

your whole program should now look like this:

```
import curses


def main(screen):
    still_playing = True
    pressed_key = ''
    while still_playing:
        screen.clear()
        screen.addstr(0, 0, 'Hello World from Curses!')
        screen.addstr(1, 0, pressed_key)
        screen.refresh()
        pressed_key = screen.getkey()
        if pressed_key == "q":
            still_playing = False


curses.wrapper(main)
```

That's probably enough on event loops for now.
