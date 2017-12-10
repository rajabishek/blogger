---
title: Helping blue collar workers manage their public transport needs
date: 2017-12-11 01:02:48
tags:
---

## Problem Overview
To design an an affordable and easy solution for blue collar workers to manage their public transport needs. The challenge is to design a solution that allows city dwellers to go easily between multiple public transport services, managing their daily, weekly and monthly needs. The goal is to help users plan for their travel and reach home early to spend time with their family.

## Target Audience
Constructions worker, maids and other blue collar workers who in particular use public transport for work commute. These users do not find using apps like Flipkart/Ola easy. 

<!-- more -->

## Discovery - Users in context
There are a couple of things I wanted to learn before working on the problem. Some of them are are follows:
- Who are these users? How technologically sound are they?
- How are they connected with technology and how what digital tools do they have access to?
- What is the day in life of a person who is just relying on public transport?
- What are the frustrations and pain points they face everyday with public transport?
- What does planning mean here? What would these users like to plan for?
- What are the frictions that causes users to not reach home early? How do they get delayed?
- And some features are already given in the problem, but are all these features even required and will they be used by our ideal user? If not how can it be designed better?
- How do these users make choices and what influences their purchasing decisions?
- What are some of the app these users are used to and how was their experience in using them? 


## Contextual Inquiry
With the help of my mom and a couple of my neighbors I was able to interview 5 different people under this category(people who rely on public transport for work commute). Each one of them told me about their objectives, frustrations, pain points and what they liked and didn’t like about their current experience. 

Interviewing and asking questions itself is a skill. You can’t just ask a user would you use this app, what don’t you like in this app? The questions have to provoke users to narrate a story or help them to recollect and give an example from past. And most often what users actually need is very different from what they tell you as a need. You have to be very cautious about taking everything seriously and just pick the sure ones while interviewing.

I usually start my interviews by writing down stuff that I would like to learn and change interview scripts based on the results from first few interviews. It's a list of known unknowns and I also keep some open ended questions to discover some unknown unknowns. While interviewing I use more of “When” rather than “What”, “How” or “Why” because asking “When”  always takes a user to a specific point in time and makes them narrate or tell you a story. In this way you get to understand the chain of cause and events. This helps you understand the true demand to deliver the right things on the supply side.

## User Experience Mapping
Using all this data I was collectively able to put out a simple user experience map. The yellow are the objectives and goals of the user, the pink are the the frustrations and the pain points and the green ones are the happiness points(things that users like about the current system).

![Screenshot 1](/img/public-transport/mapping1.jpg)

## Learnings about the user:
- All the 5 of them had android phones
- All the phones were less than 8000INR
- None of them had mobile data on their phones
- Only 3 of them use simple apps like whatsapp, while the rest only use it only for calls
- None of them have made an online payment before and also don't want to also make one in the future. They feel it's dangerous.
- They are only comfortable with clicking and are very slow while typing on mobile
- Most importantly. They are only comfortable with their native languages(tamil in this case for all 5) and cannot read english


## Learnings about their problem:
- They know which bus to take(the bus numbers), but they don’t know when the bus would arrive as they work timing varies
- With local train transportation 2 of them they were fairly comfortable with the the timings but the rest didn’t know the exact time at which the train would arrive
- One of the main reason why they would get delayed is because of lack of awareness about the bus and train schedules
- One lady would call her next owner and tell them that she would be in their house by 20mins, but she would be delayed because she isn’t aware about the bus/train timings
- Another lady had to walk all the way up till the autostand and actually even further(because auto stand charge higher) to get a ride.
- They don’t take all buses and only use the whiteboard one as they are cheaper compared to the blue colored and yellow colored ones.
- Getting a bus at the right time is purely luck, sometimes you would get a bus just as you come to the bus stop but sometimes you have to wait for a long time.
- They all wish they get direct buses, if not they will have to change bus stops and also wait there for the next bus.
- Planning for them means postponing a certain work for later(cleaning bathroom/cleaning shelves) or completing their work fast knowing that they have to leave early for the day and sometimes informing when they will come for work to their next owner.
- Most of them do not use autos, but rarely they take one if they get delayed too much. But they are very conscious about how much they have to pay and are only ready if the auto drive puts the meter on during the ride.
- The most disheartening moment is when you get into the station and see the train leaving, wish you could have come a minute early


