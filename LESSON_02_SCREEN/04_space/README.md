# Space

We haven't really animated anything to move yet, but showing things move across spaces as time progresses is a fundamental part of creating a playable game. Between space and time the easier of these 2 things to wrap your head around (in my opinion) is the space part. It is also the easiest one to visualize, which are both good reasons to start out our time/space lessons with space.

### Coordinates

Before we dive right in and start changing the code, there is something quite important to understand first. The concept of "coordinates". Think of coordinates like a "grid". Maybe you have seen a coordinate grid on a chess board or checkers or maybe battleship game? The thing to note about a coordinate grid is that there are individual "spaces" each marked by their coordinate pair aka the coordinates. Usually these are referred to as "row" and "column" or "x" and "y".

In Battleship it looks like this:

```
     A   B   C   D   E   F   G   H   I   J
   +===+===+===+===+===+===+===+===+===+===+
 1 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 2 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 3 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 4 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 5 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 6 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 7 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 8 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 9 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
10 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
```

and if you wanted to fire a shot to this square in a game of battleship:

```
     A   B   C   D   E   F   G   H   I   J
   +===+===+===+===+===+===+===+===+===+===+
 1 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 2 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 3 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 4 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 5 |   |   |   |   |   |   |   | X |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 6 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 7 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 8 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
 9 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
10 |   |   |   |   |   |   |   |   |   |   |
   +===+===+===+===+===+===+===+===+===+===+
```

you would call out "H 5" because the coordinate for your shot is on column "H" and row "5". Make sense?

In Python's `curses` the screen has a very similar set of coordinates. Just, instead of A-J and 1-10 it they're both 0 through however big your screen is at the moment. It always starts at "zero zero" in the top left corner and goes up from there. If you change the size of the screen for the game, then you will either be increasing or decreasing the available number of rows and columns for your game to be played on.

```
     0   1   2   3   4   5   ...
   +===+===+===+===+===+===+ ...
 0 |   |   |   |   |   |   | ...
   +===+===+===+===+===+===+ ...
 1 |   |   |   |   |   |   | ...
   +===+===+===+===+===+===+ ... (keeps going to the edges)
 2 |   |   |   |   |   |   | ...
   +===+===+===+===+===+===+ ...
 3 |   |   |   |   |   |   | ...
   +===+===+===+===+===+===+ ...
 4 |   |   |   |   |   |   | ...
   +===+===+===+===+===+===+ ...
 .   .   .   .   .   .   .
 .   .   .   .   .   .   .
 .   .   .   .   .   .   .
   (keeps going to the edges)
```

Now, back to the event loop code.

### Step 1

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

Let's get rid of the parts where we just did `addstr` to add text to the screen and in their place we will still do an `addstr` but using a few variables instead of using `0, 0, 'Hello World from Curses!'`. Let's add 3 variables at the start, `row = 0`, `column = 0`, and `me = ":)"`. Then put those variables inside the `screen.addstr(row, column, me)`. (I used "me" because that is you now).

It should look like this now


```
import curses


def main(screen):
    still_playing = True
    pressed_key = ''
    row = 0
    column = 0
    me = ":)"
    while still_playing:
        screen.clear()
        screen.addstr(row, column, me)
        screen.refresh()
        pressed_key = screen.getkey()
        if pressed_key == "q":
            still_playing = False


curses.wrapper(main)
```

### Step 2

Then, we are going to replace the `pressed_key = screen.getkey()` with `pressed_key = screen.getch()`, because we are going to use the arrow keys instead of letter keys going forward and you cannot really use the arrow keys with `getkey()` because `getkey()` returns a string for the key you pushed. But what happens when you push a key that doesn't type things? Thankfully, all of the keys on the keyboard have a secret number code assigned, even the arrows, so we will use `getch()` to get that number code instead of the actual letter. Since we are changing the value from letters to number codes, we will also need to translate the "quit game" part to use the number code for "q" instead of the letter. Thankfully, you can translate any letter into its number code using the `ord()` function!

so this

```
pressed_key = screen.getkey()
if pressed_key == "q":
    still_playing = False
```

becomes

```
pressed_key = screen.getch()
if pressed_key == ord("q"):
    still_playing = False
```

Everything should still work at this point, just nothing is moving... *yet*.

### Step 3

Time to move it! Now, after the check for if the "q" key was pressed to end the game, we can check to see if other keys were pressed, and if they were we can move our character!

Let's look back at the coordinates to make sure we get the correct arrows assigned to the correct movements.

```
LEFT ARROW            RIGHT ARROW
 <-- These are the columns -->
     0   1   2   3   4   5   
   +===+===+===+===+===+===+  ^
 0 |   |   |   |   |   |   |  | UP ARROW
   +===+===+===+===+===+===+ 
 1 |   |   |   |   |   |   | 
   +===+===+===+===+===+===+
 2 |   |   |   |   |   |   |  These are the rows
   +===+===+===+===+===+===+ 
 3 |   |   |   |   |   |   | 
   +===+===+===+===+===+===+ 
 4 |   |   |   |   |   |   |  | DOWN ARROW
   +===+===+===+===+===+===+  v
```

So, looking at the above, if we press the left arrow, we want to go `-1` space on columns, if we press the right arrow we want to go `+1` space on the columns. If we press the up arrow we want to go `-1` space on the rows and if we press the down arrow we want to go `+1` space on the rows.

Make sense?

I hope so!

Also, the number codes for the arrows are stored in the curses library as special variables you can use. Get the codes by just using `curses.KEY_LEFT`, `curses.KEY_RIGHT`, `curses.KEY_UP`, or `curses.KEY_DOWN` and that will do it! Try and see if you can figure out how to put that together.

It should end up looking something like this:

