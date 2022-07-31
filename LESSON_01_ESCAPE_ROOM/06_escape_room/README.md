# Escape Room

We made it! You now have everything that you need in order to design an escape room video game. This escape room will not have any graphics at all. It will be entirely text-based, but you can do it yourself. If you completed these lessons you have all of the skill you need to go to the next step and actually make the game work.

## Making the Game

I am not really going to force you to make the escape room and particular way. I have a very loose escape room program that I will share here. Feel free to steal this one and modify it or completely start from scratch and make your own.

Initial starting point:

```python3
from time import sleep
from random import randint

game_over = False
window = 1
padlock = 2

# We did not cover the random library, but this way the
# code changes every time you play to use a random 4 digit
# number so nobody can cheat even if they can read code!
# `str` casts the number to a string, and `zfill(4)` is making
# sure that the number always has 4 digits, even if the first
# few digits are zero.
padlock_combination = str(randint(0, 9999)).zfill(4)

while not game_over:
    where_to_look = int(
        input(f"""Where do you want to go? (type the number)
        {window} = Look Out The Window
        {padlock} = Try The Padlock
        ?: """)
    )
    if where_to_look == window:
        print("You look out the window")
        sleep(0.5)
        print("...")
        sleep(0.5)
        print("...")
        sleep(0.5)
        print("...")
        sleep(0.5)
        print("Is that a chicken with a number painted on it?!")
        sleep(2)
        print("IT IS!!!")
        sleep(2)
        print(f"The number is {padlock_combination}")
        sleep(1)
    elif where_to_look == padlock:
        attempted_combination = input("Try the lock, it is 4 digits: ")
        if attempted_combination == padlock_combination:
            print("It unlocked!!!")
            game_over = True
            sleep(3)
        else:
            print("It will not budge.")
            sleep(1)

print("You Escaped! Congrats.")
sleep(1)
print("Now go catch that chicken.")
```

You can start with this, add more clues, add other rooms that lead to nowhere. Take your player anywhere that you can write! Have fun.
