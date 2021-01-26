# Frequentist Probability

Now we are going to change our sample space, so that the outcomes have a more interesting biological meaning. In this case, we are going to imagine that we are sampling individual organisms from some population (say, a population of salamanders). Individuals can have four possible phenotypes:

1. large and striped
2. large and spotted
3. small and striped
4. small and spotted

We will say that the population vector holds all individuals in our population. While, in this case, we could simply tally the phenotypes of every individual in this vector, we will not do that here in order to maintain our thought experiment. In almost any real biological population, we would not know precisely how many individuals it contained and we could not survey all of their phenotypes.

```
population = ["large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","large_striped","small_striped","small_striped","small_striped","small_striped","small_striped","small_striped","small_striped","small_striped","small_striped","small_striped","small_striped","large_spotted","large_spotted","large_spotted","large_spotted","large_spotted","large_spotted","large_spotted","large_spotted","large_spotted","large_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted","small_spotted"]
```

To estimate what the frequencies of the four phenotypes might be in our population, we will draw random samples. To do this, we can use the same RevBayes syntax as above, with one new skill. As we draw samples, we will want to tally the number of times we've sampled different phenotypes.  The first thing we'll need to do is to set up a variable to hold the number of times we've sampled each phenotype. In this case, we'll use a vector (`phenoCounts`) that will have four integers. Each value stores the number of times we've sampled one of the four phenotypes listed above. Then, we'll build a for loop to sample from our population and store the counts.

```
for (i in 1:4){
    phenoCounts[i] = 0
}

numSamples = 20
for (s in 1:numSamples){
    sample = population[runifInt(1,1,population.size())[1]]
    if (sample == "large_striped"){
        phenoCounts[1] += 1
    } else if (sample == "small_striped"){
        phenoCounts[2] += 1
    } else if (sample == "large_spotted"){
        phenoCounts[3] += 1
    } else if (sample == "small_spotted"){
        phenoCounts[4] += 1
    }
}
print(phenoCounts)
```

We can transform the counts to frequencies by dividing the entire vector by the number of samples we've drawn.

```
phenoCounts/numSamples
```

Ok, now we'll run this whole sampling procedure with 20 samples per replicate 10 times so that we can see how consistent our estimates are.

```
for (rep in 1:10){
    for (i in 1:4){
        phenoCounts[i] = 0
    }

    numSamples = 20
    for (s in 1:numSamples){
        sample = population[runifInt(1,1,population.size())[1]]
        if (sample == "large_striped"){
            phenoCounts[1] += 1
        } else if (sample == "small_striped"){
            phenoCounts[2] += 1
        } else if (sample == "large_spotted"){
            phenoCounts[3] += 1
        } else if (sample == "small_spotted"){
            phenoCounts[4] += 1
        }
    }
    print(phenoCounts/numSamples)
}
```

How variable are each of the frequencies across replicates? Now we'll run this same procedure again, but drawing 100 samples per replicate.

```
for (rep in 1:10){
    for (i in 1:4){
        phenoCounts[i] = 0
    }

    numSamples = 100
    for (s in 1:numSamples){
        sample = population[runifInt(1,1,population.size())[1]]
        if (sample == "large_striped"){
            phenoCounts[1] += 1
        } else if (sample == "small_striped"){
            phenoCounts[2] += 1
        } else if (sample == "large_spotted"){
            phenoCounts[3] += 1
        } else if (sample == "small_spotted"){
            phenoCounts[4] += 1
        }
    }
    print(phenoCounts/numSamples)
}
```

According to the __frequentist__ interpretation of probability, the probability of an event (like sampling a large, striped individual) is defined by its long-run frequency. The long-run frequency is the frequency of an event over a very large number of trials. So, the frequencies above (from 100 samples) are estimates of each event's true probability. However, because we have only drawn a finite number of samples (e.g., 100), our estimates have some error. The fact that our estimates become more precise as we draw more samples is known as the [Law of Large Numbers](https://en.wikipedia.org/wiki/Law_of_large_numbers). Let's run this one more time with 1,000 samples.

```
for (i in 1:4){
    phenoCounts[i] = 0
}

numSamples = 1000
for (s in 1:numSamples){
    sample = population[runifInt(1,1,population.size())[1]]
    if (sample == "large_striped"){
        phenoCounts[1] += 1
    } else if (sample == "small_striped"){
        phenoCounts[2] += 1
    } else if (sample == "large_spotted"){
        phenoCounts[3] += 1
    } else if (sample == "small_spotted"){
        phenoCounts[4] += 1
    }
}
print(phenoCounts/numSamples)
```