## User Personas
User personas can be very effective in providing consistent design solutions if they are used in the right way. The persona document is kept simple with only the major details like goals, frustrations, technology awareness and a description and was used as a blueprint during the design process.
![Screenshot 3](/img/public-transport/persona.png)


## Storyboarding
For these kinds of projects where retaining empathy is very important storyboards are a great tool and can always be used as a reference. I stick it in front of my desk and this helps me remember the frustrations and remind me constantly about the reason why this app is being designed and for whom it is being design for under which situations.
![Screenshot 4](/img/public-transport/storyboarding.jpg)

## Jobs to be done - JTBD Framework
By writing down job stories it becomes easier to understand why people hire your product for. Situations and circumstances force people to look out for tools and they certainly hire every product to accomplish their job. I believe that understanding the actual job for which the product is hired for is more important than understanding about the user. 

Unlike user stories, job stories provides as much context as possible and highlights the motivation instead of just the implementation or the action that is important for the user. It follows the order Situation-Motivation-Expected Outcome. Based on the user research there we 3 important job stories:
- Before leaving my house I would like to see the bus/train timings so that I can call and inform my next owner so that I can reach there on time.
- When I know that I am going to finish work I would like to see the timings for white board buses(cheaper) so that I can finish my work earlier.
- When I know that I am going to finish work I would like to see the timings direct buses so that I need no change bus stops to reach home.
- When I know that I am going to finish work in a place I would like to book an auto that can come to my place so that I need not walk long way to hail a auto and spend time on looking for an auto.


## Ideation, B = MAT framework
Typically during the ideation process I use the B = MAT framework to ideate on design solutions to solve a user problem. Every behaviour should have these 3 components in place for the behavior or action to occur - Motivation, Ability and Trigger. When we use the MAT analysis and think through these terms it pushes us to question and improve every single component that we introduce inside the application. 

The ideation process is focussed at increasing the motivation, reducing the ability and improving the trigger(right kind and at the right time) to cause the intended behavior.
I also always do an exercise as to what I call as CSS diagramming to get a better idea on what is the actual problem here and what “better” means for the user.

A CSS diagramming activity is very simple. Based on the research we write down the current situation, the current solution that is used to deal with the situation and the bad results that we would like to improve. Then we write down the better result i.e if a good solution is in place what problems would it solve and then we try to find out the new solution that brings this change. The delta between the current result and the better results is the progress here.
![Screenshot 5](/img/public-transport/css.png)

## Unique selling propositions
Now it is clear that if there needs to be sufficient motivation for someone to use this product it must have the following abilities without fail:
Support native languages
Search and look for buses that are cheaper and direct
Look for the next train time at a particular station
Ability to hail an auto where I am clear about pricing and charges
Work without internet

## Low Fidelity - Paper Sketches
Now that I have a good understanding about the actual needs, the users and their problems, I started prototyping in low fidelity. Low fidelity design and prototyping allows you to quickly validate assumptions without wasting a lot of time(designing directly all the screens on software).

But the biggest challenge for me here was that all my prototypes should be in Tamil language so that I can collect feedback. And I don’t know to write tamil. So I took some help from my friend to help me translate from English to Tamil. In Fact the entire of prototyping was done in Tamil so that all users were able to use the interface and give inputs.
![Screenshot 6](/img/public-transport/low-fidelity1.jpg)
![Screenshot 7](/img/public-transport/low-fidelity2.jpg)

