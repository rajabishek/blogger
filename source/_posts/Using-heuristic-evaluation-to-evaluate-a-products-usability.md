---
title: Using heuristic evaluation to evaluate a product’s usability
date: 2017-03-14 20:40:03
tags:
---

## Introduction
In a heuristic evaluation, usability experts review the product's interface multiple times and compare it against an accepted set of usability principles. This analysis is helpful in listing down the potential usability issues in the product. These principles or thumb rules are sometimes revised by the usability engineers to accommodate more findings.

<!-- more -->

## When should heuristic evaluation be done ?
The best way to find out usability issues and test the user experience is by testing the product with actual users. But conducting user tests is expensive and consumes more resources. User feedbacks are pricey and interpreting them is also time consuming process. In such cases using heuristic evaluation helps in identifying and minimizing usability problems with a much lower consumption of your limited resources.

Research also shows that a team of four usability experts would be able to discover 77% of the problems during an evaluation process. It is important to note here that this percentage of success is achievable only when evaluation is performed by experts and decreases with decrease in expertise and experience of the evaluators.

It is important to understand that a heuristic evaluation should not replace usability testing. This is because the issues identified in a heuristic evaluation are different than those found in a usability test. Instead it should be seen as a way for getting early feedback in the design process.

## How to perform Heuristic Evaluation ?
The basic needs to perform a Heuristic Evaluation includes
- 3 to 5 expert evaluators
- Observers who can assist the evaluators
- Evaluation manager (When there are no observers)
- Usability heuristics to evaluate

It is certainly true that some usability problems are so easy to find that they are found by almost everybody, but there are also some problems that are found by very few evaluators. Therefore it is highly recommended for evaluators to perform the evaluation process individually and correlate the data at the end to remove duplication. Working individually also makes sure that the evaluators are independent and evaluations are unbiased.

As the evaluators review the product they can verbalize their comments to an observer as they go through the interface. Or in the absence of observers the evaluators can record their observations as written reports. After the evaluation these written reports needs to be read and aggregated by an evaluation manager. Using an observer adds to the overhead of each evaluation session, but reduces the workload on the evaluators.

The observer can also assist the evaluators in operating the interface in case of problems. As we all know prototypes are only close to real products, there might be some dead ends or unstable conditions in prototypes. In certain cases when the evaluators have limited domain expertise and need to have certain aspects of the interface explained observers can help them with the interface.

## What are the Heuristic Principles ?
One of the well accepted usability principles is given by the [Nielson Norman group](https://www.nngroup.com/articles/ten-usability-heuristics/). Nielsen refined the list originally developed in 1990 by himself and Rolf Molich.

### Visibility of system status
The user must always be kept informed about the status of the system at all times with efficient feedback interactions. Appropriate feedback must be given within reasonable time to keep the users informed about what is going on with the product. For example after the user enter their credit card information a progress or loading indicator must be present to let them know that the website is processing the credit card details rather than just making them wait for minutes on a blank screen, making them wonder if their card details are being processed or if the website is down.
![Screenshot 1](/img/heuristic-evaluation/feedback.png)

### Match between system and the real world
The system’s communication with the user must be familiar to the user. The user should be able relate it with their real world equivalent. This might be regarded as one of the obsolete techniques, but still with the majority of population being unfamiliar with technology, it is important to give this principle a thought. For example a shopping cart system on a e-commerce website reflects the same shopping experience users have when they buy something from their local store.
![Screenshot 2](/img/heuristic-evaluation/real-life.png)

### User control and freedom
User should have the control to revert back their actions with the freedom to exit the system when they wish to, at all times. Control and freedom also includes easy navigation as the users use the product. They should be able to find their way through the site, be it to find a page or product, or to find the way back if they accidentally clicked on the wrong button or link. For example if you take Google Docs you always have the option to revert back to a previous version of the file and also quit the application whenever you like. On top of being able to quit the application at any time they have also made sure that you can quit without thinking about whether the document would have been saved or not, by making sure that the file is periodically saved.
![Screenshot 3](/img/heuristic-evaluation/revert.png)

### Consistency and standards
The system must follow standard interface conventions with user familiar terminologies that accommodates same meaning all over the system.
Fro example the application should avoid having inconsistent labels over buttons with same meaning. Lets say we have 2 pages from where the user can log out of the website, on one page if it says Sign Out on the other page the button must not use some other term like "Log Off" or "Shut Down". This inconsistency in design can cause confusion in users about what a particular call of action will actually do.
![Screenshot 4](/img/heuristic-evaluation/products.png)
![Screenshot 5](/img/heuristic-evaluation/cart.png)

### Error prevention
Humans are bound to make errors, the system should support the user in eliminating them. For example the auto suggestions menu in a search bar will prevent the user from making mistakes.
![Screenshot 6](/img/heuristic-evaluation/error-prevention.png)

### Recognition rather than recall
The application shouldn't expect the users to remember everything. It must provide assistance wherever possible to reduce the user's memory load. Example the system can help the user in categorizing their favorites/most used items instead of expecting them to remember how they did something last time.
![Screenshot 7](/img/heuristic-evaluation/recognition.png)

### Flexibility and efficiency of use
The system must prove to be useful and efficient for both novice and advanced users. For example Adobe products have shortcuts for professional users and have obvious alternatives for new users also. This helps in making sure that the system is designed in such a way that it proves to be efficient for both kinds of users.
![Screenshot 8](/img/heuristic-evaluation/novice.png)

### Aesthetic and minimalist design
User should be presented only with relevant data. More the relevant data more easy it is for the system to acquire user focus.

### Help users recognize, diagnose, and recover from errors
The system must help the user in recovering from errors. Error messages should be constructed with empathy. For example the error message that are presented to the users can be recognizable and constructive in nature.
![Screenshot 9](/img/heuristic-evaluation/bad-error.png)
![Screenshot 9](/img/heuristic-evaluation/friendly-error.png)

### Help and documentation
User should be provided with appropriate help documents both on line and off line about the system. The documentation must deliver effective steps for the users to accomplish their goals.
![Screenshot 9](/img/heuristic-evaluation/documentation.png)

## Summary
Though heuristics can never replace the conventional user testing methods it still could deliver a lot about a product’s broken usability and experience. Not every product manager/designer can afford the time, money or effort to perform user testing and heuristic evaluations could be the faster yet effective way to solve them.