First, I find and talk to Dusty Giftwrap to get some information and context about the challenge. 

![Screenshot 2025-01-02 153409](https://github.com/user-attachments/assets/27643e79-b38a-4fac-8eb8-1048ae14338c)

This challenge is a browser based game where I must take down the opposing elves. When Dusty said client side, I thought first to tweak values using my browser's developer console or modifying the URL. But before I tried that, I wanted to see if I could win the game without any modification. After a few tried I win and get told it isn't "hacky" enough.

![Screenshot 2025-01-02 171517](https://github.com/user-attachments/assets/19c624aa-ae04-4e4e-9547-29ef078c1ea6)

Due to the message, I start to think about how I can modify client side values to gain an advantage in the game. Two ways of doing this that came to mind is modifying function parameters in the game's code or to tweak values in the URL. 

When I reload the game, I take a look at the URL: 
* ```https://hhc24-snowballshowdown.holidayhackchallenge.com/?&challenge=termSnowballShowdown&username=LaatDovahkiin&id=29e074eb-e5c3-4a74-ac97-4eed80b36b39&area=frontyardact2&location=30,33&tokens=termSnowballShowdown&dna=ATATATTAATATATATATATATATATATATATCGATCGGCATATATATATATATCGATATATATATATTACGATATCGTAATATATATATATATGCATATATATATATTATAATATATTA```

I don't see any meaningful values I can change. I close the game window and open it again. After experimenting with the different options to start the game, I noticed that there's a URL parameter I can change when I select option 2, create private room. 

![Screenshot 2025-01-02 172205](https://github.com/user-attachments/assets/343ea40c-9094-412f-8bf8-67953749012f)

The full URL is ```https://hhc24-snowballshowdown.holidayhackchallenge.com/game.html?username=LaatDovahkiin&roomId=66e248a6&roomType=private&id=f37cdfd8-dd34-4b3b-9e63-fefc2b0dee80&dna=ATATATTAATATATATATATATATATATATATCGATCGGCATATATATATATATCGATATATATATATTACGATATCGTAATATATATATATATGCATATATATATATTATAATATATTA&singlePlayer=false```. 

One value that I tried modiftying in the URL is ```singlePlayer```. I set the value to true and can play the game in single player mode. 

![Screenshot 2025-01-02 172332](https://github.com/user-attachments/assets/af1773c4-32a5-4924-a5bc-2c4e45357c3f)

Playing the game in single player is preferred, so I don't have to wait to join a match or create a private match. Next I think about how to modify the game code through the developer console. I open the developer console and look around in the code for function values I can modify. After looking the game files, the  ```phaser-snowball-game.s``` file has some function parameters that I can modify. 

![Screenshot 2025-01-02 175734](https://github.com/user-attachments/assets/2c98f463-b788-4d08-83da-5d1576772a42)

Some useful parameters that I can modify are below:

```javascript
this.snowBallBlastRadius = 24;
this.onlyMoveHorizontally = true;
this.throwSpeed = 1000;
this.throwRateOfFire = 1000;
```
