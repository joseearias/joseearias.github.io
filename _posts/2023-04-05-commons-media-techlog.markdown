---
layout: post
title:  "Technical Log: Wikimedia Commons Media App"
date:   2023-04-05 12:39:15 -0500
categories: technical-log
---

This is the technical log for my pull request to the Wikimedia Commons “apps-android-commons” repository. Here you will find a description of the issue that I’m solving with this pull request and also a description about the solution I used to solve the issue. 

## Description

Wikimedia Commons is a non-profit media repository of free-to-use images, sounds, videos and other media. They maintain several different repositories on Github, and one of them is the apps-androids-commons repository, which hosts the codebase for their open source Android application which serves as a platform for users to upload their own original content to the official Wikimedia Commons media repository.

The project codebase it’s open source and it’s maintained by a community of developers and other collaborators. The project is written mostly in Kotlin and Java as the code in the repository is for an Android application. The Wikimedia Commons application can be found on the Google Play Store. 

## Issue’s description

The application allows both logged-in users and non-logged-in users to see a “Explore” section where the user can see some of the featured images of the day. By clicking an image the user will be able to see details about the image or media of interest. There are several fields, like author, location, description, etc. 

When a logged-in user tries to access the author of an image or media by clicking the username they will be shown the author’s achievements and statistics according to the number of media they have uploaded to the site. This is the expected behavior for logged-in users.

The issue at hand describes that there’s an app crash whenever a non-logged-in user tries to access the author’s achievements. When this happens the application closes and an error pops up on screen showing that an error has occurred.

## Solution

The first step was searching where the error originated from. Seeing that the problem was somewhere inside the media file’s detail. I searched inside the codebase for a place where the media details view was rendered. After a thorough search I ended up finding that the fragment that showed this view was bound to the `MediaDetailFragment` that creates the view that displays all the displays about a specific media file. 

The method that is in charge of rendering the author’s achievements is inside this `MediaDetailFragment` file. This fragment is the root fragment for the details of a specific media file. Here the user can see the description of the file, its author, etc. There’s a method called `onAuthorViewClicked` that serves as a callback function whenever the user accesses the author’s username on the details of a media file.

```java
@OnClick(R.id.mediaDetailAuthor)
public void onAuthorViewClicked() {
    if (media == null || media.getUser() == null) {
        return;
    }
    ProfileActivity.startYourself(getActivity(), media.getUser(), !Objects
        .equals(sessionManager.getUserName(), media.getUser()));
}
```

This method is binded to the `mediaDetailsAuthor` fragment, that represents the section where the username of a media file’s author is displayed. The method is binded through the `@onClicked` annotation, so whenever this section is “clicked” this method will be called. 

The cause of the crash in the application lies in that there exists a conditional for when this method is called inside the `MediaDetaiFragment`, so that the method will check if the username of the current logged-in user is equals to the media’s author. This is done by the next condition:

```java
ProfileActivity.startYourself(getActivity(), media.getUser(),
  !Objects.equals(sessionManager.getUserName(), media.getUser()));
```

This statement calls the method startYourself that is executed only when the media object is not `null` or when the author of the media object is also not `null`. The problem is that whenever there’s not a logged-in user found by the sessionManager object, the method `getUserName` returns `null` which cannot be compared to the string returned 

After asking for guidance of the expected result for this case, I received an answer by the development team where they arrived at the conclusion of opening a new browser window with the author’s profile page on Wikimedia Commons.

To do this a new condition needed to be added after checking if the media object or if the media’s author existed. In this condition we check if `sessionManager.getUsername` is equal to null, if it’s then it means there’s no user associated with the current session which means there’s no logged-in user. By doing this we force the program to not enter the last statement where the crash happens. 

Inside this block we can now write the code to execute whenever there’s not a logged-in user associated with the current session. 

First we have to create our URL that will be opened by the browser. This is done by assigning to the `userProfileLink` variable a string consisting of the constant declared in the app for the default URL (given by the `COMMONS_URL` constant in the `BuildConfig` object) concatenated with the string returned by the `media.getUser` method. By having a dynamic URL given by the declared URL we can have the correct URL declared in the build configuration.

```java
String userProfileLink = BuildConfig.COMMONS_URL + "/wiki/User:" + media.getUser();
```

After this we create a new BrowserIntent that opens the browser with the link created and assigned in the `userProfileLink` variable. After that it exits the function by returning so that the last statement is not executed.

```java
Intent browserIntent = new Intent(Intent.ACTION_VIEW, Uri.parse(userProfileLink));
startActivity(browserIntent);
return;
```

This solution is not a perfect one, because it depends on a user profile existing for a correct profile showing up. If this is not correct an empty profile shows up. This is only an issue when there’s a media file that has an author associated with another website, like But given the concluded solution by the project developers.
