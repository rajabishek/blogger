---
title: Snackbar - Android Material Design
tags:
---
## Better notifications
Material design includes another interesting component called as a snackbar. They are just like toast messages except they also provide action to interact with. And unlike toast notification which can exist independently of the application(even after the application was closed), snackbar messages feel more tied up with the application's user interface, as they are presented as a small bar sliding from the bottom of the screen. We can even swipe them off to dismiss them.

<!-- more -->

## Simple Snackbar
Below is the syntax of a simple snackbar. First step would be to import the `Snackbar` class from the material design package by placing `import android.support.design.widget.Snackbar` at the top of the java file. The `Snackbar` class has a factory method called as `make` that returns us an instance of `Snackbar`. The make method accepts three parameters. A view instance, message to display and the duration of the message.

Normally passing `CoordinatorLayout` as view param is the best option as it allows Snackbar to be dismissed via swipe and automatically takes care of moving of widgets like `FloatingActionButton` as the snackbar slide in and out. The message parameter is a String object which is the message to be displayed by the snackbar. 

The duration parameter is of type `int` and you can provide either 0 or -1 or -2. 0 for longer time, -1 for shorter time and -2 for a message of indefinite time. But typically for code clarity and to make sure you are providing only either of these 3 values it is a recommended practice that you use one of the static final fields on the `Snackbar` class. The duration should be `Snackbar.LENGTH_SHORT`, `Snackbar.LENGTH_LONG` or `Snackbar.LENGTH_INDEFINITE`. Internally these static final fields on the `Snackbar` class map to these curresponding integer values. When `Snackbar.LENGTH_INDEFINITE` is used, the snackbar will be displayed indefinite time and can be dismissed with swipe off.
```java
Snackbar snackbar = Snackbar.make(coordinatorLayout, "Helloworld from Raj Abishek", Snackbar.LENGTH_LONG);
snackbar.show();
```

## Snackbar with an action
You can also mention a callback interaction method using `setAction` method. This allows us to take certain action when user interacts with the snackbar action button. The `setAction` method takes two parameters, first one is the name of the action button and the 2nd parameter is an instance of a class that implements the `OnClickListener` functional interface. Since lambda expressions are not yet supported in android we can make use of anonymous classes instead. As you can see below we are creating an object of an anonymous class that implements the `OnClickListener` and overrides the `onClick` method and passing it as the 2nd parameter.
```java
Snackbar deletedMessage = Snackbar
        .make(coordinatorLayout, "Message is deleted", Snackbar.LENGTH_LONG)
        .setAction("UNDO", new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Snackbar restoredMessage = Snackbar.make(coordinatorLayout, "Message is restored!", Snackbar.LENGTH_SHORT);
                restoredMessage.show();
            }
        });
 
deletedMessage.show();
```

## Customizing the Snackbar
Snackbar comes with default white color text and `#323232` background color. You can override these colors as mentioned below.
```java
Snackbar snackbar = Snackbar.make(coordinatorLayout, "Helloworld from Raj Abishek", Snackbar.LENGTH_LONG);
snackbar.setAction("RETRY", new View.OnClickListener() {
    @Override
    public void onClick(View view) {
    }
});

// Changing action button text color
snackbar.setActionTextColor(Color.BLUE);

View snackbarView = snackbar.getView();
// Changing background color of the snackbar
snackbarView.setBackgroundColor(Color.GREEN);
TextView textView = (TextView) snackbarView.findViewById(android.support.design.R.id.snackbar_text);
// Changing message text color
textView.setTextColor(Color.BLACK);
snackbar.show();
```