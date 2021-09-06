---
layout: post
title:  "Are imaginary numbers real?"
categories: math
---

I took this weekend to binge watch on the phenomenal videos from [3blue1brown](https://www.youtube.com/c/3blue1brown). This led me to revisit complex numbers and how I never really grasped the intuition behind them... until now.

It was amazing to see how multiplying by `i` meant rotating a vector in the complex plane. And once I saw the applications it became quite clear why complex numbers were heavily used, especially in problems that require some kind of rotation or periodicity.

But along with that, the natural question came: do imaginary numbers really exist?

At first I was happy to think of them as just tools, nothing but means to an end. After all, there can't be such a thing as sqrt(-1), it just can't exist in nature. Therefore, `i` is nothing but a mathematical trick to simplify notations and calculations, but when applied to real things we should always get a real number in the end. Great! The whole nomenclature makes sense: real numbers are real and imaginary numbers are, well... imaginary.

But I kept on researching and, after some thought, I guess the real question ends up being: what do you mean by "really exist"?

Think of it: humans started with the natural numbers: 1, 2, 3, 4, 5... And that makes a lot of sense, those numbers were quite useful and meaningful. And then there were sums ("+") and multiplications ("x") and it was all algebraically closed (see [closure](https://en.wikipedia.org/wiki/Closure_(mathematics))) and life was good. But then... subtractions ("-"). The concept of taking away:

6 - 3 = 3  
5 - 1 = 4  
...   
2 - 2 = <span style="color:red">0</span>  
3 - 4 = <span style="color:red">-1</span>

The concepts of 0 and negative were not easy to digest for centuries. They could very well have been called imaginaries themselves.

> Prior to the concept of negative numbers, mathematicians such as Diophantus considered negative solutions to problems "false" and equations requiring negative solutions were described as absurd.  
Western mathematicians like Leibniz (1646–1716) held that negative numbers were invalid, but still used them in calculations. ([Wikipedia](https://en.wikipedia.org/wiki/Negative_number))

And if you think about it, 0's and negatives don't exist in nature neither. But they were surely nice abstractions that made math more powerful. Now, our set of numbers (the Integers) are closed algebraically for the operators "+", "x" and "-".

Here as well, one could say: zero and negatives are imaginary, they are just tools, means to an end. Similar to the argument of how imaginary numbers aren't real. But nowadays we learn all these numbers early in age, and therefore accept all of them as real. In fact, we accept all of the Real numbers as real. And even if we can accept 1/3 (0.33333) as real, it's harder to imagine an irrational number like π as real. After all, a number whose decimal expansion doesn't terminate nor repeats itself... how can it exist?!

That should start showing how fragile this concept of "real" really is. But before we get all philosophical with this, let's touch on the imaginary numbers. Similar to the negative numbers as we saw above, they actually come as a solution, making math more powerful. You see, the Real numbers are not a closed set on exponentiation. What real number answers this: x^2 = -1? Similar to the question: what natural number answers this: x = 3 - 5.

So, in the same way that we accepted zero and negative numbers, why can't we accept imaginary numbers? x^2 = -1 is solved by x = i or -i. And `i` doesn't live in the Real line. It's another dimension, forming the complex plane:

![Complex plane](/assets/imaginary_cycle.png)

And then we can see a great intuition: we can get from 1 to -1 by rotation 90 degress twice. So `i` is basically saying: rotate 90 degrees. If you do it twice in a row, i.e., i^2, then you get -1.

And by defining the sum and multiplication of complex numbers in a specific way, which is quite intuitive, the whole algebra works in the same way and we are left with a much more powerful set of numbers, now algebraically closed for exponentiation.

What is very interesting too is the whole history behind imaginary numbers. It is really fun to see how hard it was to accept them at the time, and how this whole intuition of considering them as another dimension and tightly related to rotations actually took a while after their invention. For more on that, I highly recommend [this series of videos](https://www.youtube.com/playlist?list=PLiaHhY2iBX9g6KIvZ_703G3KJXapKkNaF).

So, to the question of "are imaginary numbers real?", my answer is "as much as the other numbers". But seeing how elegantly this new set of numbers can be introduced just filling the gaps of the existing set and making things better without breaking anything, the bigger question we are left with is "are they an invention or a discovery?".

And since we've entered the philosophical field now, here is another piece of thought: even natural numbers aren't real. It's just that from our human perspective, which has evolved to discretize things, these numbers look natural. But if you think about it, nature in itself could be seen as just as a single continuous of energy. From the perspective of an X-ray, what we see as discrete units don't really exist. To nature itself, which is apathetic to any kind of human concept, there's no meaning to an individual element. It's all just one.

So, to wrap it all up, math as we _see_ (with its notations and rules) is an invention. There's no such thing as a `2` in nature, nor `sqrt(2)`. There's no exact measure in nature. There are no negative numbers. But the essence of math is natural and real: logical and reproducible. The existence of math itself is, to me, already a proof that nature is "mathematical". We wouldn't be capable of "doing math" if nature wasn't logical and reproducicle. So while the objects we use in math are not real, the underlying principles with which we derive an object from another are, i.e. the behavior and "motion" of these objects. To make it more concrete, think of this example: negative numbers aren't real, and the rules we have to operate on them aren't real neither, but they enable us to model things like "deacceleration" of change and reversal of motion, which, _if you go past the terms themselves_, is what is real. Therefore all the mathematical objects and rules we create are representations that, at their core, produce equivalent behaviors to those we can observe in nature.

So when we see `x^2 = -1`, to ask "what object solves it?" is to limit ourselves to the extent of our current invention. If instead we look at it and ask "can I solve it in a way that maintains the logical and reproducible nature of math?", then we are thinking in term of operations, in terms of what really exists. `sqrt(-1)` makes as much sense as `2` and `-1`. In nature, change is what matters. Same in math: it doesn't matter how we represent the objects, what is real and natural are the operations on them. The rest is invention.

Other references:
- [Interest rate of sqrt(-1)](https://www.youtube.com/watch?v=IAEASE5GjdI&ab_channel=3Blue1Brown)
- [Euler's formula](https://www.youtube.com/watch?v=ZxYOEwM6Wbk)
- [Do Complex Numbers Exist](https://www.youtube.com/watch?v=ALc8CBYOfkw)
