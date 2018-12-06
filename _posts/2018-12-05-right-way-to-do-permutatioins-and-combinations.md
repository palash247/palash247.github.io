---
layout: post
title:  Right way to do Permutations and Combinations
modified:   2018-07-31 23:00:19
excerpt: "Right way to do Permutations and Combinations."
categories: [maths,statistics]
comments: true
share: true
pinned: false
image:
    feature: https://raw.githubusercontent.com/palash247/palash247.github.io/master/img/rubik.png
    credit: Andrew Martin
    creditlink: https://pixabay.com/en/users/aitoff-388338/
---

So, I was reviewing all my high school stats from Khan Academy because I think my stats has got little rusty, and I got hooked with the way of teaching of Mr. Sal Khan. I remmember how I used to mug up the formulas of permutations and combinations without understanding the actual concept. This article is my version of the uderstanding I got from Khan Academy.

We will first start with a basic introduction how permutation and combination, then we will try to understand how their formulas are derived.

#### Permutation

It gives the number of ways you can arrange things with emphasis on the **order**. Best way to understand it is by going through an example. Suppose you've been asked to compute how many different sequence of Heads(H) and Tails(T) are possible if you toss a coin three times in a row? I will show you my reasoning behind this


1. How many positions do I have to arrange the H and T?
    - Ans: The coin was tossed $$ 3 $$ times in a row so I have 3 positions.
2. How many options do I have for first position?
    - Ans: A coin can have two outcomes, H or T, so I have 2 options for first position.
3. How many options do I have for second position?
    - Ans: 2, and same goes for the third position.
4. How many ways I can arrange all the options available to me for all the positions?
    - Ans: Simply multiplying each option should suffice, i.e, $$ 2*2*2 = 2^3 = 8 $$
5. Are there any repeating sequences that needs removal?
    - Nope.

The questions I have enlisted above has helped me a lot to arrive at an answers in combinatorics. If you know the number of positions, the number of options for each position and the impact of order, you can tackle any combinatorics question. You can now derive the formula for the **Permutations with Repetation** where you can repeat any element $$ (n) $$ for any number of times for the given number of positions $$ (r) $$ which is:

$$ 
    _nP_r = n^r
$$

Let's step up the difficulty level a little bit and try positions and options method to validate my point.

You have some letters $[F,I,C,D,E]$ and you are asked to calculate the number of 5 letter string that are possible by using them without repetation.

We will try to use the same reasoning we used before,

1. How many positions do I have to arrange the availabel letters?
    - Ans: I have 5 positions.
2. How many options do I have for the first positioin?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since, I have already selected on letter and I can not repeat it again, my set of options is reduced by 1, so I have 4 options now.
4. How many options do I have for the rest of the positions?
    - Ans: For position 3, 3 options, for position 2, 2 options and only one option for last position.
5. How many ways I can arrange all the options available?
    - Ans: $$5*4*3*2*1=120$$
6. Are there any repeating sequences that needs removal?
    - Nope.
  
See, I told you you can solve any permutation question using this reasoning, still don't believe me? Let's step up the difficulty little more. Don't you notice something? $$ 5*4*3*2*1 = 5! $$. You can generalize and derive another formula for **Permutaitions of n distict elements**:

$$ 
    _nP_n = n!
$$

What if, in the previous question, you had only 3 positions instead of 5?

Now, I am going to copy paste most of the stuff from above.

1. How many positions do I have to arrange the availabel letters?
    - Ans: I have 3 positions.
2. How many options do I have for the first positioin?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since, I have already selected one letter and I can not repeat it again, my set of options is reduced by $$1$$, so I have 4 options now.
4. How many options do I have for the third position?
    - Ans: For position $$3$$, $$3$$ options are available.
5. How many ways I can arrange all the options available?
    - Ans: $$5*4*3=60$$
6. Are there any repeating sequences that needs removal?
    - Nope.

The only differece we have here is we've stopped at third position. We can generalize this by using factorial. We just need to come up with a way to stop the factorial at desired position. In above example, we stopped at 3rd position because we had only 3 positions at our disposal. If we had all the 5 position, we would have continued the factorial using $$ 2*1 $$. How do you remove $$ 2*1 $$ from $$ 5! $$, simply, by divideing by $$ 2! $$. What is $$ 2! $$? It is factorial of total number of elements $$ n $$ minus the total number of positions at disposal $$ r $$ i.e, $$ (n-r)! $$ . This resulted into:

$$ 
    _nP_r = \frac{n!}{(n-r)!}
$$

Let's step up the difficulty again. What if you had some common letters in sample list to choose from? Consider the list $$[F,I,C,D,C]$$, you have two $C$ and other letters are unique. What is the total number of strings of length 5 that are possible using the elements of given list once. (Note: As $C$ appearse two times, you can use it two times.)

1. How many positions do I have to arrange the availabel letters into?
    - Ans: I have 5 positions.
2. How many options do I have for the first positioin?
    - Ans: 5
3. How many options do I have for the second position?
    - Ans: Since, I have already selected one letter and I can not repeat it again, my set of options is reduced by $$1$$, so I have 4 options now.
4. How many options do I have for the third position?
    - Ans: For position $$3$$, $$3$$ options are available.
5. How many ways I can arrange all the options available?
    - Ans: $$5*4*3*2*1=120$$ 
6. Are there any repeating sequences that needs removal?
    - **Yesssss!** I have two $$ C's $$ which can introduce some common sequences according to the way I calculated the total number of sequences. Consider, the list $$ [F,I,C,D,E] $$ in the previous question, our list is same with the difference of  second $$ C $$ in place of $$ E $$. Now, consider the two sequence for the list $$ [F,I,C,D,E] $$, $$ FICDE $$ and $$ FIEDC $$ both are different sequece. What if I replace the $$ E $$ with $$ C $$? I get two $$ FICDC $$ which should be counted as 1 only. This whould be true for every sequence possible with $$ [F,I,C,D,E] $$ which means we have counted every sequence twice. So we need to divide the total by 2. So, the final answer is $$ 120/2=60 $$.

Notice the reasoning in the last question I asked to myself. Why do you think we had to divide by 2? Why 2? Why not any other number? It is because by replacing the $$ E $$ with the second $$ C $$, you have removed the importance of **order** between them. You don't care in which order they apear because after the replacement you are going to get the same sequence. i.e, all the $$ CE $$ and $$ EC $$ are going to become $$ CC $$ no matter where they appear in the sequence. You are going to have all the sequnce repeated by some factor, and that factor is all the way you can arrange $$ C $$ and $$ E $$ in two positions. Which is $$ 2*1 = 2 $$. And hence you need to divide by 2. This question leads to the foundation of **Combinations** where order of the sequence does not matter. 