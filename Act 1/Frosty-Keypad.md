# Silver Trophy

![Screenshot 2024-12-25 131909](https://github.com/user-attachments/assets/2de9ca2b-776c-4e39-9983-2d6ed9c532fe)

After exploring the Act 1 island for a little bit, I talk to Morcel to learn more about the Frosty Keypad challenge. After talking to Morcel, I get three hints, which I read by clicking on the green "i" icon on the left hand side of the GUI. The hints are:
* See if you can find a copy of that book everyone seems to be reading these days. I thought I saw somebody drop one close by...
* Well this is puzzling. I wonder if Santa has a seperate code. Bet that would cast some light on the problem. I know this is a stretch...but...what if you had one of those fancy UV lights to look at the fingerprints on the keypad? That might at least limit the possible digits being used...
* Hmmmm. I know I have seen Santa and the other elves use this keypad. I wonder what it contains. I bet whatever is in there is a National Treasure!

I wander around the game world to look for a copy of the book. I find the book nearby, it's placed behind that last crate all the way at the right of the above screenshot. I can read its contents at https://frost-y-book.com/. I read that and then go to the challenge terminal to learn more about the challenge.

![Screenshot 2024-12-25 133048](https://github.com/user-attachments/assets/50ed3efa-ff74-4239-90f8-ac73f5cc7af9)

This challenge involves finding pins to successfully access this machine. One of the hints mentions using a UV light. After some guessing, I look at the game's source code using my browser's developer tools. That wasn't successful for me, and after talking to someone in the Discord server for the event, they tell me to use the sticky note in the top left of the page.

![Screenshot 2024-12-26 072615](https://github.com/user-attachments/assets/47a30786-43dc-48d9-9b41-bdfe6bb41772)

I figure out that each of these number sets correlate to the same format of ```page#:word#:character#```. After going through the hint for each of the five number sets, the numbers correlate to ```SANTA```, or ```72682```. After putting in this PIN and hitting enter, I get the silver trophy for this challenge.

![Screenshot 2024-12-26 072858](https://github.com/user-attachments/assets/0f57ad38-3e3a-4aa4-8087-89a7527c92ee)

Next Challenge:
* [Curling - Silver and Gold](https://github.com/Rockman-Blue/SANS_HHC_2024/blob/a8a920e4ff7106041084d52cfadcc38fa654accb/Act%201/Curling.md)