```
import curses


def main(screen):
    still_playing = True
    pressed_key = ''
    row = 0
    column = 0
    me = ":)"
    while still_playing:
        screen.clear()
        screen.addstr(row, column, me)
        screen.refresh()
        pressed_key = screen.getch()
        if pressed_key == ord("q"):
            still_playing = False
        if pressed_key == curses.KEY_LEFT:
            column = column - 1
        elif pressed_key == curses.KEY_RIGHT:
            column = column + 1
        elif pressed_key == curses.KEY_UP:
            row = row - 1
        elif pressed_key == curses.KEY_DOWN:
            row = row + 1


curses.wrapper(main)
```

### Step 4

Run it and I want you to try something. Try moving your character around so that they run off of the edge of the screen, doesn't matter which edge, just find one and run off of it. What happens?

For me, I get an error like this:

```
_curses.error: addwstr() returned ERR
```

This is because we told the program to draw something on a part of the screen that does not exist. How can we protect against that so the game doesn't break while we're playing? Well, when we set the new values for row/column, we need to know if the value we are trying to set is still on the screen or not. If it is off the screen then don't move there! How can we tell if the value is on the screen? Thankfully, the lowest possible number is always zero, and the highest possible number for the columns on the screen is know by curses as `curses.COLS` and the highest number for rows is known by curses as `curses.LINES` (I know, I also wish it was called ROWS). So anything between `0` and `curses.COLS` is fine for `column` values, and anything between `0` and `curses.LINES` is fine for `row` values. How do we put that into the code? There are a few possible ways.

**Way 1 if/else**

You could just simply use an if to see what the number is about to be changed to. If it is inside the boundaries then changing it is fine and if it is outside then don't change it!

That could look like this:

```
if pressed_key == curses.KEY_LEFT:
    if column - 1 < 0:
        column = column
    else:
        column = column - 1
elif pressed_key == curses.KEY_RIGHT:
    if column + 1 > curses.COLS:
        column = column
    else:
        column = column + 1
elif pressed_key == curses.KEY_UP:
    if row - 1 < 0:
        row = row
    else:
        row = row - 1
elif pressed_key == curses.KEY_DOWN:
    if row + 1 > curses.LINES:
        row = row
    else:
        row = row + 1
```

but that is a lot more lines of code.

**Way 2 min/max**

You could also use the python min and max functions to select the highest /lowest value to assign. So for example, if we are going left (column - 1) then we would want the highest between 0 and column - 1. Written out that could look like this for all of the above cases:

```
if pressed_key == curses.KEY_LEFT:
    column = max(column - 1, 0)
elif pressed_key == curses.KEY_RIGHT:
    column = min(column + 1, curses.COLS)
elif pressed_key == curses.KEY_UP:
    row = max(row - 1, 0)
elif pressed_key == curses.KEY_DOWN:
    row = min(row + 1, curses.LINES)
```

Personally I think the min/max looks a lot neater and it is a lot less code to look at/change in the future if you want to change things. Do either one or come up with your own way!

Try that out and see if you can still run off all 4 of the edges!

...

oh... wait... you can? But just to the bottom and to the right? Hm weird. Why is that?

It is due to the fact that the `curses.COLS` and `curses.LINES` tells you the total number of columns and rows on the screen. What it does *not* tell you is the maximum coordinate possible. Since the first coordinate is 0, if the last coordinate is 10, then there are actually 11 total possible places you could be. But if you try to go to coordinate number 11 you will fall off the face of the earth because it only goes up to 10! So we actually need to use `curses.COLS - 1` and `curses.LINES - 1` when doing our comparison.

Change that and try it again.

Oh, it's still acting weird?

You can go all the way to the right then it peeks you around on the left?

And if you go to the very bottom right corner then it still breaks everything?

oof.

Okay there are still a few more things to tweak. Let's address them 1 at a time.

#### Your face wraps around to the next row

This happens because when we set our character `me` to equal `:)` we took up *2 whole coordinates* not just 1. The first for the `:` and the second for the `)`. So when it comes to the `curses.COLS` we need to not just do `-1` we need to do `-1` and `-2` (total -3) because the current size of our face is 2 columns. But let's be smart about this part. If we wanted to change our face in the future from `:)` to maybe `>:)` then we would need to add yet another `-1` for every extra column our face took up. So instead of just changing the `-1` to `-3`, let's instead subtract the length of our face using `len(me)`.

So this part

```
elif pressed_key == curses.KEY_RIGHT:
    column = min(column + 1, curses.COLS - 1)
```

should look like this now

```
elif pressed_key == curses.KEY_RIGHT:
    column = min(column + 1, curses.COLS - 1 - len(me))
```

and that should solve the wrap around issue.

#### The game crashes when you go to the bottom right corner

The above fix actually solves both problems in this case. Before we *were* wrapping around and now we are not. Wrapping around was a huge problem if you got to the last row and tried to wrap around to a row that doesn't exist. Now that there are no more wraparounds, there should be no more crashes in the bottom corner!

## Done

All in, it should look something like this:

```
import curses


def main(screen):
    still_playing = True
    pressed_key = ''
    row = 0
    column = 0
    me = ":)"
    while still_playing:
        screen.clear()
        screen.addstr(row, column, me)
        screen.refresh()
        pressed_key = screen.getch()
        still_playing = pressed_key != ord("q")
        if pressed_key == curses.KEY_LEFT:
            column = max(column - 1, 0)
        elif pressed_key == curses.KEY_RIGHT:
            column = min(column + 1, curses.COLS - 1 - len(me))
        elif pressed_key == curses.KEY_UP:
            row = max(row - 1, 0)
        elif pressed_key == curses.KEY_DOWN:
            row = min(row + 1, curses.LINES - 1)


curses.wrapper(main)
```