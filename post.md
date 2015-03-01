## 1 Introduction

You’ve probably already heard by now about Android Wear, Watches, Moto360 and all this hype that is about to go over the roof in the next 6 months. Android Wear was and is designed to focus on timely information, delivered when it's most relevant.   In this article we will discuss Android Wear from design and philosophy perspectives through setting up your IDE to writing code and testing your code on real Android Wear devices or emulators.

## 2 Getting started with the Android Wear Design

Before we start writing code for Android wear, we should go over main design, guidelines and concepts.   At a high-level perspective , the Android Wear UI consists of two main core functions **Suggest** and **Demand**.

### 2.1 Suggest: The Context Stream

The context stream is a vertical list of cards,  each showing a useful or timely piece of information.  For easier reference,  let’s recap Google Now feature on Android phones/tablets. Users can swipe vertically for navigation. One card is displayed at a timely manner.  Photos are being used for additional visual information (usually background photos).  Same applies here, our application can create cards and inject them into the stream accordingly.  On a side note, Google Glass also incorporates the same Card stream metaphor, but uses the cards  stream as a long timeline for some sort of history for all events that happened.  

Cards in the stream can be swiped horizontally and reveal more pages  or buttons allowing the user to act upon notification. Cards are dismissed by left to right swiping, removing them until new notification  arrives from the same application with new information to display.  With this UI model Android Wear ensures a simple uncluttered stream of fresh  updated information.

### 2.2 Demand: The Cue Card

We might encounter use cases where Android Wear isn’t supposed to actively provide  the information through the context stream, so we need to ask or interact with the wearable device by saying **“OK Google”** or tapping the home screen. The cue card will open and swiping up shows a list of suggested voice commands, which can also be tapped. Each voice command activates a specific type of intent. 

We as developers should match our applications to some of these intents so that users can complete tasks using these voice commands. Multiple applications may register for the same single voice intent, while the user will have the opportunity to choose which application they prefer to use. Our Wear applications can respond to a voice command in the same way they can respond to a on the card in the stream. Voice interaction needs to be as direct as possible and a lot of it is simply in a form of a command, for example : **”set a timer for 10 minutes”**.

### 2.3 Design Principles for Android Wear

Following these design principles will help plan and assess our Android Wear app design.
1. **5 Seconds rule**

    Focusing on giving the user the ability to interact and perform his desired action in 5 seconds or less is a key design for Android wear.  Let’s think, why ?  While using a watch, for instance, we have a device that you use while doing something else, such as running, walking, eating or even talking with other people. If you use the watch and pause your conversation for 5 seconds each time you look at it, it affects your thoughts and eye contact and will make other participants feel neglected and unwilling to continue. This is why Google’s thumb rule for any Interaction with Android Wear is that you should follow the 5 seconds rule.

    _Simple Practice:_
     Think about a typical use case for your Wear app. Time it, If using it takes more than 5 seconds, you should think about making your app more focused.

2. **“I have a Big Thumb” rule**

    While Designing our app we need to design it for big gestures. This means try using as less touch targets as possible while making them large and making them more accessible.  Swiping through photos on a phone not in Grid mode uses a large area of the display and users don’t have to be precise while touching.  We should consider this as the best kind of interaction with a wearable device.  Think carefully about where the users can use the app.

    _Simple Practice:_
    Consider various situations, such as walking, talking to people, or ordering food. If you have to slow down/stop in order to touch/interact better, then we must create bigger gestures. 

3. **Cards flowing down the stream**

    Let’s say we want to allow users to grab a smoothie nearby. We would “appear” in the Stream of information on the wearable device after a  certain amount of time, suggesting the user one or more places to get that smoothie.  Appearing only when the user needs it can be tough to achieve but this is why we have  sensors or cloud computing.  Worst case scenario, user will have to speak or use a finger to get a smoothie.   

    _Simple Practice:_ 
    Try and list all possible situations where users will use your app.  Where will it be used? When?  Maybe time or place isn’t the trigger, maybe it’s just a specific event? Listing several situations means you can create a special flow for each situation and make sure triggers will apply if possible.

