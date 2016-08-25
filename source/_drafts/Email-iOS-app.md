---
title: Design to Production - iOS Email Client
tags:
---

## Usefulness + Simplicity
I was very particular in not reinventing the wheel. I wanted to use interface elements that all mobile users are already used to. Users must be able to recognize what it’s for and how to use it.
<!-- more -->

Usefulness and simplicity is the key. If the application is not useful, there is no reason why the user will want to use it, and at the same time no one would bother spending time learning how to use your app. The app has to be simple and self explanatory. 

Before staring out with the UI design for the screens I had a few ideas in mind. Not that I am unhappy with the current email clients for iOS, I wanted the app to be very intuitive and at the same time aesthetically appealing in nature. The user shouldn't be navigating screens for the commonly used tasks and at the same time we can't clutter all the options on the main screen also, there has to be a balance.

## Typical workflow
Engineering time is precious. After weeks of programming we can't ask the developer to change the elements suddenly and rework on what they have done. This is why designing and prototyping is so essential is a software development life cycle. Its makes everyones life easier. The typical work flow that I carry out while building a project is:

1. Ideation and brainstorming 
1. Listing out the functional & non-functional requirements
1. Wire framing and deciding user flows
1. User experience & designing interfaces
1. Giving visual finesse & Pixel perfecting the designs
1. Prototyping interactions
1. Programming & Implementation

> If a picture is worth 1000 words, a prototype is worth 1000 meetings.
-- **@ideo**

Today its not enough showing the design screens alone to the client. What if the client can actually touch and use a dummy version of the app to get a feel of it. All this happens even before we write even a single line of code. Today's tools and software are so powerful that they allow us to make prototypes that are so close to the original app. Developing prototypes and getting approval before starting can save so much time, effort and money. The final working app would look exactly the same as the prototype but will have all of the functionality built in.

## On-boarding Screens
The on boarding process is a critical step in setting your users up for success with your product, but there are a number of considerations and hard decisions to be made when you are designing your on boarding to define how best to get your users familiar with your product and its value.

![Screenshot 1](/img/inbox-mail-app/onboarding-screens.png)

**Avoid long tutorials**
Its not a really good idea to put the user through swiping several screens in the name of getting them started. Its a good practice to keep the number of screens fewer than five.

**On-boarding must be contextual and progressive**
Rather than presenting all the features up-front, its better to provide guidance as they use. The startup tutorial can be used to explain just the main feature of the app.

![Screenshot 2](/img/inbox-mail-app/getting-started.png)

## Inbox Screens
The inbox screen in the most important screen of all in the mail application. People receive hundreds of emails everyday, they have to deal with all this data and be able to take quick actions based on the message. At the very basic the user must have the following options.

- User should be able to differentiate between unread and unread emails
- The sender, subject and the date of the email should be visible
- It should be also clear whether the mail has any attachments
- User must be able to see the date of the email
- The message should also indicate whether its a conversation and if so the number of conversations
- A part of the body must be visible
- The photo of the sender has to be visible for easy identification
- The user must be able to differentiate between normal and scheduled emails
- The emails need to be separated (Primary/Social/Promotions)

As you can see above all these information needs to be shown on the inbox screen for every email. Thats a lot of information to deal with and it needs to be presented in a nice way. It should appear natural.
![Screenshot 3](/img/inbox-mail-app/inbox-screens.png)

## Inbox Actions
Users also need to take quick actions to email.
![Screenshot 4](/img/inbox-mail-app/inbox-actions.png)

## Compose Mail
![Screenshot 5](/img/inbox-mail-app/compose-mail.png)

## Message
![Screenshot 6](/img/inbox-mail-app/message.png)

## Settings
![Screenshot 6](/img/inbox-mail-app/settings.png)

## Xcode
![Screenshot 7](/img/inbox-mail-app/xcode-screenshot.png)