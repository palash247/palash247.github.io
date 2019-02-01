---
layout: post
title:  Right way to do Permutations and Combinations
modified:   2019-01-30 23:00:19
excerpt: "I was reviewing all my high school stats from Khan Academy because I think my stats have got little rusty, and I got hooked with the way of teaching of Mr. Sal Khan. I remember how I used to mug up the formulas of permutations and combinations without understanding the actual concept. This article is my version of the comprehension I got from The Khan Academy."
categories: [statistics]
tags: [maths, statistics, permutations, combinations, combinatorics]
comments: true
share: true
pinned: false
use_math : true
# image:
#     feature: https://raw.githubusercontent.com/palash247/palash247.github.io/master/img/rubik.png
#     credit: Andrew Martin
#     creditlink: https://pixabay.com/en/users/aitoff-388338/
---

I was reviewing all my high school stats from Khan Academy because I think my stats have got little rusty, and I hooked up with the way of teaching of Mr. Sal Khan. I remember how I used to mug up the formulas of permutations and combinations without understanding the actual concept. This article is my version of the comprehension I got from The Khan Academy.

We will first start with a basic introduction to permutation and combination, then we will try to understand how their formulas are derived.

## Permutation

Permutation gives the number of ways you can arrange things with an emphasis on the **order**. Best way to understand it is by going through an example. Suppose you've been asked to compute how many different sequences of Heads(H) and Tails(T) are possible if you toss a coin three times in a row? I will show you my reasoning behind this

1. How many positions do I have to arrange the H and T?
    - Ans: The coin was tossed $ 3 $ times in a row so I have 3 positions.
2. How many options do I have for the first position?
    - Ans: A coin can have two outcomes, H or T, so I have 2 options for the first position.
3. How many options do I have for the second position?
    - Ans: 2, and the same goes for the third position.
4. How many ways I can arrange all the options available to me for all the positions?
    - Ans: Simply multiplying each option should suffice, i.e, $ 2\*2\*2 = 2^3 = 8 $
5. Are there any repeating sequences that need removal?
    - Nope.

The questions I have enlisted above has helped me a lot to arrive at an answer in combinatorics. If you know the number of positions, the number of options for each position and the impact of order, you can tackle any combinatorics question. You can now derive the formula for the **Permutations with Repetition** where you can repeat any element $ (n) $ for any number of times for the given number of positions $ (r) $ which is:

$$
    \begin{align\*}
        _nP_r = n^r
    \end{align\*}
$$

Let's step up the difficulty level a little bit and try positions and options method to validate my point.

You have some letters $[F, I, C, D, E]$ and you are asked to calculate the number of 5 letter words that are possible by using a letter without repeating. The words do not need to have any meaning.

We will try to use the same reasoning we used before,

1. How many positions do I have to arrange the available letters?
    - Ans: I have 5 positions.
2. How many options do I have for the first position?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since I have already selected one letter and I can not repeat it again, my set of options is reduced by 1, so I have 4 options now.
4. How many options do I have for the rest of the positions?
    - Ans: For position 3, 3 options, for position 2, 2 options and only one option for the last position.
5. How many ways I can arrange all the options available?
    - Ans: $ 5\*4\*3\*2\*1=120 $
6. Are there any repeating sequences that need removal?
    - Nope.
  
Don't you notice something? $ 5x4x3x2x1 = 5! $. You can generalize and derive another formula for **Permutations of n distinct elements** i.e, number of ways you can arrange $n$ distinct elements within $n$ positions:

$$
    \begin{align\*}
        _nP_n = n!
    \end{align\*}
$$

What if, in the previous question, you had only 3 positions instead of 5?

Now, I am going to copy paste most of the stuff from above.

1. How many positions do I have to arrange the available letters?
    - Ans: I have 3 positions.
2. How many options do I have for the first position?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since I have already selected one letter and I can not repeat it again, my set of options is reduced by $1$, so I have 4 options now.
4. How many options do I have for the third position?
    - Ans: For position $3$, $3$ options are available.
5. How many ways I can arrange all the options available?
    - Ans: $5\*4\*3=60$
6. Are there any repeating sequences that need removal?
    - Nope.

