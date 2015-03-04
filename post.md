I’m not a coder
-----------
I’m not a coder. Not really. Well, I am compared to some people but I’m not a professional. Even amateur is kind. Perhaps… beginner? Okay, I’ve been coding since the ZX81 but I never got good, I never became an expert despite my years of experience, mostly with Basic and then JavaScript.

Even so, for the past couple of years I’ve been making apps and have published 5, yes five, with my limited knowledge. They’ve all been Android and iOS and this is all thanks to hybrid apps and, if we’re really being serious, Cordova/PhoneGap.

I started making apps by hand-coding HTML, CSS and JS and using PhoneGap Build to deploy them to Android and iOS.

I just want to make a note here about platforms. I build for Android and iOS and not Windows Mobile only because when I started the information about the requirements was anything but clear. It was so frustrating trying to find out what I needed and so I just gave up. I believe this affected other people and it was just bad strategy by MicroSoft.

My first attempts worked but they weren’t perfect. My code was okay but the phones didn’t want to play nice with my hand scripted tab menus that had their widths set at 33, 33 and 34% in CSS. Nothing was really respsonsive and I’m not a designer. I found jQuery and thought I was onto something big. jQuery, JavaScript, HTML, CSS — yes, these were made for each other!


jQuery Mobile 
--------------
This was the game changer. No longer was I restricted by my own HTML5, now I was restricted by a set of controls I could use out of the box. It worked and my first 4 apps are built with this (plus some custom code of course, and a bit of JSON and so on). They aren’t the prettiest but they work and they work well.

jQM is really heavy though and I started looking at some other frameworks, like Zepto, Foundation and even Twitter Bootstrap.

And then I came upon Ionic.

Ionic apps are built with Cordova and therefore you can, theoretically, build for iOS, Android, Window Mobile, BlackBerry and more, just like with PhoneGap Build.


Ionic and Angular 
------------------
Angular is baffling. It’s powerful, useful, cool, takes away a lot of headaches and generates a whole new set. It really depends what you want to do with Ionic tbh. If you want a really simple nice interface you’ll get it and you don’t really need to know what you are doing; the out of the box components look and work really nicely.

But if you want to do anything more than the most basic app you have to get your head around how it works and how it works is Angular. And Angular is baffling. It’s baffling because its so powerful. I think. I don’t get all of it (why is $scope sometimes not defined?). I’m too eager to make stuff and I’ve managed to make an Ionic app already and though it’s number 5 on my list it’s still in beta (on Android) and not anything on iOS.

Which is where I come to the sticking point.


Working with Ionic 
----------------
Ionic is the next big thing. In fact it might be the the now big thing, in hybrid app building anyway. The Ionic team have done an amazing job because it’s not just the core Ionic directives (Ionic is Angular) they’ve build, it’s the tools and the community.

Here’s a run down of what you get.

* A set of command line tools for setting up, testing and building your app. These make things so easy. Get over the fear of the command line — I did.

* A cross-platform (iOS and now Android) app that you can deploy your app to for testing — Ionic View. Anyone can get this app and if they have the code for your app they can test it. Amazing. It’s not compatible with all of the plugins yet so you have to do your final testing on device, as it should be.

* A set of pre-build, but customisable, components for building your apps UI; tabs, swipe cards, forms, buttons, and much much more.

* Instructions on the Ionic site on how to use all this stuff.

* A forum for help. This isn’t as fruitful as using stackoverflow but… well, stackoverflow. And as Ionic is Angular and Angular is JavaScript and JavaScript is by far the most popular language on stackoverflow you’re not going to have a bad time if you post questions there either.

This stuff is all great and you can make a simple but good looking app. The front end stuff is largely all there but if you want your app to do anything that involves the device, like geolocation or using the camera you’re going to have to use plugins.


Plugins in Ionic 
----------------

The plugins for Ionic are actually all Cordova plugins. This means you can get them from cordova.io. These all work with any Cordova project and there is pretty good documentation. Most of these plugins now seem to also play nicely with PhoneGap Build, which certainly wasn’t the case when I was using it.

