---
title: BoxMail - Design to Production
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

To keep the on boarding process interesting and short its better to provide guidance as the users use the app rather than presenting all the features upfront. The startup tutorial can be used to explain just the main feature of the app. Its a good practice to keep the number of screens fewer than five.

![Screenshot 2](/img/inbox-mail-app/getting-started.png)

To also help the user identify the current screen we should always highlight the corresponding bottom circle. This gives them information about the number of such screens and also an idea about how much they have progressed. The user may already be familiar with the app, probably they are installing it on their new phone. Therefore there should always be a way for the users to skip through the tutorial and use the app directly.

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
- Navigate to compose mail screen easily.

As you can see above all these information needs to be shown on the inbox screen for every email. Thats a lot of information to deal with and it needs to be presented in a nice way. It should appear natural.
![Screenshot 3](/img/inbox-mail-app/inbox-screens.png)
The users can bring the compose email screen by clicking the pencil icon. This design idea was taken from the principles of material design. A floating action button can be used to represent the primary action in an application. Only one floating action button is recommended per screen to represent the most common action.

## Inbox Actions
Users find it useful if they can quickly takes actions for the email. Actions such as archiving and rescheduling and an email are common tasks. Swiping an element in a list is a common action that iOS users are already aware of.
![Screenshot 4](/img/inbox-mail-app/inbox-actions.png)
The users can swipe rightwards to schedule an email and they can swipe leftwards to archive an email. The swiping method is perfectly suitable for scheduling or archiving an email because it is a common task that users would do frequently, but not for a group of emails. If it was a action that is usually performed for a group of emails then the better interface would be to allow them to select the emails first and then perform the action.

## Compose Mail
The another important screen in the mail app is the screen that allows users to type out email and send them. As the user types out the recipient's email address the email address would change to a pill that contains the photo and the name of the recipient. By adding the photo of the recipient the user can quickly verify the details and send the email. The right side screen shows the notification message when the email has been successfully sent. By keeping the color translucent the notification can seem to be more pleasant and less annoying in nature.
![Screenshot 5](/img/inbox-mail-app/compose-mail.png)
Its also a good practice to give a reasonable amount of padding on the left and right hand side of the message text box. As you can see above we have a lot of inputs to take in from the user such as email addresses, subject, message, cc, bcc. Adding labels for each elements would occupy a lot of space and would be distracting for the user, placeholder texts can come in handy in such places.

## Message & Sidebar
Reading lengthly emails is hard, lets make the process enjoyable. The email screen needs to show the email and provide an option to download the file. Placing an icon for the type of attachment such as pdf, image, word files cam be useful because in most cases users will be expecting certain files via email. Showing the number of attachments can be helpful especially when there are lot of attachments in the email. The three action icons at the bottom help in replying, replying to all and forwarding the message. These are common actions that a user would take and deserves an explicit place on the screen instead of being hidden somewhere.
![Screenshot 6](/img/inbox-mail-app/message.png)
The sidebar is a common user interface in mobile apps to bring navigation links for the user. The right side screen shows the navigation bar which slides from the left. It helps the user in navigating to the different screens of the app and also show the recent notifications. When presenting any type of navigation element its important that we highlight the current place where the user.

The number inside the small circle can help choose the need for navigation. If there are no mails in drafts why should I bother navigating to that screen. These small little things can make a lot of difference in the user experience. If the small circle was there the user would need to navigate to the drafts screen and then find out that there are no emails there. The small drop down icon near the profile image of the user can be used to switch email accounts.

## Settings
The user must be able to customize the app to suit his needs. This is the place where the user would add and remove email accounts. Customize the notifications and get support from the company. Since there are a lot of settings that the user can customize its a good idea to divide into sections as shown below.
![Screenshot 6](/img/inbox-mail-app/settings.png)
Account management in one section, navigation in another and social interaction in another. Similarly the disclosure indicator in the settings can be helpful to the user to let that know that there is more and they will be navigated to another screen. This is a common practice followed in iOS apps in general.

## Xcode
Keeping engineering in mind is also an important quality while designing. There is no point in designing something if can't be actually made. No designer would like to work on something only to be told that it can't be practically done. But anyway the designs that we have worked on are very simple and requires only a reasonable amount of effort to bring them to life.
![Screenshot 7](/img/inbox-mail-app/xcode-screenshot.png)
The above image shows the screenshot taken after writing code in Xcode and running the app in iPhone 6 simulator. Since the design that we created is a lot different from what a typical boilerplate that Apple would give for iOS apps, every little user interface element like a button, or navigation bar or the placement of icons needs to be completely customized. 
