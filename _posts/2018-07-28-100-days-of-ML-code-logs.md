---
layout: post
title:  100 days of ML code logs
modified:   2018-07-31 23:00:19
excerpt: "My everyday progress logs of the #100daysofMLCode challenge."
categories: [logs]
comments: false
page.share: false
image:
    feature: https://raw.githubusercontent.com/palash247/palash247.github.io/master/img/100daysofmlcode.jpg
    credit: Siraj Raval
    creditlink: https://www.youtube.com/watch?v=cuQMBj1cWPo
---

My everyday progress logs of the #100daysofMLCode challenge.


### Date: 27/07/2018:

For the day, I revisited the derivation for the back-propagation algorithm. I struggle with writing differential equations for matrices. The only way I could come up with the proper differentiation is by matching the dimensions of the matrices. I don't know if it's the correct way of doing Linear Algebra-Calculus, but for now, it is working for me. For reference, I've used the first course of Andrew Ng's Deep Learning specialization from Coursera.

### Date: 28/07/2018

Read an article by Randal J. Barnes about Matrix Differentiation. I found it interesting and now I know how to backpropagate without matching the dimensions of the matrices involved in the differentiation. Then I went back to the maths of forwarding and backward propagation of Deep-L layer neural network from Andrew Ng's Deep Learning course. Now I feel a little more confident about the derivation and I hope I would not forget it soon. I think I should make flashcards about this real soon.

### Date: 29/07/2018

Downloaded assignments from Coursera as they don't let you redo your assignments after completing the certifications. Now, I have a copy of every ipython notebook assignments of Deep Learning course. I don't know if its illegal, but I find it helpful to solve problems while revising, so I will keep them. For the day, I've completed the Deep-L layer NN assignment from the first course of Deep Learning Specialization. And there's one more project I am working on which allows you to schedule a message on a message platform. Today, I've explored different third-party APIs to automate message sending on WhatsApp and then I went with Selenium web driver as it appears to all the third party APIs are doing it the same way. I've successfully shared text message through Selenium but then I had to grant the access permission every time I ran the application which sucks. I found solutions for it and I've tried some with no luck I will try more soon. Also, I learned how to set up a VNC server on a cheap digital ocean droplet which will help me with this selenium automation. Another thing is I am trying to wake up at 4 am but I am struggling with going to sleep early. I will keep on trying though. That's it for the day.

### Date: 30/07/2018

Today, I struggled to wake up at 4 am again. Next day I will try harder. For the day, I've configured Twilio with the chatbot I am building for my company. Before that, I was engaged in the generating more stories (conversation flows) for the bot to tackle mistakes it was doing. Before that when I woke up at 6 am I went through some modular way to implement fully connected NN with any architecture. Tomorrow I will try a little harder to wake up at 4.

### Date: 31/07/2018

The struggle with the early waking up is still on. In the morning I revised L1, L2 Regularization, Dropout for reducing over-fitting and for the rest of the day I was stuck with the [Asterisk][Asterisk] configuration for setting up a [Duplex like AI agent][Duplex like AI agent]. I am learning a way to set up packages so that a user can call an AI agent and have a meaningful conversation with it.
[Asterisk]:https://www.asterisk.org/
[Duplex like AI agent]:https://medium.com/rasa-blog/building-your-own-duplex-ai-agent-using-rasa-and-twilio-bbd23c80ed30
### Date: 01/08/2018

Finally, woke up at 4 am. Implemented He Initialization to tackle the problem of vanishing/exploding gradients in NNs, then L2 and Dropout to perform regularization and reduce over-fitting and then implemented Gradient Check to validate the implementation of back-propagation. In the office, I've successfully integrated Twilio's Programmable Voice & Speech recognition APIs with Rasa chatbot. I am really excited about this project and I will make a tutorial for it real soon.



### Date: 30/10/2018
#### Slept: 11:30 pm
#### Woke up: 5:10 am

Starting the challenge again. I was expecting too much from myself which resulted in me being depressed and guilty of not doing everything that is possible. I've stopped smoking a month ago and also started working out at least 6 days a weak. Recently, I am feeling a little better about myself and hence I want to continue this challenge from where I left. 

Learning from previous mistakes, I've changed the definition of a successful day. It's only minimum 1 hour of focused work on machine learning which makes up the successful day. Anything extra would be a bonus.

Wrote stories for a chatbot (office work). Read about [how to manage multiple git/bitbucket SSH keys on a single machine](https://medium.freecodecamp.org/these-tools-will-help-you-write-clean-code-da4b5401f68e). And posted on the blog again.

Today's target:

Primary:
1. Complete the chatbot
2. Read at least two chapters of Pandas for data analysis.
3. Run 2 km
4. Go to Gym
5. Complete the backlog reprots.

May be:
5. Find a way to integrate any type of task planner in the jekyll theme.
6. Integrate it with current theme.