4. **“Faster than a speeding Bullet”**

    Remember we talked about the 5 seconds rule? Well, when you only have 5 seconds to act you have to do it fast. Doing something fast and well can be tricky sometimes, but nailing it with a solid and simple design flow will get the user happy and more willing to reuse the app again.

    _Simple Practice :_ 
    Go over your design and check if you  could split it up into separate cards.  If you can split a card design then in most cases you should. Don’t forget that you can use multiple pages if you need to.

5. **“More than meets the eye, the other way around”**

    Time is a luxury, not just in general, but particularly when dealing with Android Wear app. We want to design and build our app as a minimal flow of information for the user to look at while getting the job done. This is called designing for glancing. 

    _Simple Practice :_
    If you own an Android Wear device, put it on and try focusing on your knuckles while your watch is displaying your app. Does your design help you convey the message?  

6. **“Buzzing is the new oomph”**

    When your app runs on a phone, you want to gain/attract user’s attention with vibes/sounds in notifications/in app. When you have an Android Wear device, this means the user is wearing your app. Pay attention to intimacy and resist the urge to buzz your users on every move.

    _Simple Practice :_
    While making a phone call, ask someone to buzz your wrist or tap your shoulder. Can you continue your call? No, you will try and get more information from the tapper/buzzer and end up losing your focus in both tasks. If the information does not justify suspending a conversation, you should not make the notification interruptive.

*****

## 3 Setting up the environment

