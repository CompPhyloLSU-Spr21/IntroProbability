# Sampling Exercise

Let's create our own sample space using the Rev language. We'll begin by creating a vector in RevBayes. A vector is simply a list of values. To create a vector, we first give it a variable name (in this case, `sampleSpace`) and then assign the list of values to that variable name. An equals sign (_=_) is one of the assignment operators in RevBayes. It takes whatever is on the right and assigns it to the variable on the left. There are a few different ways to create a vector, but the simplest is probably to enclose a comma-separated list of values in square brackets [ . . . ]

```
sampleSpace = ["a","b","c"]
```

To check the value of any variable, we can simply type the name of that variable and RevBayes will print its current value.

```
sampleSpace
```

We can verify the size of our vector (i.e., the number of values it contains) by using its _size()_ method. You can think of a method as a way of asking a question about a variable. In this case, we're asking our vector, how big are you?

```
sampleSpace.size()
```

We can also check individual values in a vector by using the name of the vector and providing indices. For instance, to look at only the 2nd value in the list we would type:

```
sampleSpace[2]
```

To sample values from our sample space, we need to know a few more things about the Rev language. First, if we want to create a new vector, we can do so implicitly by starting to assign values to individuals positions in the new vector. For instance, if we wanted to store a vector of values (called `mySamples`) sampled from our sample space, we could start by doing something like this:

```
mySamples[1] = "a"
mySamples
```

If we want to do something repetitious, like sample from our sample space many times, we'll want to use a construct called a `for` loop. `for` loops are ubiquitous across programming languages. They're structured so that they create a new variable (in this case, `i`) that takes on a different value every time you go through the code inside the loop. When you set up the loop, you both give the variable a name and you tell it what values you want it to take. In this case, we're taking advantage of some Rev shorthand (also used by R). If you type 1:4, it automatically creates a vector of all values between 1 and 4. This syntax is handy when you're dealing with consecutive integers. The code that is executed as part of the loop is contained inside curly braces `{ . . .}`. If the loop variable (e.g., `i`) is used in this code, it will change values every time you run through the loop. In the simple example below, we're just printing out the value of `i` every time we go through the loop.

```
for (i in 1:4){
    i
}
```

Now let's set up a for loop to do something more interesting. But we need one more trick. RevBayes has a lot of built-in functions that we can call to do interesting things. These functions always have this form - `functionName()`. The name of the function is followed by parentheses. Most functions will also have options that affect how they run. These options can be changed by passing different arguments to a function. In that case, the syntax looks like this - `functionName(functionArguments)`. The possible arguments are always specific to that function. In our case, we're going to use a function called `runifInt()`. This name can be broken up into these three parts

1. `r` (sample values from a distribution)
2. `unif` (in this case, use a uniform distribution)
3. `Int` (more specifically, use a uniform distribution across only integers)

A uniform distribution just means that we assign equal probability to all values included in the distribution. `runifInt()` takes three arguments

1. the number of samples you want
2. the lower bound on your uniform distribution
3. the upper bound on your uniform distribution

Using a for loop, we can see what it looks like to sample from this uniform distribution several times.

```
for (i in 1:10){
    runifInt(1,1,5)
}
```

While the specific output will vary each time you run this loop, because the sampling process is stochastic, you should see a series of values sampled roughly evenly between 1 and 5. One last thing to note, though, is that even when you only want to sample a single value from this distribution, the result is _returned_ as a list. A _return_ value is the thing that a function hands back to you when you call it. Sometimes, we just want to pull that single number out by itself, so that it's not nested in a list. Because we know `runifInt()` will return a vector, we can add a vector index to pull out the single number.

```
for (i in 1:10){
    runifInt(1,1,5)[1]
}
```

Do you see how the output changes? Ok, now it's time to put this all together. We are going to create a `for` loop that will draw samples from our sample space and create a new vector called `mySamples` to store the sampled values. Can you use each of the pieces of syntax we talked about above to break down how this `for` loop works?

```
for (i in 1:4){
    mySamples[i] = sampleSpace[runifInt(1,1,sampleSpace.size())[1]]
}
mySamples
```
