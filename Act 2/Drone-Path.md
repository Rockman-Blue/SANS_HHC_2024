# Silver Trophy

I wander around the game world to talk to Chimney Scissorsticks. Chimney tells me that I'll be working with drone log files to find and decode hidden information. 

![Screenshot 2024-12-28 102612](https://github.com/user-attachments/assets/5d4ebc6c-d9b4-485f-8780-d6cbd224585c)

I access the challenge terminal and download the only available file, ```fritjolf-Path.kml```. KML files can be used with Google Earth. I open Google Earth and open the file.

![Screenshot 2024-12-28 103344](https://github.com/user-attachments/assets/538adb9d-a751-4add-a404-1e4be52ecd09)

Between this image and the filename, I need to find the login information to access the terminal login page. 

![Screenshot 2024-12-28 103549](https://github.com/user-attachments/assets/fdd9fb4d-4e19-47ad-9cb6-63dc659df9dd)

From the filename and the drone path in the file I have two key pieces of information:
* fritjolf
* GUMDROP1

I test both combinations of these at the login page and get in with fritjolf/GUMDROP1. I can search for a drone name to get drone details. 

![Screenshot 2024-12-28 103712](https://github.com/user-attachments/assets/f0bbc761-458b-4fc8-a299-78f2e8f843b8)

However, I don't have any drone names. So I start thinking about finding vulnerabilities on this page that can disclose information, like testing for SQL injection, command injection, cross site scripting, etc. After some testing, I input `' or '1'='1` to display available drone details via an SQL injection attack. 

![Screenshot 2024-12-28 104723](https://github.com/user-attachments/assets/63ab65d2-53fb-4b99-ac3f-a6b7014eada9)

The revealed drone names are:
* ELF-HAWK
* Pigeon-Lookalike-v4
* FlyingZoomer
* Zapper

In the comments for ELF-HAWK, the page tells me where to find the activation code. I download the CSV file. 

![Screenshot 2024-12-28 105022](https://github.com/user-attachments/assets/83f91552-fec4-4da8-a4cc-763f82253cae)

I go to the profile page to look for more information, and find another CSV file. 

![Screenshot 2024-12-28 105421](https://github.com/user-attachments/assets/e7f24e6f-b32e-4d15-b030-4442676968c2)

I first look at the ```ELF-HAWK-dump.csv``` file, since the comments for ELF-HAWK mention where to find the activation code. As you can see, the file is very messy and has way too much data to sift through by hand. 

![Screenshot 2024-12-28 105839](https://github.com/user-attachments/assets/11f28948-322b-4dfc-a7c0-5e46758c1526)

After trying to filter the data within Google Sheets and other means I got stuck. I asked in the Discord for a hint, and someone mentioned they had used the [QGIS software](https://www.qgis.org/) and that they converted the CSV file to KML. First I used a CSV to KML converter to convert ```ELF-HAWK-dump.csv``` to ```ELF-HAWK-dump.kml```. Then, I download the QGIS software and import the ```ELF-HAWK-dump.kml``` file into it. This took some messing around with the menus, since I'm unfamiliar with the software. 

After I did that, I got the image below. So the activation code is ```DroneDataAnalystExpertMedal```.

![Screenshot 2024-12-28 113243](https://github.com/user-attachments/assets/8c4c6a2a-dc60-4949-9432-972c8896c086)

I go back to the challenge window and input the activation code to get the silver trophy for this challenge. 

![Screenshot 2024-12-28 113354](https://github.com/user-attachments/assets/5d0cf227-da30-4bb0-aa7a-ccfaaae588cb)
