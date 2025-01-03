# Silver Trophy

After talking to Angel, Angel tells me that he needs help with the elf connect game. Angel describes how the game works, and two hints open up, one for the silver trophy and one for the gold trophy (the i icon in the left hand menu). 

![Screenshot 2024-12-24 074226](https://github.com/user-attachments/assets/2832e4b3-eda5-4d64-9969-678749774857)

After clicking on the terminal, I am presented with this interface. The goal of the game is to find groups of items that share something in common. 

![Screenshot 2024-12-24 074535](https://github.com/user-attachments/assets/ed325afd-c57d-431a-868e-b10d63e61bda)

Right away, I notice some names of Santa's reindeer names. The reindeer names are Dasher, Dancer, Prancer, Vixen, Comet, Cupid, Dunder, Blixem, and Rudolph. One hint I have seen repeated in the Discord server for this event is to look at the source code for the challenges. I do that by using the inspect element feature in my browser's development console and I find the below code.

```javascript
        const wordSets = {
            1: ["Tinsel", "Sleigh", "Belafonte", "Bag", "Comet", "Garland", "Jingle Bells", "Mittens", "Vixen", "Gifts", "Star", "Crosby", "White Christmas", "Prancer", "Lights", "Blitzen"],
            2: ["Nmap", "burp", "Frida", "OWASP Zap", "Metasploit", "netcat", "Cycript", "Nikto", "Cobalt Strike", "wfuzz", "Wireshark", "AppMon", "apktool", "HAVOC", "Nessus", "Empire"],
            3: ["AES", "WEP", "Symmetric", "WPA2", "Caesar", "RSA", "Asymmetric", "TKIP", "One-time Pad", "LEAP", "Blowfish", "hash", "hybrid", "Ottendorf", "3DES", "Scytale"],
            4: ["IGMP", "TLS", "Ethernet", "SSL", "HTTP", "IPX", "PPP", "IPSec", "FTP", "SSH", "IP", "IEEE 802.11", "ARP", "SMTP", "ICMP", "DNS"]
        };

        let wordBoxes = [];
        let selectedBoxes = [];
        let correctSets = [
            [0, 5, 10, 14], // Set 1
            [1, 3, 7, 9],   // Set 2
            [2, 6, 11, 12], // Set 3
            [4, 8, 13, 15]  // Set 4
```

Going by the source code above, ```correctSets``` defines the index positions of the right combinations for each wordset. Below are the challenge solutions for each set. I apply the index patterns for sets 1-4 for each ```wordSet``` item and remember that index numbering starts at 0, not 1. After creating the list of solutions for each set, I click them, complete the round and move onto the next one. 

Round 1 Solutions:
* Tinsel, Garland, Star, Lights
* Sleigh, Bag, Mittens, Gifts
* Belafonte, Jingle Bells, Crosby, White Christmas
* Comet, Vixen, Prancer, Blitzen

![Screenshot 2024-12-24 080748](https://github.com/user-attachments/assets/1d0e58c3-2af7-4aa3-9183-926e8c0a1176)

With Round 1 complete, I move onto Round 2. 

Round 2 Solutions:
* Nmap, netcat, Wireshark, Nessus
* burp, OWASP Zap, Nikto, wfuzz
* Frida, Cycript, AppMon, apktool
* Metasploit, Cobalt Strike, HAVOC, Empire

![Screenshot 2024-12-24 080936](https://github.com/user-attachments/assets/35279df9-99ab-4f40-b278-875f42623cbf)

With Round 2 complete, I move onto Round 3. 

Round 3 Solutions:
* AES, RSA, Blowfish, 3DES
* WEP, WPA2, TKIP, LEAP
* Symmetric, Asymmetric, hash, hybrid
* Caesar, One-time Pad, Ottendorf, Scytale

![Screenshot 2024-12-24 081252](https://github.com/user-attachments/assets/0a5f4d86-37fc-462b-b136-65f5df878235)

With Round 3 complete, I move onto Round 4, the final one. 

Round 4 Solutions:
* IGMP, IPX, IP, ICMP
* TLS, SSL, IPSec, SSH
* Ethernet, PPP, IEEE 802.11, ARP
* HTTP, FTP, SMTP, DNS

![Screenshot 2024-12-24 081409](https://github.com/user-attachments/assets/372d78f7-204a-4117-8a26-9e75cb885995)

After completing Round 4, I get the silver trophy for this challenge. 

# Gold Trophy

I am curious about the gold badge for this challenge, so I look at the requirements. It mentions a high score of 50,000 points. Seeing this, I think back to how I looked at the source code earlier in this challenge and how that helped me. So I look at the source code again. 

```javascript
let score = parseInt(sessionStorage.getItem('score') || '0'); // Initialize score
        let scoreText;  // Text object for score display
        let highScore = 50000;
```

I go the my browser's developer tools to modify the score value. 

![Screenshot 2024-12-24 082013](https://github.com/user-attachments/assets/bdf1b094-dfd9-4ca3-b64a-34c295a85cd9)

From here, I complete the one row and my score goes above 50000, giving me the gold trophy for this challenge. Now it is time to talk to Poinsettia and move onto the next challenge. 

![Screenshot 2024-12-24 082134](https://github.com/user-attachments/assets/fde73201-d7b9-4a92-a5c3-6f1dd354dea7)

Next Challenge: 
* [Elf Minder - Silver](https://github.com/Rockman-Blue/SANS_HHC_2024/blob/6ca19fe2cff31830b17ea9d187128d241716afc6/Prologue/Elf-Minder.md)