The other option is the ngCordova plugin repository. These are all the Cordova plugins that play nicely with ngCordova — an Angular wrapper for the plugins. In truth I don’t get why you’d need the ngCordova versions, and there are less of them, but the way you use the plugins (as in the way the JavaScript is written) makes them a little bit easier for an amateur like me to use them.

So you got your UI, you got your plugins, you’ve written a bunch of Angular or jQuery or JavaScript (though you really should just be using Angular) and your test versions all work when you test them in Ionic View.

And then you’ll need to deploy it.


Deploying Ionic apps 
----------------
For someone only who a. doesn’t usually use the command line and b. despite having a Mac and publishing 4 iOS apps in the past hadn’t ever used XCode before this was, and is, a mission.

I should clarify — my new Ionic app is out in beta for Android and I finally deployed the iOS development version to an iPhone yesterday. I started writing this before that so earlier on in this peice you’ll see I said it was nothing on iOS yet (although I’d tested it on Ionic View).

PhoneGap Build 
----------------
In PhoneGap Build you do this:

* Sync your app with GitHub

* Pull the app into PGB from GitHub

* Upload your Android and iOS keys as per the PGB documentation for iOS and for Android. I actually didn’t use this method for Android — I got my key using this tutorial. Remember — you will need different keys for iOS Development builds, which you test on your devices and your friends devices by adding their UDIDs to the permissions list in your iOS developer account.

* Download your .apk and .ipa and then upload them to the respective stores. The Android developer portal is web based but you need to use Application Loader to upload to iTunes.

If you’re using Ionic from the command line (and you can use it with PhoneGap Build if you want I understand) you’ll need to build your apps in a different way.

Android 
----------------
The command line command to build an unsigned .apk is this:

`$ ionic build --release android`

This puts the .apk in platform/android/ant-build so navigate to it.

You still need to sign the .apk from the command line like this:

`$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore YourKeystore.keystore YourApp-release-unsigned.apk alias_name`

“YourKeystore.keystore” will be the keystore you generated. You’ll have to enter your keystore password and “alias_name” will be the keystore alias.

“YourApp” will be the name of your application.

After signing you’ll have to optimise your .apk with the zipalign tool, like this:

`$ zipalign -v 4 YourApp-release-unsigned.apk YourApp.apk`

Now you may have an issues here, with the path to zipalign. Even though it’s somewhere on your computer you might need to search for it and run it like this:

`$ /Users/MyUsername/Development/adt-bundle-mac/sdk/build-tools/android-4.4W/zipalign -v 4 YourApp-release-unsigned.apk YourApp.apk`

If this all worked out you’ll have YourApp.apk signed and ready for upload to the Google Play Store.

Phew!

iOS 
----
You do this with XCode. I’ve only used XCode 6 so any other versions may well be different.

Start by navigating to platforms/ios/YourApp.xcodeproj in you Ionic application folder. Double clicking the .xcodeproj file will open the application in XCode.

Remember, if you make any changes in your code at this point it won’t update to the .xcodeproj as this isn’t a live reload environment. You’ll have to use this command to refresh things, and I recommend closing and restarting XCode:

`ionic prepare ios`

Okay. Now you’ve got your final code into XCode.

In XCode go to Project->Archive. If Archive is greyed out then click on your project name, right at the top of the window, and make sure iOS Device is selected and not one of the emulators. Now go to Archive. If you get a Build Failed error go to Project>Clean and try again. Even if this doesn’t fix your project it will likely tell you what you need to fix.

There are a few issues you may have:

1\. You get a clang error like this:

`clang: error: no such file or directory: '/Users/myUserName/myApp/platforms/ios/CardsApp/Plugins/de.appplant.cordova.plugin.email-composer/APPEmailComposer.m'
clang: error: no input files
Command /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang failed with exit code 1`

Lo and behold, that folder wasn’t there so XCode wasn’t lying or being awkward! To fix this I removed the iOS platform from Ionic and then re-added it.

`ionic platfrom remove ios`

