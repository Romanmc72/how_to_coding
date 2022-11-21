# Spike Dodger

Head's up! Somebody put a spike in the ceiling on our last lesson and now it keeps falling from the ceiling over and over. Thankfully it is not a deadly spike, it's more like a ghost spike that falls and stops then keeps falling over and over again in the same spot. Pretty lame. But what if when it hit us we got killed by it? And maybe we even keep track of how many spikes we dodged and have a score for the game! Yeah I like that. Let's try it!

## Step 1

We need to now add a check for the game on every frame that if the spike's coordinates and your player's coordinates are the same, then it is GAME OVER. Probably doesn't sound too bad right? Matter of fact, let's see if you can handle this one.

No, I'm serious. I believe in you!

Here's where we left off last time:

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

See if you can add some of the following features:

- Spike changes to a new, random spot whenever it hits the floor
    - (hint: remember the `random` library from the escape room? use that probably.)
- There is a counter on the screen keeping track of how many spikes hit the floor
- The game ends if the spike hits the player
- Extra challenge, can you make more spikes appear every time you dodge one?

Also, don't forget about the edges of the screen!
