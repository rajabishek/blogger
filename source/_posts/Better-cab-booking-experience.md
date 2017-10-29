---
title: OLA Cabs - Designing a simpler cab booking experience
date: 2017-10-29 15:15:51
tags:
---

## Project details
Recently I found my colleague Sanjay, booking a cab for his mother. I wasn't shocked when he told me that his mom doesn't book a cab by herself. Sanjay's mom owns a smartphone and is comfortable using apps like youtube and whatsapp. When she can youtube and whatsapp, how is that she is finding it difficult to book a cab?

As a designer I wanted to fix this. My instinct told me, if the design could be more user centered, Sanjay's mom should be able to make a booking by herself.

## Problem Statement
Designing a simpler cab booking experience with minimum friction to allow many such Indian mom's to book a cab without anyone's help.

<!-- more -->

## Things to learn
As a first step I started writing down on a higher level some of the things that I wanted to learn from user interviews.
- Where are users struggling with the current app to make a booking
- Why aren't still many people confident enough to make a booking by themselves
- For limited mobile users, what are the basic interactions they are familiar with.

## Picking users for interviews
This wasn’t as difficult as I assumed it to be. Since OLA is a popular cab booking app used in India, I was able to find quite a number of users without much difficulty. I wanted to go out of my circle to interview different kinds of users, but die to the lack of time I just interviewed people inside my circle whom I already knew as OLA users.

I decided to do multiple interviews instead of a predefined fixed number of them and settle down when I had enough learnings with me.

I interviewed around 10 people on Saturday and each interview on an average lasted for around 15-20 minutes. 2 were done on phone calls, while the rest of them was done in person. I prefer doing in person interviews especially for these kinds of tasks where users are easily accessible.


## Known Unknowns
Based on the things I wanted to learn, I started writing down questions that I wanted to ask during the interviews. The actual questions that we asked slightly varied from one person to another based on their response. But in general these were the kind of questions that were asked:

- Can you introduce yourself? What do you do? Where do you work?
- Which cab booking service do you use?
- When is the last time you booked a cab?
- What device do you use ? Do you have mobile data every time?
- Do you feel that with OLA app, the cab booking is time consuming?
- Do you prefer using OLA every time?
- When do you end up not using OLA cabs? 
- Can you take me to a specific point in time and narrate this incident for me?

One nice trick that I employed during user interviews was to use more of when rather than why. Asking when resulted in users taking me to a specific point in time, describing the incident as a story that gave me more context into the problems they had. The more stories they had to share, I was able to discover the chains of cause and effect leading up to usage on the demand side(what users actually needed) to build the right things on the supply side(the solution that I built for them).

## Unknown Unknowns
I also kept some space at the end of every interview to ask some open ended questions that to discover some unknown unknowns too. Questions like:
- Is there anything else that you would like to tell me?
- Is there something I should have asked but I didn't?

## User Personas
Personally I am not a very big fan of user personas but I decided to go ahead with this as it gives a sense of consistency while designing solutions. Based on the interviews they were two important personas.

## User Journey 1 
- Isai is a homemaker
- Her mother Chandra is a cancer patient and has to be taken to the hospital for treatment.
- She takes her mom to the same hospital every 2 days.
- She gets a confirmation for her mother’s appointment only an hour in advance
- She calls her son Sanjay to book a cab for her when he is at work
- Her son books an OLA cab with pickup point as his house address
- He guides the cab driver when he finds it difficult to reach the address
- He keeps checking the map to see where the cab driver is as he has to inform his mom 10 mins before as his grandmother is slow walking down the stairs.
- If he doesn’t inform 10 mins before the cab arrives the drives calls him and trouble hims. He has to explain - every time that he has made a booking for his mom and grandmother.
- He also tells his mom not to pay because he has added the payment method as card and the app pays automatically once the ride is complete
- Sometimes Isai’s son is busy with office work and is not able to book a cab and she ends up calling the local travels to arrange for a car. But this is expensive and it's not affordable every time. In these cases she takes an auto while coming back.
- Once Isai arrange for local travels vehicle and also Sanjay ended up booking a cab later for him mom. Sanjay has to cancel the OLA booking later as he didn’t know that his mom arrange another mode of transport.
- Isai doesn’t book a cab by herself though she has a smart phone with OLA app installed because she is not used to modern interfaces.
- Isai’s son tried teaching her how to use the app once, but still she doesn’t remember and is afraid of booking as it has a lot of options.
- Isai is aware of basic mobile interactions and uses apps like youtube and whatsapp. In either case she doesn’t type much on phone(she is very slow at typing and is not very comfortable with that) and primarily uses mobile to consume content(watching whatsapp videos, watching videos on youtube etc).

## Persona Document
The persona document is simple with only the major details about the goals, frustrations, technology awareness and a basic description about Isai.
![Screenshot 1](/img/cab-booking/persona.png)

## Storyboarding
For each persona I also wanted to draw a rough storyboard, which can be used as a reference throughout my design process.

![Screenshot 1](/img/cab-booking/storyboarding.jpg)

Ideation
Before ideating on a good solution for a problem, I always do an exercise as to what I call as CSS diagram mapping to get a better idea on what is the actual problem here and what “better” means.

A CSS diagramming activity is very simple. Based on the research we write down the current situation, the current solution that is used to deal with the situation and the bad result that we would like to improve. Then we write down the better result i.e if a good solution is in place what problems would would solve and then we try to find out the new solution. The delta between the current result and the better results is the progress here.

![Screenshot 1](/img/cab-booking/ideation.jpg)


## Low fidelity - wireframing & prototyping
Now that I had a good understanding about the user, their problems and the actually need for a good solution here. I started prototyping and iterating in low fidelity to validate my assumptions.

Some of my assumptions:
- It's a lot easier for Isai is the app has a similar interface like Whatsapp that she is already used to, but with more interactions on clicking rather than typing
- It's easier for Isai if the app doesn’t ask for the pickup location and picks the current location by default
- It’s easier for Isai if the app doesn’t ask for the drop location and presents the recently travelled ones for selection
- It’s less scary for Isai if the app shows the pricing of the cabs upfront before a booking rather than after ending the ride
- It’s easier for Isai if the app doesn’t ask her for the payment method and picks cash by default so that she can control over the money
- It’s better for Isai if she is called by someone from OLA for a confirmation about the booking
- It’s better for Isai if she is aware about the cab arrival time as she can plan to lock her house and bring her mom down

![Screenshot 1](/img/cab-booking/view-hierarchy.jpg)

With some usability testing and questions I was able to validate the effectiveness of my solution my presenting them to Isai and by seeing how comfortable and simpler it was for now to book a cab.

## High fidelity prototyping

<iframe src="https://marvelapp.com/109fbj46?emb=1" width="452" height="800" allowTransparency="true" frameborder="0"></iframe>

Once I was clear about the entire flow and what works well for Isai I was able to prototype the design in high fidelity using the Marvel app and get more feedback.

Below is a photo of Isai using the interface herself. A few words from Isai - “Did you make the app? This is very easy to use.” (Translated from Tamil to English)

![Screenshot 1](/img/cab-booking/high-fidelity.jpg)
