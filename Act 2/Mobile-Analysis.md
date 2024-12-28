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

Next I open the SantaSwipeSecure.aab file (release version of app) in jadx. My first instict is to go to the com/northpole.santaswipe directory, since that was the directory that contained the file with the answer for the debug version of the app. Like the previous part of this challenge, the answer is in a DatabaseHelper class. I find the following line, but it is encrypted. 

```java
db.execSQL(decryptData("IVrt+9Zct4oUePZeQqFwyhBix8cSCIxtsa+lJZkMNpNFBgoHeJlwp73l2oyEh1Y6AfqnfH7gcU9Yfov6u70cUA2/OwcxVt7Ubdn0UD2kImNsclEQ9M8PpnevBX3mXlW2QnH8+Q+SC7JaMUc9CIvxB2HYQG2JujQf6skpVaPAKGxfLqDj+2UyTAVLoeUlQjc18swZVtTQO7Zwe6sTCYlrw7GpFXCAuI6Ex29gfeVIeB7pK7M4kZGy3OIaFxfTdevCoTMwkoPvJuRupA6ybp36vmLLMXaAWsrDHRUbKfE6UKvGoC9d5vqmKeIO9elASuagxjBJ"));
```

After looking around in the same DataBase class I find the following code. This code reveals where the strings are being loaded from.

```java
    public DatabaseHelper(Context context) {
        super(context, DATABASE_NAME, (SQLiteDatabase.CursorFactory) null, R.xml.data_extraction_rules);
        Intrinsics.checkNotNullParameter(context, "context");
        String string = context.getString(R.string.ek);
        Intrinsics.checkNotNullExpressionValue(string, "getString(...)");
        String obj = StringsKt.trim((CharSequence) string).toString();
        String string2 = context.getString(R.string.iv);
        Intrinsics.checkNotNullExpressionValue(string2, "getString(...)");
        String obj2 = StringsKt.trim((CharSequence) string2).toString();
        byte[] decode = Base64.decode(obj, R.xml.backup_rules);
        Intrinsics.checkNotNullExpressionValue(decode, "decode(...)");
        this.encryptionKey = decode;
        byte[] decode2 = Base64.decode(obj2, R.xml.backup_rules);
        Intrinsics.checkNotNullExpressionValue(decode2, "decode(...)");
        this.iv = decode2;
        this.secretKeySpec = new SecretKeySpec(decode, "AES");
    }
```
