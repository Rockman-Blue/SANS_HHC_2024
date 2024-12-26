I talk to Jewel to get some of the story context behind this challenge, and Jewel gives me a hint. In addition to the hint that shows up for this challenge that I can access by clicking the green "i" icon in the left pane of the GUI, Jewel says I should talk to Morcel Nougat. 

![Screenshot 2024-12-26 073230](https://github.com/user-attachments/assets/57e135e6-14dd-4333-8f3d-20070890ed80)

I talk to Morcel, and Morcel tells me there's a sample Python script for a heuristic detection technique [here.](https://gist.github.com/arnydo/5dc85343eca9b8eb98a0f157b9d4d719) 

Morcel mentioned shredded paper in my initial conversation with him. I check my items and find the image of the paper [here.](https://holidayhackchallenge.com/2024/shreds.zip) After downloading and unzipping the file, I notice it's just many images about one pixel wide, emulating pieces of shredded paper. 

The Python script above can help me put together the image I need to help with this challenge. I download the script and run it with the images downloaded from the ZIP file to get the image below.

![Screenshot 2024-12-26 075722](https://github.com/user-attachments/assets/1e6462ab-96c6-45c7-9960-d57b16066428)

Next, I use ChatGPT to fix the image by mirroring it. I get the below image. 

![Screenshot 2024-12-26 081028](https://github.com/user-attachments/assets/a4776579-3d75-46f0-91a0-fb2737a443a6)

This gives me the following information:
* Baud - 115200
* Parity - Even
* Data - 7 Bits
* Stopbits - 1 bit
* Flow Control - RTS

However, before I select those settings on the device itself, I have to make sure the wires and cables are connected properly. I'm not too familiar with hardware, so I ask in the Discord server for some help and am able to connect the wires.

![Screenshot 2024-12-26 081726](https://github.com/user-attachments/assets/aaee8262-3eaa-4526-b618-67d4515846c6)

I click Zoom In on the device and use the in game controls to configure the options to be the same as the reconstructed image and click start. When I clicked start, I got smoke, which indicated a voltage issue. 

![Screenshot 2024-12-26 082115](https://github.com/user-attachments/assets/e3effdc7-fae7-4d9c-8b52-be62d9f5aad0)

I look at the manual and it tells me that I can change the voltage on the UART-Bridge device between 3V or 5V. I change it to 3V and hit start again. This allows me to complete the first part of this challenge, and the game tells me to talk to Jewel to proceed further. 

![Screenshot 2024-12-26 082340](https://github.com/user-attachments/assets/85f62064-a9be-47ad-a921-33bac19e3c23)

I talk to Jewel and Jewel tells me that Santa is missing, and that the only way to track him is to access the Wish List in his chest. I must modify the access_cards database to get entry by granting access to card number 42. Jewel tells me that I must use the slh application which is the key to get into the access database. That slh tool is password protected, so I have to find it before granting access to card number 42. 

I get two hints for this part of the challenge. One of them mentions that passwords can get added to log files and other easy to access locations, and that in these cases you can step back in history and identify the password. The second hint mentions there being a HMAC generator included in [CyberChef.](https://gchq.github.io/CyberChef/#recipe=HMAC(%7B'option':'UTF8','string':''%7D,'SHA256'))