The only difference we have here is we've stopped at the third position. We can generalize this by using factorial. We just need to come up with a way to stop the factorial at a desired position. In the above example, we stopped at the 3rd position because we had only 3 positions at our disposal. If we had all the 5 positions, we would have continued the factorial using with $2x1$. How do you remove $ 2x1 $ from $ 5! $, simply, by dividing $5!$ by $ 2! $. What is $ 2! $? It is factorial of total number of elements $ n $ minus the total number of positions at disposal $ r $ i.e, $ (n-r)! $. This can be generalized to:

$$
    \begin{align\*}
        _nP_r = \frac{n!}{(n-r)!}
    \end{align\*}
$$

Let's step up the difficulty again. What if you had some common letters in the sample list to choose from? Consider the list $[F, I, C, D, C]$, you have two $C$ and other letters are unique. What is the total number of words of length 5 that are possible using the elements of the given list exactly once? (Note: As $C$ appears two times, you can use it two times.)

1. How many positions do I have to arrange the available letters into?
    - Ans: I have 5 positions.
2. How many options do I have for the first position?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since I have already selected one letter and I can not repeat it again, my set of options is reduced by $1$, so I have 4 options now.
4. How many options do I have for the third position?
    - Ans: For position $3$, $3$ options are available.
5. How many ways I can arrange all the options available?
    - Ans: $5\*4\*3\*2\*1=120$
6. Are there any repeating sequences that need removal?
    - **Yesssss!** I have two $ C's $ which can introduce some common sequences according to the way I calculated the total number of sequences. Consider, the list $ [F,I,C,D,E] $ in the previous question, our list is same with the difference of  second $ C $ in place of $ E $. Now, consider the two sequence for the list $ [F,I,C,D,E] $, $ FICDE $ and $ FIEDC $ both are different sequence. What if I replace the $ E $ with $ C $? I get two $ FICDC $ which should be counted as 1 only. This would be true for every sequence possible with $ [F, I, C, D, E] $ which means we have counted every sequence twice. So we need to divide the total by 2. So, the final answer is $ 120/2=60 $.

Notice the reasoning in the last question I asked to myself. Why do you think we had to divide by 2? Why 2? Why not any other number? It is because by replacing the $ E $ with the second $ C $, you have removed the importance of **order** between them. You don't care in which order they appear. Because, after the replacement, you are going to get the same sequence. i.e, all the $ CE $ and $ EC $ are going to become $ CC $ no matter where they appear in the sequence. You are going to have all the sequence repeated by some factor, and that factor is all the way you can arrange $ C $ and $ E $ in two positions. Which is $ 2\*1 = 2 $. And hence you need to divide by $2$. This question leads to the foundation of **Combinations** where the order of the sequence does not matter.

## Combinations

Let's try another problem. You have some letters $[F, I, C, D, E]$ and you are asked to calculate the number of ways you can choose $3$ letters without repeating given that the **order** of choosing the letters does not matter?

1. How many positions do I have to arrange the available letters into?
    - Ans: I have 3 positions.
2. How many options do I have for the first position?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since I have already selected one letter and I can not repeat it again, my set of options is reduced by $1$, so I have $4$ options now.
4. How many options do I have for the third position?
    - Ans: For position $3$, $3$ options are available.
5. How many ways I can arrange all the options available?
    - Ans: $5\*4\*3\*2\*1=120$ permutations.
6. Are there any repeating sequences that need removal?
    - **Yesssss!** Suppose we chose three letters $F$, $I$ and $C$. These three letters can be arranged in 6 possible ways viz, $FIC$, $FCI$, $CFI$, $CIF$, $IFC$ and $ICF$. Since the order in which the letters are chosen/arranged does not matter, these 6 arrangements should be counted as $1$. This is true for any three letters chosen from the list. So, to calculate the combination, we need to divide the permutations by the number of ways it is possible to arrange 3 letters in 3 positions.

$$
    \frac{_5P_3}{3!} = \frac{120}{3!} = 20
$$
In general, number ways of choosing $r$ elements from the set of $n$ distinct elements irrespective of the order can be derived as follows:

$$
    \begin{align\*}
        _nC_r = \frac{_nP_r}{r!} = \frac{n!}{r!(n-r)!}
    \end{align\*}
$$

This should be it. Of course, you need the practice to master this topic. The aim of this article is to convey the idea of doing permutations and combinations without depending on the formulas. I derived the formula to help you relate article with your textbooks. Please leave a comment if you like the post or if you have any suggestions.

Thank you.