# Time

Time and space, space and time. We take these things for granted in our world, but in the digital world we have to define them! What rate does time move at and where are things located within the space of the game? As of the last lesson, we created some movement across space inside our event loop, but in our event loop, time doesn't quite work like it does in the real world. In our event loop, everything happens instantaneously then stops suddenly and waits for something to happen. In the real world, things just happen and time just keeps moving. So we want to make our game in such a way that time also keeps moving even if we choose to do nothing. Not only does time move, but as time progresses, things move across spaces. In this lesson we will add another object to the screen and just try to have it move at a constant speed the entire time across the screen while we freely move (or sit still) inside the game and just observe the passing of time in our game.

## Step 1

Starting from where we left off, we should have a game that looks like this:

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

Let's add another character to the game, this time it will be a single letter, maybe "v" because it looks kind of like a spike, and we will have it fall from the top of the screen to the bottom of the screen. Then when it reaches the bottom, it will go back to the top and start falling all over again. To do this we will need to give it its own coordinates and its own `addstr` for the screen. Let's start like this:

```
def main(screen):
    still_playing = True
    pressed_key = ''
    row = 0
    column = 0
    me = ":)"
    spike = "v"
    spike_column = 3
    spike_row = 0
    while still_playing:
        screen.clear()
        screen.addstr(row, column, me)
        screen.addstr(spike_row, spike_column, spike)
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
```

Then at the very end of the loop we will increase the row for the spike until it hits `curses.LINES` then reset it to 0 again.

There are actually a couple ways to do this as well.

**Way 1 if/else**

Nothing wrong with your classic `if/else`.

```
if spike_row == curses.LINES - 1:
    spike_row = 0
else:
    spike_row = min(spike_row + 1, curses.LINES - 1)
```

**Way 2 modulus %**

The modulus operator (the percent symbol %) is a super neat tool. You can think of it like a clock. Where once the hand gets to 12, it starts back over again. Except with this you can put the "reset" to any number, not just 12.

```
spike_row = (spike_row + 1) % curses.LINES
```

So in that case it will keep adding 1 to the `spike_row` until it gets to the last line, then it will reset it to zero! I prefer the modulus. It looks weird at first, but it is also a great tool to have in your arsenal of programming tricks.

*why use `% curses.LINES` not `% curses.LINES - 1`*

Good question, the way modulus works, is if it was a "normal" clock and you did  `% 12` it would actually never reach 12. It would hit 11 then go back to zero. The whole point of `curses.LINES - 1` was to prevent us from going to the coordinate `row = curses.LINES` and the `%` resets the value before we get there.

It should look like this now:

```
def main(screen):
    still_playing = True
    pressed_key = ''
    row = 0
    column = 0
    me = ":)"
    spike = "v"
    spike_column = 3
    spike_row = 0
    while still_playing:
        screen.clear()
        screen.addstr(row, column, me)
        screen.addstr(spike_row, spike_column, spike)
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
        spike_row = (spike_row + 1) % curses.LINES
        
```

Try and run it to see what happens!

Kinda bogus, the spike isn't "falling", it is really just reacting to when we move. Like I said before, time is weird in the game world, we have to create it ourselves.

## Step 2

Now we will need to do something we have not done before. We will need to change the way that curses listens for our key presses. Right now it is "blocking" meaning that once the code reaches the part where it is supposed to detect what key we press, it stops and waits. We don't want that because that stops time in our game. What we want instead is that if there is a key pressed when it gets there, we want it to notice, but if nothing is being pressed then the code should still keep going. This is actually super simple to do. We just need to add `screen.nodelay(True)` as the first thing that happens inside the `main()` function. So the first few lines of the program are now:

```
import curses


def main(screen):
    screen.nodelay(True)
```

Try and run it and see what happens.

Holy Moly that looks weird. What's happening now is the code is running as fast as it possibly can and either your eyes cannot keep up, the computer screen cannot keep up, or both. Next up we need to actually tell our program to slow it down a little.

### Step 3

Slowing it down means we have to decide on a reasonable speed. Usually in a video game they call it the "frame rate" or "frames per second" or "fps" for short. We will declare a variable for the FPS in a moment here, but i will briefly stop and explain what that all means. I will start the explanation by asking a question. How does a video work? When you watch something on youtube or netflix, what are you actually looking at? Are things "moving"? If you think about it, nothing is really "moving". It's just a TV or computer screen that is sitting there. But it looks like things are moving doesn't it? If you break it down, a video is actually just a ton of pictures that are played over top of one another really really fast. It is exactly like a flip book. If you have ever read captain underpants and done the flip-o-rama or made your own flip book out of post-it sticky notes, that is what happens with any kind of video. Whether it is a video game or a youtube video, all of it is just a bunch of picture playing so fast that it tricks your brain into thinking that things are moving when they really aren't.

Why am I telling you this?

Because it is important to know what we are talking about here when we try to pick our own frames per second. It will control the most basic unit of time in our game. I the real world time can get infinitely small, down to nanoseconds. In video games though, the smallest unit of time is one frame. The human brain cannot actually tell the difference when there are more than 60 frames per second. Anything less than 15 frames per second, and the human brain doesn't immediately think it is a moving thing like a video. A lot of games clock in around 30 frames per second, so we will actually start with that and see how it looks.

Add a variable called `FPS = 30` and then where we imported `curses` at the top, we are also now going to import the `sleep` function we used earlier in the escape room game to make the program wait for each frame. If `sleep(1)` is sleep for 1 second, and we want to sleep 30 times in 1 second, we need to do `sleep(1 / 30)` or `sleep(1 / FPS)` since we set our FPS to 30.

We should now have:

```
import curses
from time import sleep


def main(screen):
    screen.nodelay(True)
    still_playing = True
    FPS = 30
    pressed_key = ''
    row = 0
    column = 0
    me = ":)"
    spike = "v"
    spike_column = 3
    spike_row = 0
    while still_playing:
        screen.clear()
        screen.addstr(row, column, me)
        screen.addstr(spike_row, spike_column, spike)
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
        spike_row = (spike_row + 1) % curses.LINES
        sleep(1 / FPS)


curses.wrapper(main)
```

## Done

Try it out!

Muuuuuch better right?

That's it for the time lesson. Try messing around with the `FPS` variable and see what changing it to different levels looks like.
