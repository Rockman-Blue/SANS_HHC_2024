After talking to Angel, Angel tells me that he needs help with the elf connect game. Angel describes how the game works, and two hints open up, one for the easier and harder version of the challenge in the left hand menu (i icon). 

![Screenshot 2024-12-24 074226](https://github.com/user-attachments/assets/2832e4b3-eda5-4d64-9969-678749774857)

After clicking on the terminal, I am presented with this interface. The goal of the game is to find groups of items that share something in common. 

![Screenshot 2024-12-24 074535](https://github.com/user-attachments/assets/ed325afd-c57d-431a-868e-b10d63e61bda)

Right away, I notice some names of Santa's reindeer names. The reindeer names are Dasher, Dancer, Prancer, Vixen, Comet, Cupid, Dunder, Blixem, and Rudolph. One hint I have seen repeated in the Discord server for this event is to look at the source code for the challenges for hints. This is done by using the inspect element feature in my browser's development console. I do that and find the below code.

```
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

Going by the source code above, below are the challenge solutions for each set. I remember that the index numbering starts at 0, not 1. 
* Set 1 - Tinsel, Garland, Star, Lights
* Set 2 - burp, OWASP Zap, Nikto, wfuzz
* Set 3 - Symmetric, Asymmetric, hash, hybrid
* Set 4 - HTTP, FTP, SMTP, DNS