Some of my assumptions:
- The app will be easy to use if it only involves clicking and typing is completely avoided wherever necessary
- The app will be easy to use if it picks the most searched/most used data as the default ones instead of asking the user every time
- The easiest way to show the train timings is to ask for the from station and to station
- Both arrival and departure time is important for users while showing the train and bus schedules.
- It will be less scary for Kanika if she is clear about pricing before booking a auto. She will feel better if she is kept clearly told about the pricing.
- It’s less scary for Kanika if the app doesn’t ask her for the payment method and only has cash as an option so that she need not worry about the money in her bank
- Stick bottom button are a good way to guide the user through the intended experience, one main call to action on every screen.
A bottom navigation bar would make it easy for users to switch from one service to another

![Screenshot 6](/img/public-transport/low-fidelity3.jpg)
![Screenshot 7](/img/public-transport/low-fidelity4.jpg)

Low fidelity designs clearly proved that some of my assumptions were wrong:
- Users don’t prefer and also are not concerned about the to station, they are only here to know the train arrival timings in a particular station. What made more sense was asking for the direction, towards which side are they taking the train
- The sticky footer button confuses them, they think it of a label or heading rather than a button, users have to see the 4 corners and the border with some shadow depth to understand that it is tappable.
- Both arrival and departure time confuses users and make the app look more complicated for them. They prefer and care only to see the arrival times.
- The bottom navigation bar is common pattern in iOS and these users are not used to using this kind of interface in any of the android apps before. Infact adding the bottom navigation bar only occupied more space and reduced the readability of the screens. However they are very comfortable using the back button(hardware button) on the mobile to get back to previous screens.



## Low Fidelity - Prototyping
Once there was some clear direction about design The low fidelity prototype was designed in the native language of the user and had moved through 3 iterations in total to get to the final version. You can find the final version of the prototype here:
<iframe src="https://marvelapp.com/4835e05?emb=1" width="390" height="755" allowTransparency="true" frameborder="0"></iframe>

![Screenshot 8](/img/public-transport/low-fidelity5.jpg)
![Screenshot 9](/img/public-transport/low-fidelity6.jpg)


Above is the image of the user interacting with the final prototype version. You can learn about some of the learnings I got from usability test below. The usability test were conducted multiple times and the designs for updates to reflect the feedback and slowly improved over time.


## Learnings from usability tests
- Don't select the default language by default as English on the first screen, users keep clicking on the options wondering what to do next
As these users are not used to complex interfaces, reduces the number of choices at every screen and if possible ask only one question at a time
- Recent searches doesn’t make sense here, as they typically search for the same thing again and again. Therefore populate the most used data as the default values.
- While displaying the train/bus schedules, users first look at the first cell in the list, so highlight there instead of adding a separate section on top.
- Don't show both the timings(arrives at and departs at), only the arrives at timings is enough. This gives them an estimate on when the train/bus will arrive so that they can plan their work accordingly.
- The time is important that the remaining mins
- Pictorial representation is helpful for them to understand the context and take quicker actions, especially when they have to make a choice 
- Do not use sticky bottom buttons, they are not used to this pattern, they need to see all the 4 border with some margin around them to identify it as a clickable item.
- Navigation is a problem. Most users found it really hard to go back to search for other service. For example after looking a train schedule, users are stuck and unable to see bus schedules/ book autos.


## High Fidelity
You can find the link for the high fidelity prototype here:
<iframe src="https://marvelapp.com/32ibc3e?emb=1" width="390" height="755" allowTransparency="true" frameborder="0"></iframe>
Gestalts principle and complexion reduction principle were used or the UI design. If you observe over the last year some of the design leaders like Facebook, Airbnb and Apple have followed a similar technique to simplify products and drive users towards the engineered direction. The main principles of this new trend is to use bigger, bolder headlines, simple thin and recognizable icons and extraction of color. The idea is to remove color and use it extremely sparingly to indicate the main call to actions.

## Conclusion
The app may not look fancy, but it is designed for ease of use and intuitiveness. During the final usability tests, all users were comfortable and confident with using the app and provider the exact information that they were looking for. Some words from the users themselves(all translated from Tamil to English):
- Can you install this app for me?
- Did you work on this app. Its very simple and easy to use.

