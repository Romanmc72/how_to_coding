# Loops

This is the last piece we will need in order to create an escape room style game. Loops are awesome and super powerful ways to really simply write code that will run over and over and over again until your program is "done". Let's look into loops!

## While

So now we will start with the ice cream program we just wrote in the conditionals lesson. You should have a program like this:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
judgement = "You my friend, have {taste} taste."
best_flavor = "chocolate chip cookie dough"
decent_flavors = [
    "strawberry",
    "chocolate",
    "mint chocolate chip",
]
if favorite_flavor == best_flavor:
    print(judgement.format(taste="great"))
elif favorite_flavor in decent_flavors:
    print(judgement.format(taste="decent"))
else:
    print(judgement.format(taste="terrible"))
```

And we will serve this person a new scoop of ice cream until they are full. Let's try it out!

### Step 1

After we judge this person, we will now serve them their favorite ice cream (no matter how terrible their taste is). To do this we will add what's called a `while` loop. This will basically say "while this person still wants more ice cream, we will server them more ice cream".

so add this at the end of the file:

```python3
while wants_more == "yes":
    print(f"Here is another scoop of {favorite_flavor}!")
```

### Step 2

If you run this right now it will break. We must get another answer from this person in order to determine if they actually want some ice cream.

So before the loop begins, we will add:


```python3
wants_more = input(f"Do you want a scoop of {favorite_flavor}? ")
```

Now your program should look like this:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
judgement = "You my friend, have {taste} taste."
best_flavor = "chocolate chip cookie dough"
decent_flavors = [
    "strawberry",
    "chocolate",
    "mint chocolate chip",
]
if favorite_flavor == best_flavor:
    print(judgement.format(taste="great"))
elif favorite_flavor in decent_flavors:
    print(judgement.format(taste="decent"))
else:
    print(judgement.format(taste="terrible"))
wants_more = input(f"Do you want a scoop of {favorite_flavor}? ")
while wants_more == "yes":
    print(f"Here is another scoop of {favorite_flavor}!")
```

But at this point you do not want to run it! If you did run it, and your whole screen is just filled up with the program giving you another scoop of your favorite flavor, then you can hold the "Control" key then press "C" it will interrupt the program and stop it. This is useful to know in general in case you ever get into an infinite loop.

As a matter of fact, maybe just run it and answer "yes" to the question about getting a scoop of ice cream. See what happens. Break the program with control c when you're done getting a million scoops of ice cream.

### Step 3

In order to interrupt this infinite scoop loop, we will need to add another input inside the `while` "block". Just like the `if` blocks, the `while` loop will run ALL OF THE THINGS that have the whitespace right after it, then it will look at its condition again an while that condition is still true, it will keep running its block. So let's add another `input` inside the `while` block to update the variable `wants_more` to see if the person really wants more ice cream still.

That should look like this:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
judgement = "You my friend, have {taste} taste."
best_flavor = "chocolate chip cookie dough"
decent_flavors = [
    "strawberry",
    "chocolate",
    "mint chocolate chip",
]
if favorite_flavor == best_flavor:
    print(judgement.format(taste="great"))
elif favorite_flavor in decent_flavors:
    print(judgement.format(taste="decent"))
else:
    print(judgement.format(taste="terrible"))
wants_more = input(f"Do you want a scoop of {favorite_flavor}? ")
while wants_more == "yes":
    print(f"Here is another scoop of {favorite_flavor}!")
    wants_more = input(f"Do you want another scoop of {favorite_flavor}? ")
