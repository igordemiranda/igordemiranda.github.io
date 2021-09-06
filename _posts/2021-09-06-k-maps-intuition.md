---
layout: post
title:  "The intuition behind Karnaugh maps"
categories: miscellaneous
---

In my second year of college, in the Digital Circuits class, I was introduced to Karnaugh maps as the tool to help us simplify Boolean algebra expressions, and therefore create an optimized version of our digital circuits based on a truth table.

![Karnaugh map](/assets/karnaugh-map.jpeg)

I was amazed by the tool! You could group the 0's or the 1's and for some strange reason that would simplify the expression. Magic, right?!

I've always been of the kind to want to understand things at a deeper level. There has always been an itch when I see a beautiful tool without any explanation of why it works. So of course I asked my professor "Why does it work?". The answer did not answer it. So I tried a few more times over a few classes, rephrasing the question in hopes that the previous one was just not fully understood. But to not avail.

So one weekend, I decided to take the task for myself. The first biggest question to me was: "Why is the order 00, 01, <span style="color:red">11</span>, 10? Why not 00, 01, <span style="color:red">10</span>, 11?". So I spent a while exercising Karnaugh maps, trying to create different types of tables, trying to retrace Karnaugh's steps in his finding. After a few hours, I had finally understood why. Now, instead of memorizing the map, I could reconstruct it myself. And even expand it to larger truth tables that we haven't seen in class! The itch had finally been scratched! During classes and exams I could now solve any simplification of Boolean expressions with a deeper intuition, without depending on just memorizing a tool. This was so powerful that even now, about 7 years later, I was still able to rebuild the Karnaugh map when I needed to. That certainly wouldn't have been possible if all I had done was memorizing it.

This itch was present in other classes too. In fact, it has always been there and it's still here. Even at work I always try to understand things at a deeper level, and I believe that's what enables me to more quickly solve things by myself going forward. It starts with a slower ascent, but soon enough the growth is exponential. You can start deriving answers and finding patterns that others can't.

And it's deeply moving when you see the intuition behind things. In fact it's beautiful. I see myself doing more of that in the near future, sharing these kinds of intuitions with the world, first via this blog, then via videos. Similar to what [3blue1brown](https://www.youtube.com/c/3blue1brown) does for math, I want to do that for Computer Science and Software Engineering.

Anyway, here was my finding of why Karnaugh's map is the way it is: the bits are ordered in a way that "neighboring cells" only switch a single bit. This enables neighboring cells to be grouped together, eliminating the inputs represented by the bits that change, since those aren't relevant for producing the same output (if they were relevant, a change in their value would change the output). Because inputs are only irrelevant when all of its values can be ignored in that group, and because we are working with binary inputs, that means the groups have to be powers of 2.

Knowing this, this quote from [Wikipedia](https://en.wikipedia.org/wiki/Karnaugh_map) explains it best:
> The Karnaugh map reduces the need for extensive calculations by taking advantage of humans' pattern-recognition capability.

Therefore, Karnaugh had first understood the principle behind simplification: find the largest groups with irrelevant inputs. And then reshaped the truth table in a way that allowed for these largest groups to show patterns in space, which we humans are optimized to do... to some extent. When you go to 5 inputs and beyond the K-maps are not so intuitive anymore. There are still some ways to format the table in a way that eases the process, but the "neighoring" cells are not so clear on a 2D plane (piece of paper) anymore, and therefore require an additional layer of mental work. Still, a lot easier than without the tool.

And, to be clear, finding the intuition behind something is quite different from actually discovering it. The latter is much harder and should not be deemed small in any way. Still, finding the intuition behind something enables you to more easily invent in different domains. In this case, next time you find yourself with a problem that you want to make easier for humans, you can try reshaping the problem in a way that leverages our pattern-recognition capability. That's the beauty of understanding the "why" behind solutions. And behind the beauty there is usually a general principle.