`ionic platform add ios`  



2\. You get a chown error like this:

`Command /usr/sbin/chown failed with exit code 1`

Fixing this just required a restart again. I removed and added the iOS platform again to be sure.

Okay, ready to get the .ipa now. Project>Archive.

Once the Archive operation is successful press Window->Organiser. You’ll get a new window with Project and Archives tabs. Click Archives and you’ll see your ready to use .ipa file. From here you can upload it to iTunes or get a development version for yourself. The menus should be pretty self explanatory.

Phew! Again!


The Final Hurdle-ish 
--------
There is one last issue you may encounter.

Upon submission to iTunes Connect you’ll likely get an email saying this:

>Dear developer,

>We have discovered one or more issues with your recent delivery for “YourApp”. Your delivery was successful, but you may wish to correct the following issues 
in your next delivery:  

>Missing Push Notification Entitlement — Your app appears to include API used to register with the Apple Push Notification service, but the app signature’s 
entitlements do not include the “aps-environment” entitlement. If your app uses 
the Apple Push Notification service, make sure your App ID is enabled for Push Notification in the Provisioning Portal, and resubmit after signing your app with a Distribution provisioning profile that includes the “aps-environment” 
entitlement. See “Provisioning and Development” in the Local and Push Notification Programming Guide for more information. If your app does not use the Apple Push Notification service, no action is required. You may remove the API from future submissions to stop this warning. If you use a third-party framework, you may need to contact the developer for information on removing the API.  

>After you’ve corrected the issues, you can use Xcode or Application Loader to upload a new binary to iTunes Connect.  

>Regards,  

>The App Store team  


This appears to be a Cordova issue. I think I started getting this message in late 2013 or 2014. It’s been a much discussed issues on stackoverflow and the PhoneGap Build forums. The thing about it is — it doesn’t seem to affect the Apple app review process and so far hasn’t been reported as a reason for rejection.

However you may wish to consider that

* There is no guarantee that Apple won’t suddenly say “Nope. All apps with this issue get insta-rejected.” in the future. Including retroactive rejections! It could happen.

* Many coders are pretty fussy and would rather have everything nice and clean.

With that in mind, here is one potential solution.

In XCode, go to the top left and open the project files (it’s the folder icon on the far right, not in the toolbar but in the lefthand panel). Navigate to Classes and then AppDeligate.m

In AppDeligate.m find and comment out this code:

`— (void) application☹UIApplication*)application
didRegisterForRemoteNotificationsWithDeviceToken☹NSData*)deviceToken
{
// re-post ( broadcast )
NSString* token = [[[[deviceToken description]
stringByReplacingOccurrencesOfString:@”<” withString:@””]
stringByReplacingOccurrencesOfString:@”>” withString:@””]
stringByReplacingOccurrencesOfString:@” “ withString:@””];
[[NSNotificationCenter defaultCenter] postNotificationName:CDVRemoteNotification object:token];
}
'- (void) application☹UIApplication*)application
didFailToRegisterForRemoteNotificationsWithError☹NSError*)error
{
// re-post ( broadcast )
[[NSNotificationCenter defaultCenter] postNotificationName:CDVRemoteNotificationError object:error];
}`

How do you comment out this code? With your standard

`/* code between these things */`

Now when you submit your app you won’t get that email. Hopefully this will future-proof your app. We’ll have to see what happens with it though as Apple are little unpredictable like that.


Ready? 
-------
You should be ready to go now. It’s a mission alright, and it’s fraught with problems some of which I’ve tried to address. The result should be a working app though and once you’ve tried Ionic you’ll never go back to jQM or hand-coding. It’s still in beta (though v1 will be released soon) but is still perfectly usable. I don’t think native apps will ever die out because there are too many people with the skills and knowledge for them. Hybid apps will grow though; it’s reusable tech that many, many people already use for websites and web apps.

Get into Ionic.

***
*This content originated on my Medium account, [here](https://medium.com/@sub_effect/adventures-in-apps-hybrids-for-the-amateur-6ef83cff335a "Medium").*


