# User Input

Hopefully this next part makes it a little clearer why variables rock. Let's start with the program from last time and then this time instead of greeting "World", we will ask the person running the program (in this case, you) what their name is, then give them a personal greeting.

## input()

So at this point your `main.py` should look like this:

```python3
greeting = "World"
print(f"Hello {greeting}!")
print(f"Goodbye {greeting}!")
```

### Step 1

instead of `greeting = "World"` let's make that into this:

```
greeting = input("What is your name? ")
```

What's `input()`? Good question. So it makes the program stop in its tracks, and it prints the string you give it, then waits for the user to type something. Once the user types something and hits *Enter* then it saves that as a string to the variable (`greeting` in this case).

### Step 2

Your program should look like this now:

```python3
greeting = input("What is your name? ")
print(f"Hello {greeting}!")
print(f"Goodbye {greeting}!")
```

Run the program and answer the question with your name then hit enter.

I ran it and it looked like this:

```
What is your name? Romanmc72
Hello Romanmc72!
Goodbye Romanmc72!
```

### Done

Hopefully that was an easy one. But now it should be clearer how cool a variable can be. We didn't eve know somebody's name but we can write one program that can greet literally anybody who can read and spell their own name correctly all with the same code.
