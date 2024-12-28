I wander around the game world to talk to Chimney Scissorsticks. Chimney tells me that I'll be working with drone log files to find and decode hidden information. 

![Screenshot 2024-12-28 102612](https://github.com/user-attachments/assets/5d4ebc6c-d9b4-485f-8780-d6cbd224585c)

I access the challenge terminal and download the only available file, fritjolf-Path.kml. KML files can be used with Google Earth. I open Google Earth and open the file.

![Screenshot 2024-12-28 103344](https://github.com/user-attachments/assets/538adb9d-a751-4add-a404-1e4be52ecd09)

Between this image and the filename, I need to find the login information to access the terminal login page. 

![Screenshot 2024-12-28 103549](https://github.com/user-attachments/assets/fdd9fb4d-4e19-47ad-9cb6-63dc659df9dd)

From the filename and the drone path in the file I have two key pieces of information:
* fritjolf
* GUMDROP1

I test both combinations of these at the login page and get in with fritjolf/GUMDROP1. I can search for a drone name to get drone details. 

![Screenshot 2024-12-28 103712](https://github.com/user-attachments/assets/f0bbc761-458b-4fc8-a299-78f2e8f843b8)

However, I don't have any drone names. So I start thinking about finding vulnerabilities on this page that can disclose information, like testing for SQL injection, command injection, cross site scripting, etc. After some testing, I input `' or '1'='1` to display available drone details. The revealed drone names are:
* ELF-HAWK
* Pigeon-Lookalike-v4
* FlyingZoomer
* Zapper

In the comments for ELF-HAWK, the page tells me where to find the activation code. I download the csv file. 

![Screenshot 2024-12-28 104723](https://github.com/user-attachments/assets/63ab65d2-53fb-4b99-ac3f-a6b7014eada9)