Let’s start by making sure that we have all that we need to get started.
Android studio is the recommended IDE.  Google States :  [Android studio](http://developer.android.com/sdk/installing/studio.html "Android studio") 
provides project setup, library inclusion, and packaging conveniences that aren't available in ADT.

**The rest of this article assumes you're using Android Studio. **

Android SDK Manager and appropriate packages : 

 1.   Android 4.4W API 20 package **required**. 
 2.   Android 4.4.2 API 19 package **recommended**.
 3.   Android SDK tools - latest version -  **required**.
 4.   Android SDK Build-tools - latest version -  **required**.


![alt text](//i.imgur.com/2BZcKa5.png "SDK Manager")

AVD(Android virtual device) for Android Wear :

Setting up an Android Wear emulator is quite the same as we were setting up Android emulators before. We just need a few changes for Device/Phone communication. 

 To set up an Android Wear virtual device:
* Open AVD Manager
* Click Create    

Now fill in the following details for the AVD and leave the with default values:
		* AVD Name - A name for your AVD		
		* Device - Android Wear Round or Square device types
		* Target - Android 4.4W - API Level 20
		* CPU/ABI - Android Wear ARM (armeabi-v7a)
		* Keyboard - Select Hardware keyboard present
		* Skin - AndroidWearRound or AndroidWearSquare depending on the selected device type
		* Snapshot - Not selected
		* Use Host GPU - Selected, to support custom activities for wearable notifications
		* Click OK.    

Sample Android Wear AVD:

![alt text](//i.imgur.com/o7OqXjH.png "AVD Example")

After we finished setting up the emulator we need to start it up for further configuration. This part is important and will allow our Android handheld to connect with the Android Wear emulator we just created.

Start the emulator:

*	Selecting the virtual device we just created.

*	Clicking Start and then clicking Launch.  Wait until the emulator shows the Wear home screen.

*  Pairing our handheld with the emulator:
	* On our handheld,we need to install the [Android Wear app](https://play.google.com/store/apps/details?id=com.google.android.wearable.app) from Google Play.

	* Connecting the handheld to your machine through USB and Forwarding the AVD's communication port to the connected handheld device

        `adb -d forward tcp:5601 tcp:5601 ` 

	**we must do this every time the handheld is connected**
	* Now we need to start the Android Wear app on your handheld device and connect to the emulator: 

		* Tapping the menu on the top right corner of the Android Wear  app to select “Demo Cards”.

		* The cards selected appear as notifications on the home screen of the emulator.
*****

## 4 App building blocks 

Android Wear is different from Ordinary Android apps. We got used to clicking on icons. Android Wear uses **cards**. Android Wear app adds a card to the stream of cards. This is done according to context and only at a relevant moment or by user's demand.

Building Android Wear app is done by using special building blocks. We can use one or more according to our needs.

*   **Contextual card in the stream:**
    *   **Bridged notifications -  **
          The card is usually being pushed to the wearable from the handheld that shows a standard Android notification. This is done automatically with almost no Android Wear code addition to existing apps. In fact, your app already use it if it uses notifications. You can add Wear-specific features like extra pages and voice replies by using the new notification APIs.

		**Contextual notifications -  **
The card appearance depends on events/triggers and is generated locally on the wearable.  Showing users information and functionality just when they need it. The easiest way to implement this is to use standard templates for Android notifications. We can also make our own layout from scratch with an activity inside a card. 

*   **Full screen UI app**

    *   **2D Picker **
       Google states this is a design pattern that is useful for showing options in a list. Using pre-built components can reduce development time.

       The design pattern is available as the _GridViewPager_ component.
    *   **Custom layouts**
        There are some things you can’t do on a card so...In comes custom layouts.  Custom layouts are used where apps need to extend the basic card in stream, such as presenting gauges, maps or graphs.

*******
Now we will start our Android Studio project setup. Yes, it’s time to code :)

## 5 Project Setup

We will start by opening our Android studio, which has optimized features for Android Wear Development.  For example, the Project Wizard which allows us to easily create 2 modules: 

1. **The Mobile**, Android handheld app. **You can set API 15 as minSDK**. Here i selected the best API version that suites my needs, There is a lot of debate on minSDK versions, but  you can set minSDK to lower API if you need/want to support older devices (these devices can’t use Android Wear for now) .
2. **The Wear App**, Android Wear Device module. **You need to set API 20 (KitKat Wear)**
*****

![alt text](//i.imgur.com/qmGckIv.png "New Project Wizard")


We will continue by creating blank activities to both our Mobile(Phone/Tablet app) module and our Android Wear module.

First we select blank activity from Mobile(Phone/Tablet app)


![alt text](//i.imgur.com/ZSbhlFe.png "New Project Wizard Mobile part")


Now we just name our Activity, layout and give it a title.

![alt text](//i.imgur.com/GTV90RC.png "New Project Wizard Mobile naming")

After naming it we choose the Blank Wear Activity for our Android Wear app/module:

![alt text](//i.imgur.com/QVwQ3nV.png "New Project Wizard Wear part")


And here we need to enter the appropriate information :

![alt text](//i.imgur.com/IjalfKk.png "New Project Wizard Wear naming")


**At the end of the setup, we’ll have a simple Project Structure in our Android Studio project.**
*****

We now have 2 modules:

**Mobile** : here we will place all the components of our Mobile Application
**Wear** : our Android Wear App

![alt text](//i.imgur.com/WpoEIOR.png "Project Wizard structure")


Now we can see we have a sample layout for our Android Wear app and also for our Mobile app. We will talk about Android Wear as Android layouts should be well known to you by now. 


    <?xml version="1.0" encoding="utf-8"?> 
    < android.support.wearable.view.WatchViewStub
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/watch_view_stub"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:rectLayout="@layout/rect_activity_buzz_move_wear"
        app:roundLayout="@layout/round_activity_buzz_move_wear"
        tools:context=".BuzzMoveWearActivity"
        tools:deviceIds="wear">
    </android.support.wearable.view.WatchViewStub>
    

** _WatchViewStub_** is a container that automatically inflates the right layout, based on the screen shape. You’re not forced to use it, so you can keep to declare layouts just as you usually do. Anyway, I think it would be good practice to distinguish different layouts for different shapes, at least for starters.
 
  How do we use it in our Activity?  
The wizard already created the code for us :


<!--code lang=Java linenums=true-->
    
    public class BuzzMoveWearActivity extends Activity {
     private TextView mTextView;
     @Override
     protected void onCreate(Bundle savedInstanceState) {
       super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_buzz_move_wear);
        final WatchViewStub stub = (WatchViewStub) findViewById(R.id.watch_view_stub);
        stub.setOnLayoutInflatedListener(new WatchViewStub.OnLayoutInflatedListener() {
            @Override
            public void onLayoutInflated(WatchViewStub stub) {
                mTextView = (TextView) stub.findViewById(R.id.text);
          }
       });
    }
    } 

 The **_WatchViewStub_** initializes like a normal view, then we need to set an **_OnLayoutInflatedListener_**. **_WatchViewStub_** will inflate our layout depends which screen shape we run at. **_OnLayoutInflatedListener_** interface allows us detecting when internal layout inflation has completed. We then get a reference to the TextView assuming we want to change the Text shown or do some text manipulation. If we need to perform a series of findViewById calls to locate inflated views we should do it here, in the method onLayoutInflated.

**********


So far we have a simple Android project that has a Wear module. Before we go into a less basic implementation, we need to cover the support libraries Android Wear has. The Project Wizard had imported the correct dependencies for us in the appropriate module's build.gradle file.

 These are optional dependencies and should be used only as noted: 

1. **Notifications**

    The Android v4 support library (or v13 - containing v4) contains APIs to extend existing notifications on handhelds to support wearables.
If we want notifications that appear only on the wearable, created when an app runs on Wear, we can just use the standard framework APIs (API Level 20) on the wearable and remove the support library dependency in the mobile module of our project. 

2. **Wearable Data Layer**

    We want to sync-send data between wearables and handhelds with the Wearable Data Layer APIs, and we must have the latest version of Google Play services. All data transfers are done via the Google Play services as a central, single 2 lanes highway. If we’re not using these APIs, we should remove the dependency from both modules.

3. **Wearable UI support library**

    Google noted this as an unofficial library that includes UI widgets designed for wearables.  These widgets are the best practices Google has at the moment but can and will change at any time. If the libraries are updated, our apps won't break since the libraries are compiled into our app.  Getting new features from an updated library is just a matter of statically linking the new version and updating our app accordingly. This library is only applicable if you create wearable apps and want to use the best practices Google provides at the moment.

********

## 6 Bundling our Android Wear applications

Wear devices do not have Google Play on them, so Wear apps should be coupled with apps installed on the handheld. The Wear app gets bundled into the phone / tablet APK and it will be automatically installed on the Wear device. Sometimes we built a standalone app that we want to put to use. Standalone meaning our app will only run on the Wear device and has no UI or real Interaction with the phone/Tablet we use. 

**What should we do then?** 

We will use a simple container APK that will encapsulate our Wear application and will get installed to the paired handheld (phone/tablet). This will give our Android Wear app a Parent APK and upon installation the Wear module will be automatically installed on to a paired Wear device.  The process is fully explained on the Android Developers [website](http://developer.android.com/training/wearables/apps/packaging.html)

 One thing i want to add is you must make sure permissions are being requested both on Wear module and also on our Parent APK. The Android Wear APK won’t get installed if it required permissions that were not being declared by its parent APK.

*********

## 7 Closing thoughts

We now have a functioning Android Wear sample application. We've opened a path to explore more on Android and Android Wear, and hopefully you learned a few new things.  We’ve covered Android Wear IDE and development environment setup, design principles and followed the path to our very own first Android Wear application.

**Should I use this in production?**

Sure, why not ?  all the tools and principles we learnt here should be your future’s developer equipment. 

**  Where do I go from here?**

There are quite a few resources available. 

The general go to place for information is the [Developer Android Wear](http://developer.android.com/wear/index.html).

 There is also the [Android Wear Developers community](https://plus.google.com/communities/113381227473021565406).

Finally, you should experiment with the code and see what else you can add to it and share what you have created with the world!