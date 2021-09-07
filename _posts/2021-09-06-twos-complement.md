---
layout: post
title:  "Two's complement"
categories: miscellaneous
---

Following up on my previous post, on the intuition behind Karnaugh maps, in this one I'll talk about the principles behind our preferred way of representing negative numbers in computers: two's complement.

In a similar way, when I was first presented to this method of representation and how nicely things just worked out (you could use normal binary addition to handle negative numbers and subtractions), I wanted to understand why this worked. Again, classes were unsatisfying in that realm. For this one in particular I don't remember taking the time to explore myself, so the deeper understanding never really stuck with me. So I've decided to fill this gap now. What I present below are three pieces of intuition behind the magical behavior of two's complement.

### Intuition #1: friendly overflows
If you are working with a limited number of bits, there's one built-in way to perform subtraction through addition: overflow.

```
  111 = 7
+ 011 = 3
  ---
 1010 = 10
```

If we are limited to working with 3 bits and therefore we drop the leftmost bit above, we are effectively subtracting 8 (or 1000 in binary).

```
  111 = 7
+ 011 = 3
  ---
 X010 = 2
```

There lies one of the keys for intuition #1: we are naturally able to subtract our overflow bits through addition.

So let's say we want to subtract 3 out of 7, which would give us 4. How can we leverage this limited ability to subtract through addition so that we can subtract any other number?

That means we have `7 - 3 = 4`, but how can we get rid of the inexisting subtraction operator. Gladly, based on the key above, we can write:

```
7 - 3 = 4

<=>

7 - 3 + 8 = 4 + 8

<=>

7 + (-3 + 8) = 4 + 8
```

If you think about it, that means we can always work with adding positive numbers and then rely on the overflow to subtract what we need.

Notice that this also means that it doesn't matter how many bits we are working with, all of those are equivalent:

```
7 + (-3 + 16) = 4 + 16

7 + (-3 + 32) = 4 + 32

7 + (-3 + 64) = 4 + 64

7 + (-3 + 128) = 4 + 128
```

In fact, it doesn't even have to be a power of 2, it just has to be any number that we will drop after via overflow: any number where the digits we work with are 0 and the other leftmost digits are any non-zero combination of bits (from this we can derive the intuition behind the [sign extension](https://en.wikipedia.org/wiki/Sign_extension) operation used in some multiplication algorithms).

Of course, using more bits than necessary is just a waste, so we can work with the minimum, which is just an additional leftmost bit of 1.

