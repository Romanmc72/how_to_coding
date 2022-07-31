# Conditionals

We are almost at a point where we can make our first game. We can ask questions, we can print the answers to those questions in a sentence. One thing we're missing is the ability to make a decision based on someone's answer.

## If Else

Now we will scrap our original program and start with something new. Let's start with a question. How about 

"What is your favorite Ice Cream flavor?"

Then we will judge them for having the incorrect favorite flavor. Fun right?

Sorry if you're lactose intolerant, feel free to change it to something else that has many flavor choices. I just chose ice cream because I like ice cream.

As always we will create a `main.py`.

### Step 1


Now let's ask the player for their favorite flavor of ice cream:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
```

then make a variable called `best_flavor` and assign the best flavor, `"chocolate chip cookie dough"`. If you don't think chocolate chip cookie dough is the best flavor, then I question your judgement. For the sake of completing this tutorial though we will agree to disagree so we can move on.

You should have:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
best_flavor = "chocolate chip cookie dough"
```

### Step 2

Right now this program just asks a question then does nothing. We next need to pass judgement on people who have bad flavor preferences, and if they have good taste, we should complement them. But how do we do that? Conditionals!

After those first 2 lines, write the following:

```python3
if favorite_flavor == best_flavor:
    print("You my friend, have great taste.")
else:
    print("You my friend, have terrible taste.")
```

### What is this??? 

This is a "conditional" where our program checks to see if a certain condition is `True` or `False`. If it is `True`, it will do one thing, and if it is `False` we con do something completely different.

You will notice that there are 4 spaces before we print the judgemental sentence. Why is this? There is also a colon `:` after the `if` condition and after the `else`, what's that? And that `==` what is that, why are there 2 `=`?

Great questions. So in Python, 4 spaces is known as "whitespace" or space with nothing in it, and sometimes when you see a `:` it tells you that the next part of the code is part of the "block" for this statement / condition and will you need 4 white-spaces. Once the next line of code comes that does not have 4 white-spaces, then Python knows that the "block" is finished. So for `if` and `else`, if our `if` is `True` then all of the things that have 4 white-spaces that come right after the `if` will be run as part of that "block". If the `if` is `False` then the `else` "block" will run all of the things with 4 white-spaces that come right after it. As for the `==`, the 2 `=` signs mean we want to check if something is the same. Just 1 `=` sign means we are assigning something to a variable. 2 `=`s gives you a check which can either be `True` or `False` (which we call a `boolean`).

### Run it!

Let's run it and see if we can get the thing right:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
best_flavor = "chocolate chip cookie dough"
if favorite_flavor == best_flavor:
    print("You my friend, have great taste.")
else:
    print("You my friend, have terrible taste.")
```

pretty neat!

### Step 3

Now, let's say we want to give them something in between great and terrible. Perhaps there are a few flavors that are *fine*. I will submit to you that the list of *fine* flavors includes "strawberry", "chocolate", and "mint chocolate chip". Maybe you have a few more ideas. There are a few ways we can add something like this. Let's take a look!

#### More If's

In Python you can do `if` to check for a condition like we saw above, you can set an `else` to determine what to do if the condition is not met, but you can also add more conditions to check for if you want to have several possibilities. Those are called "else if" and in python we write that as `elif` (short for else if).

So let's add those `elif`s.

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
best_flavor = "chocolate chip cookie dough"
if favorite_flavor == best_flavor:
    print("You my friend, have great taste.")
elif favorite_flavor == "chocolate":
    print("You my friend, have decent taste.")
elif favorite_flavor == "strawberry":
    print("You my friend, have decent taste.")
elif favorite_flavor == "mint chocolate chip":
    print("You my friend, have decent taste.")
else:
    print("You my friend, have terrible taste.")
```

Let's run that and see what happens if we input a "decent" flavor. (Spoiler it works)

But! This is what programmers would call "ugly". Why? I mean it works, but we are repeating ourself all over the place. Let's clean that up a little.

#### Variables

Let's use variables from earlier because we have the following string repeated a bunch of times:

> `"You my friend, have ______ taste."`

To clean that up we can use the variable approach with a format string. So at the top let's add this at the top of the file:

```python3
judgement = "You my friend, have {taste} taste."
```

then in all of those `print` commands we can use:

```
    print(judgement.format(taste="decent"))
```

or "terrible" or "great" or whatever you want to say in that case.

So now we should have:

```python3
favorite_flavor = input("What is your favorite Ice Cream flavor? ")
judgement = "You my friend, have {taste} taste."
best_flavor = "chocolate chip cookie dough"
if favorite_flavor == best_flavor:
    print(judgement.format(taste="great"))
elif favorite_flavor == "chocolate":
    print(judgement.format(taste="decent"))
elif favorite_flavor == "strawberry":
    print(judgement.format(taste="decent"))
elif favorite_flavor == "mint chocolate chip":
    print(judgement.format(taste="decent"))
else:
    print(judgement.format(taste="terrible"))
```

#### Lists

We can simplify this even further. How? Using another data type (so far we have just used strings) called a `list`. A list is just a bunch of things that are held in the same variable. You can have a list of strings, numbers, variables, or even other lists! Pretty much anything. So let's make that list of decent flavors.

```python3
decent_flavors = [
    "strawberry",
    "chocolate",
    "mint chocolate chip",
]
```

> Notice that the list is indicated by a square bracket `[]` and each element or item within the list is separated by a comma `,`. That is how we tell python that we have a list, and how we keep the things in the list separate.

Now that we have a list, and we have someone's favorite flavor, instead of doing three `elif` checks just to `print` the same thing, we can just do one! That will look like this:

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

Boom! Now we only to do two condition checks. If we wanted to go back and add more flavors to the list of decent flavors, then we can just add another flavor to the list instead of having to copy-paste the `elif` and the `print` just to change the string for the flavor name.

### Done

Now we're done, and we have learned how to do conditionals and we got lists as a bonus.