```

Now we should be able to safely run this without looping forever. Try it out!

## For

Now, if you have ever ordered ice cream at an ice cream shop, usually they don't stop and ask you if you want another scoop infinitely until you tell them to stop. Usually they say "How many scoops do you want?" and you give them a number. Another type of loop which rocks is the `for` loop. The `while` loop will just keep looping until you finally hit a false condition. The `for` loop on the other hand, loops over an exact number of things to run its code block. So we can just ask them how many scoops they want and then give them that many scoops of their favorite flavor if ice cream.

### Step 1

Let's get rid of the entire `while` loop, everything in it, and the `wants_more` question. Then in their place let's add a different question where we will store the number of scoops like so:

```python3
number_of_scoops = input(f"How many scoops of {favorite_flavor} do you want? ")
```

If somebody puts a number into this answer, we will get a string of that number. This is actually not great. We don't want a piece of text, we want an actual number. What's the difference you ask? Well, remember, computers are stupid, so if you tell it `"4"` instead of `4` it will do all of the wrong things. Let's look at some examples.

Let's just say that the `number_of_scoops` someone puts in is 4.

If we wanted to ask them for a second flavor and then give them 4 scoops of each (total of 8), as-is we cannot just do `total_scoops = number_of_scoops + number_of_scoops`, because when `4` comes through as the string `"4"`, we get `"4" + "4"` which becomes `"44"` because when you "add" strings, it just combines them together. We need to "cast" the string into a number. In Python, whole numbers are called `int` (short for integer) and numbers with decimals are called `float` (short for floating point). To convert the response from string to int, we just wrap the variable in the `int()` function and it becomes a number so when we do the math, it is `4 + 4 = 8` not `"4" + "4" = "44"`.

So to modify the above, we would actually do this:

```python3
number_of_scoops = input(f"How many scoops of {favorite_flavor} do you want? ")
number_of_scoops = int(number_of_scoops)
```

or even more simply:

```python3
number_of_scoops = int(input(f"How many scoops of {favorite_flavor} do you want? "))
```

#### (optional)

What happens if you put something into the answer that is not a number? Look into `try` and `except` to figure out how to handle that scenario. Otherwise keep going!

### Step 2

Now that we have acquired the number of scoop that the person wants, we can give them exactly that many scoops. Here is how!

```python3
for scoop_number in range(number_of_scoops):
    print(f"Here is scoop number {scoop_number} of {favorite_flavor}")
```

Let's run it!

...

Notice anything weird? You should. If we put in `4`, then the first scoop is `0` and the last one is `3`. What? Why? So the way that `range()` works, is it creates a list (remember those?) that starts at zero and goes until the number you put in, but it stops just before the number you put in. That is because the "index" (or the spot in the list) for all lists always starts at zero. Like if you're standing in line. If you are first in line, usually we say you are at position or index 1, but in Python you're actually at position 0. If we want to start the `range()` at 1 and include our last number, we actually have to put our start and stop numbers in. It will still stop right before the last number, so we just need to tell it that the end number is our `number_of_scoops + 1`.

Change it to this and run it again:

```python3
for scoop_number in range(1, number_of_scoops + 1):
    print(f"Here is scoop number {scoop_number} of {favorite_flavor}")
```

Or! honestly, you could just change the print part to print `scoop_number + 1`. Either way would work, but it is important to know how lists and indexes work.


```python3
# This works too...
for scoop_number in range(number_of_scoops):
    print(f"Here is scoop number {scoop_number + 1} of {favorite_flavor}")
```

### Step 3 (optional)

That all happens pretty fast, like less than a second to scoop however many scoops you say. Even 100! If we wanted to make it a little more realistic by making it take a little break between scoops, then we can use the `sleep()` function to make the program wait between scoops. `sleep()` takes one argument, and that is the number of seconds you want it to "sleep" (or wait) for before it runs the next command. Let's make it wait for a half second. We can write that as either `1 / 2` or `0.5` it is the same either way. However we come to another topic here...

#### import

`sleep()` is not actually something you can just write like you can using `print()`, `int()`, `range()`, `for`, `if`, etc... Sleep is a part of another "module" or "library". Modules/Libraries are just bundles of extra code you can use if you want to, but they're not a part of your program by default because, well... there are a TON of them, and it would make your program a little slower if you had all of these things in it that you never needed or never used. So if you want to use the built in libraries (often called the standard library) you can import some of those functions like this!

(make this the first line of your program)

```python3
from time import sleep
```

Then, inside our for loop, put `sleep(0.5)` so that the program waits a half second before giving you another scoop. The whole program should look like this now:

```python3
from time import sleep
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
judgement = "You my friend, have {taste} taste."
best_flavor = "chocolate chip cookie dough"
decent_flavors = [
    "strawberry",
    "chocolate",
    "mint chocolate chip",
]
if favorite_flavor == best_flavor:
    print(judgement.format(taste="great"))
elif favorite_flavor in decent_flavors:
    print(judgement.format(taste="decent"))
else:
    print(judgement.format(taste="terrible"))
number_of_scoops = int(input(f"How many scoops of {favorite_flavor} do you want? "))
for scoop_number in range(1, number_of_scoops + 1):
    sleep(0.5)
    print(f"Here is scoop number {scoop_number} of {favorite_flavor}")
```
