---
title: Snackbar - Android Material Design
date: 2016-09-16 11:24:34
tags:
---

## Better notifications
Material design includes another interesting component called as a snackbar. They are just like toast messages except they also provide action to interact with. And unlike toast notification which can exist independently of the application(even after the application was closed), snackbar messages feel more tied up with the application's user interface, as they are presented as a small bar sliding from the bottom of the screen. We can even swipe them off to dismiss them.

The are helpful in providing lightweight feedback about an operation. They show a brief message at the bottom of the screen on mobile and lower left on larger devices. They appear above all other elements on screen and only one can be displayed at a time.

<!-- more -->

## Plain snackbar
Below is the syntax of a simple snackbar. First step would be to import the `Snackbar` class from the material design package by placing `import android.support.design.widget.Snackbar` at the top of the java file. The `Snackbar` class has a factory method called as `make` that returns us an instance of `Snackbar`. The make method accepts three parameters. A view instance, message to display and the duration of the message.

The view instance passed as the first parameter is the view to find a parent from. Snackbar will try and find a parent view to hold Snackbar's view from the value given to view parameter. Snackbar will walk up the view tree trying to find a suitable parent, which is defined as a `CoordinatorLayout` or the window decor's content view, whichever comes first. If you would like to reduce this work done by android to find the parent you can instead directly pass the reference to the `CoordinatorLayout` as view parameter.
```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    coordinatorLayout = (CoordinatorLayout) findViewById(R.id
            .coordinatorLayout);
    Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
    setSupportActionBar(toolbar);
}
```
Once you have set the content view you can get the reference of the coordinator layout. In the XML file on the frontend make sure that the coordinator layout has the xml attribute `android:id="@+id/coordinatorLayout"`. Here the coordinatorLayout field is a variable on the Activity class that is of type `android.support.design.widget.CoordinatorLayout`. You can even make this field as private as it will be used only inside this class.

Having a `CoordinatorLayout` in your view hierarchy allows Snackbar to enable certain features, such as swipe-to-dismiss and automatically moving of widgets like `FloatingActionButton`. Therefore always try using a `CoordinatorLayout` view group whenever working with material design components.

The message parameter is a String object which is the message to be displayed by the snackbar. The duration parameter is of type `int` and you can provide either 0 or -1 or -2. 0 for longer time, -1 for shorter time and -2 for a message of indefinite time. For better code clarity and to make sure you are providing only either of these 3 values it is a recommended practice that you use one of the static final fields on the `Snackbar` class. The duration should be `Snackbar.LENGTH_SHORT`, `Snackbar.LENGTH_LONG` or `Snackbar.LENGTH_INDEFINITE`. Internally these static final fields on the `Snackbar` class map to these curresponding integer values. When `Snackbar.LENGTH_INDEFINITE` is used, the snackbar will be displayed indefinite time and can be dismissed with swipe off.
```java
Snackbar snackbar = Snackbar.make(coordinatorLayout, "Helloworld from Raj Abishek", Snackbar.LENGTH_LONG);
snackbar.show();
```

## Snackbar with an action
You can also mention a callback interaction method using `setAction(CharSequence, android.view.View.OnClickListener)` method. This allows us to take certain action when user interacts with the snackbar action button. The `setAction` method takes two parameters, first one is the name of the action button and the 2nd parameter is an instance of a class that implements the `OnClickListener` functional interface. Since lambda expressions are not yet supported in android we can make use of anonymous classes instead. As you can see below we are creating an object of an anonymous class that implements the `OnClickListener` and overrides the `onClick` method and passing it as the 2nd parameter.
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

## Customizing the snackbar
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

## Listening for snackbar visibility changes
To be notified when a snackbar has been shown or dismissed, you can provide a `Snackbar.Callback` via `setCallback(Callback)` method on the snackbar instance. The `setCallback` method expects an instance of a class that extends the `Callback` class. The `Callback` class is actually a nested public static abstract class of the `Snackbar` class. You pass an instance of a class that extends this abstract class to the `setCallback` method. We essentially set a callback to be called when this the visibility of this Snackbar changes.
```java
Snackbar snackbar = Snackbar.make(coordinatorLayout, "Helloworld from Raj Abishek", Snackbar.LENGTH_LONG);
snackbar.setAction("RETRY", new View.OnClickListener() {
    @Override
    public void onClick(View view) {
    }
});

snackbar.setCallback(new Snackbar.Callback() {
    @Override
    public void onDismissed(Snackbar snackbar, int event) {
        Log.v("MainActivity", "The snackbar has been dismissed.");
    }

    @Override
    public void onShown(Snackbar snackbar) {
        Log.v("MainActivity", "The snackbar has been presented.");
    }
});
snackbar.show();
```
The abstract `Callback` nested class of `Snackbar` class has empty implementations for both the `onDismissed` and the `onShown` method. Therefore we can override that empty implementations to provide our custom functionality when a snackbar is dismissed or presented on screen. The `onDismissed` method is called when the snackbar moves away from the screen(manually swiping or automatically after the time period.)