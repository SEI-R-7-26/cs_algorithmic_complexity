# Introduction to Algorithms, and Big-O 

## Overview

For today's morning exercise, we will learn some basic fundamentals of computer science, starting with algorithms and big-o notation.

## Objectives 

- Define "algorithm" in simple terms 
- Identify what Big-O notation measures 
- Be able to determine the Big-O notation of any given function 

## Intro to Algorithms 

> algorithm (n.) - a process or set of rules to be followed to attain a goal

Basically, algorithm is a fancy word for recipe. When we have a problem, we take a **series of steps to solve that problem**. 

Say I want a peanut butter and jelly sandwich, and Tyler agreed to make it for me. The problem is, he doesn't know how, how might we tell Tyler to make me
a sandwich?

> 1.  Go to the kitchen
> 1.  Find the bread, toaster, utensils, peanut butter, and jelly
> 1.  Toast the bread
> 1.  Using a knife or spoon, spread one slice of toast with peanut butter
> 1.  Spread the other slice of toast with jelly
> 1.  Place the two pieces of bread together
> 1.  `Return` to me with the sandwich (most important step)

That series of steps could be considered the algorithm to making a pb&j.

## Big-O Notation 

Now that we have a general overview of algorithms, let's talk about how we can measure an algorithm's efficiency. As you probably already know, there are many many ways to solve one problem. Or, in other words, there can be many algorithms to solve the same problem. In small scale settings like ours and when you're just starting out, that is perfectly fine and we will constantly harp on "as long as it works, that's good!" But in larger production scale apps, say for example Facebook, determining the efficiency of algorithms become very important. 

This is where Big-O comes into play.

### What is Big-O Notation?

Essentially, a simplified analysis of an algorithm's efficiency. This notation standardizes how we discuss the efficiency of algorithms. **What Big-O really tells us is how fast the runtime grows in comparison to the input size.** Most of the time, we use Big-O notation to describe _time complexity_ as we'll be focusing on, but it can also be used to describe memory efficiency.

For time complexity, we want to count how many times the code is run in context of how large the input to the code is. For example, O(1) is a very efficient piece of code, O(N!) is very inefficient. Let's break this down into categories of Big-O.

### Chart Summary of the Complexities

![](https://i.stack.imgur.com/jIGhf.png)


## `O(1)` Complexity AKA Constant Complexity 

O(1) means that an algorithm's runtime is static or constant. The complexity stays the same no matter the input.

```js
const helloWorld = (n) => {
	console.log('hello world');
}

const addFive = (n) => {
	return 5 + n;
}
```

In both of the above examples, no matter what size the `n` argument is, the functions will only run once. This is considered a highly efficient algorithm as it is independent of the input size.

<details><summary><strong>Click to see a graph charting the complexity</strong></summary><p>
	
![](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/big-o/english/8-Input-Size-Run-Time-Graph.png)

</p></details>

## `O(N)` Complexity AKA Linear Complexity 

O(N) complexity means that, as the input sizes increase, the processing time increases linearly. Or, more simply, the code runs once for each input.

```js
const iterateLoop = (n) => {
  for(let i =0; i < n; i++) {
    console.log(i)
  }
}
```

In the above example, if n is 1, the function will run 1 time. If n is 1000, the function will run 1000 times. The runtime grows linearly along with the input size. This type of complexity is considered decent efficiency.

<details><summary><strong>Click to see a graph charting the complexity</strong></summary><p>
	
![](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/big-o/english/6-Input-Size-Run-Time-Graph.png)

</p></details>

## `O(N^2)` Complexity AKA Quadratic Complexity 

O(N^2) complexity means that, the amount of time the algorithm takes to complete is increased by n * n! Hence, it is quadratic. 

```js
function consoleLogLots (arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      console.log(arr[i], arr[j])
    }
  }
}
```
For the array `[1, 3]`, this function will print:
```js
[1, 1]
[1, 3]
[3, 1]
[3, 3]
```

For a 2 item array, the code executes 4 times. For 3 items, the code executes 9 times.  This scales pretty fast -- for an array with 100 items this code will `console.log` 10,000 times! Unsurprisingly, this type of complexity is considered inefficient as its runtime grows quickly.

<details><summary><strong>Click to see a graph charting the complexity</strong></summary><p>
	
![](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/big-o/english/10-Input-Size-Run-Time-Graph.png)

</p></details>

## `O(log n)` and `O(n log n)` Complexity AKA Logarithmic Complexity 

O(log n) refers to algorithms which cut the problem in half each time. What do we mean by 'cutting in half'? Let's look at an exmaple.

### An Example 

One example of an O(log n) algorithm is a binary search. In an unsorted array, if we want to find the index of an item with a given value, we have to iterate through it and check if each item is equal to the item we are searching for. However, if we know that we have a _sorted array_, we can do this a lot easier!

For example, say we have an array `[1, 3, 5, 7, 9, 11, 13]` and we want to find the index of 5. We can do so like this: 

- Find the item at the midpoint of the array. This ends up being 7.
- Our item is below 7, so then, since our array is sorted, we only have to search the half of the array before the 7.
- The midpoint of the sub array from 1-7 or [1, 3, 5] is 3.
- This time, 5 is larger than 3, so we search the sub-array [5]. Since the midpoint of that array 5 is equal to the number we are searching for, we just return that number.

That sort of algorithm has a complexity of O(log n) as it cuts the problem in half each time until it finds the answer. This type of complexity is considered very efficient. The process might seem more complicated than a linear one, but it greatly reduces the time. 

<details><summary><strong>Click to see a graph charting the complexity</strong></summary><p>
	
![](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/big-o/english/9-Input-Size-Run-Time-Graph.png)

</p></details>

## How to Determine Big-O 

Now that we know some of the types of Big-O notation, how do we actually determine the type for any given function?

### General Rules for Determining the Big-O of an Algorithm 

1. When we calculate the Big-O of the function, we are calculating the _worst possible runtime case_ for a given function.
1. We always ignore constants / coefficients in order to _generalize_ the efficiency 

For these types of problems, ask yourself: 
- Does the function have to go through an entire list? If so, there's an N in that Big O class somewhere.
- Are there nested loops? That might give you O(N^2) (or worse).
- Does the function break the list into smaller chunks? You could have O(log(N)).
- Is the amount of work the same, regardless of the size of the dataset? That means it's O(1).

### Let's do some examples: 

What is the Big-O of this helloWord function?

```js
const helloWorld = (n) => {
  console.log(‘hello’);
  console.log(‘world’);
}
```

What is the Big-O of this bigO function? 

```js
const bigO = (n) => {
  x = 5 + 1; 
  for (let i = 0; i < n; i++) {
    console.log(i);
  }
}
```
