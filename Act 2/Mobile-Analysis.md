I go to the Act 2 island in the event's story menu. From there I get a bunch of objectives added to my menu. To start this challenge, I must talk to Eve Snowshoes for more information.

![Screenshot 2024-12-28 094534](https://github.com/user-attachments/assets/9a1cdc10-e7af-4c3b-8c62-ce1f72defc2b)

![Screenshot 2024-12-28 094552](https://github.com/user-attachments/assets/d997ef6c-beed-45a3-8507-6074e7b01da7)

Here's the challenge. Eve built an Android app to test a modern solution to Santa's naughty and nice list. There's two versions of this app, a debug and release version. Eve accidentally left out one child's name on each version, but Eve can't remember who.

My goal is to download both versions of the app as .apk files and look for the missing child's name on both versions. Eve suggests starting with the debug version first to find out which child's name isn't shown in the list in the app. After that I can move onto doing the same for the release version. 

The hint suggests using either of these two tools:
* [apktool](https://github.com/iBotPeaches/Apktool/releases)
* [jadx](https://github.com/skylot/jadx)

I download the jadx tool and open the SantaSwipe.apk file (debug version of app). There are a lot of files to comb through. After spending some time looking through the various files and folders, I got to Discord to get a hint. There, someone tells me to look at the com.northpole.santaswipe.MainActivity file under the com/northpole.santaswipe directory. I look around in the file and find the following code. 

```java
Cursor cursor = sQLiteDatabase.rawQuery("SELECT Item FROM NormalList WHERE Item NOT LIKE '%Ellie%'", null);
```

Ellie is the missing name for the debug version of the app. I go to my objectives page in my menu to submit the missing name and get the silver trophy for this challenge. 

![Screenshot 2024-12-28 100635](https://github.com/user-attachments/assets/b3b0ae24-4d96-4fc9-88d0-aee17df9d2b5)