So what is `(-3 + 8)`? `5`. If you think of it, we are effectively asking what is the complement of 3 to reach 8 (that's what subtraction is about anyways). And that's why it's called two's complement. The "two's" part is because it's base 2 (binary). So we can represent -3 in this addition as 5, which is the two's complement of 3. If we sum 5 and the result overflows, then by dropping the leftmost bit we are subtracting 8, and therefore having effectively added -3 in the end. Magic! One interesting way to look at the two's complement of `n` is: the number that by adding `n` to it, it overflows.

This can also be visualized graphically:

```
 loop / overflow / subtract by 1000 (8 in decimal)
 -----
 |   |
111  |  7
110  |
101  |  5, which is 3 steps away from overflow
100  |  4
011  |  
010  |
001  |
000  |
 ^   |
 |----
```

If you start from 7 and walk 5 steps (which is 3's complement) you end up in the answer: 4. That's because 5 - 8 = -3, and by making the number overflow we effectively subtracted 8.

While that is great for enabling subtractions that result in non-negative numbers, we still have two problems:
- We can't perform additions/subtractions that result in a negative number.
- To store negative numbers we have to store them in sign and magnitude, and then get their two's complement when it is time to add them to another number.

It would be great if we could have a binary representation of negative numbers that solved the two problems above. And that's where the second part of the intuition comes into play.

### Intuition #2: negative representation

One of the conclusions from our visualization above is that the number 5 when added and causing overflow has the effect of "walking back 3", i.e., subtracting 3. That's because it is 3 steps away from overflowing, so a number added to it has to "waste 3 steps" to start from 0, which is effectively subtracting 3 from the number. By the same logic, a number that is 2 steps away from overflow has the effect of subtracting 2. And so on, leaving us with the following visual representation:

```
loop / overflow / subtract by 1000 (8 in decimal)
 -----
 |   |
111  |  -1
110  |  -2
101  |  -3
100  |  -4
011  |  -5
010  |  -6
001  |  -7
000  |  -8
 ^   |
 |----
```

Where each negative number is represented by its two's complement:

- The negative form of 1 is the two's complement of 1: 7 (111);
- The negative form of 2 is the two's complement of 2: 6 (110);
- The negative form of 5 is the two's complement of 5: 3 (011).

Note how we can do -1 + -2 = -3. That's because -1 is making the -2 number "walk 1 back", through the same overflow trick as before. Also note how, if we were able to add a positive number we would be getting the correct behavior: 101 (-3) + 1 = 110 (-2). And how 111 > 110, which matches the fact that -1 > -2. That's all derived from the fact that we are walking "backwards" with the representation of negative numbers, which is derived from the fact that the two's complement of the smallest number is the greatest number.

But despite all these cool features of the two's complement, now we have the reversed problem from before:

- We can't perform additions/subtractions that result in a _positive_ number.
- To store _positive_ numbers we have to store them in sign and magnitude, and then get their two's complement when it is time to add them to another number.

### Intuition #3: divide and conquer

Finally, to solve the problems of both approaches, we can simply arbitrarily split the numbers, letting part of them be positives and part of them be negatives. Here is one example:

```
loop / overflow
 -----
 |   |
111  |  -1
110  |  -2
101  |  -3
100  |  -4
011  |  -5
---  |
010  |  +2
001  |  +1
000  |  0
 ^   |
 |----
```

As you can see, we can still get all the benefits from the previous solutions, because the same principles remain the same. The only drawback is that now we can represent fewer negative and positive numbers.

The problem with this arbritrary split is that it becomes harder to detect overflows and invalid operations. For example: 1 + 2 = 3, which doesn't have a valid representation, and therefore should indicate to us a bad overflow. However, to detect that the result 011 is a bad overflow it would be rather tricky.

The way to simplify this is to split in half, so that the leftmost bit can also represent a sign bit. This will enable us to much more easily detect invalid results.

So we have:

```
loop / overflow
 -----
 |   |
111  |  -1
110  |  -2
101  |  -3
100  |  -4
---  |  
011  |  +3
010  |  +2
001  |  +1
000  |  0
 ^   |
 |----
```

### Bonus: easy reading of two's complement

Convert the following number to base 10: 10101.

People would do: 16 + 4 + 1 = 21.

Now assume the number is in two's complement, what is the negative number in base 10?

You can calculate it in a way that is very similar to the above: -16 + 4 + 1 = -11.

Why? Because calculating the two's complement in this case is effectively calculating 32 - the number, which is `32 - (16 + 4 + 1) = 11`. And we want the negative of the two's complement, so:

```
- [32 - (16 + 4 + 1)]

<=>

(16 + 4 + 1) - 32
```

And because we have the convention that all negative numbers in two's complement are represented with the most significant bit 1, then we always have 16 - 32, which is -16. Therefore, we can think of the leftmost bit as a negative and all the other bits as usual. So 10101 is -16 + 4 + 1 = -11.

So this trick is simply derived from the concept of two's complement itself along with the convention that all negative numbers have the most significant bit 1.

### Final notes

It may seem that the intuition is a lot more complex. But if you think about it, we've not only explored why the two's complement works, but during the way also noticed how many other choices are available, and why we end up preferring the one we use today. Without this mental exercise, we wouldn't even know of different possibilities.

This gives a much deeper understanding of what is behind the whole representation of negative binary numbers in two's complement. And even though that could all have been shown through algebra, by having the visualization it enables us to better grasp the details, by engaging our visual thinking, making it easier to later apply it to other problems.
