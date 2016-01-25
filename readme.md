
---

| Title | Type | Duration | Name | City |
| --- | --- | --- | --- | --- |
| Activity Lifecycle | Lab | "1:00" | James Davis | NYC |

---  
# Activity Lifecycle Lab

## Introduction

Below, you will find three scenarios, and questions following each one.

To the best of your ability, answer the questions **in english**, not in code.

Below the scenarios, you will find a few questions. Answer those however you'd like.

Answer the questions by editing this readme, pushing your changes to your forked repo, and making a pull request.

## Exercise  


####Scenario 1:

Let’s say you made a To Do list app, where you can add things to a list and cross them off. You decide to cross some items off the list and mark them as complete.

When you rotate the device, the things you marked as complete are no longer crossed off.

**Question**: Why did this happen?
<br />**Answer**: When the screen is rotated the activity is destroyed and recreated. If the things are no longer showing as crossed off after the rotation, that means their state is not being saved. When onCreate, onStart, and onResume run after the rotation, they are not aware of the state of each View object prior to the rotation, and end up recreating the layout the same way it was created in the first place.

**Question**: How do you fix this issue?
<br />**Answer**: One option is to save the state of each item in the ListView as a boolean (crossed off = true / not crossed off = false) in a Bundle object in the onSaveInstanceState method. Then in onCreate you could check if data was saved in the savedInstanceState Bundle object, and if so use those boolean values to set the status of each item as needed.


####Scenario 2:

The Amazon Kindle Android app allows you to open and read eBooks. You discovered a bug! You opened a book, and read it from the beginning up to page 68. Then, you left the app and closed it completely so you can do other things.

When you opened the app again, and opened the book, it started from page 1 (and not page 68 where you left off)!

**Question**: How would you fix this issue?
<br />**Answer**: In the onPause method I would create a SharedPreferences object, initialize it using getSharedPreferences, and use its putInt method to save an integer representing the last read page (68). Then in the onResume method I would create another SharedPreferences object, initialize it via getSharedPreferences, and use its getInt method to retrieve the last read page (using whatever key value I saved it with in putInt) and then go to that page in the book. If the getInt method returned the default value (i.e. if no last read page had previously been saved) I would then go to page 1 of the book.


####Scenario 3:

Facebook for Android added a feature last year where, if you started writing a comment on someone’s post and decided not to do so, the app would save a draft of it just in case you changed your mind.

Take this scenario. On a post on Facebook, you click the “comment” button (which opens a new CommentActivity). You start writing a comment, and then change your mind by pressing the back key (which closes the CommentActivity). You click on the “comment” button again, and in the newly-opened CommentActivity, the comment you were writing is still there.

**Question**: How would you implement this feature? Be specific; what lifecycle methods would you use in CommentActivity, and what techniques would you use?
<br />**Answer**: In the onPause method of the CommentActivity I would save the draft comment by creating a SharedPreferences object, initializing it with getSharedPreferences, then using its putString method to save contents of the EditText object (which I would get via the EditText object's getText method, then call getString on the that). Then in the onResume method of the CommentActivity I would check if any data was stored in Shared Preferences by creating a SharedPreferences object, initializing it via getSharedPreferences, using its getString method to retrieve the draft comment string, and if that string is not null, then populate the EditText object with that string (using the setText method of the EditText object).



In your own words…
==================

**Question**: What are the methods of the Activity Lifecycle?
<br />**Answer**: onCreate, onStart, onResume, onPause, onStop, onDestroy

**Question**: What order are the methods called?
<br />**Answer**: When an activity is first activated: onCreate -> onStart -> onResume. When an activity is finished or if the user hits back, or if the app is closed: onPause -> onStop -> onDestroy.

**Question**: What is a bundle?
<br />**Answer**: A bundle is an object that holds a collection of key/value pairs. You can "put" values into the bundle with a key for each value, then later you can retrieve or "get" those values from the bundle by specifying the value's key.

**Question**: How do you get the Shared Preferences of an app?
<br />**Answer**: Declare a new SharedPreferences object, then initialize it by setting it equal to the return value from the getSharedPreferences method.
