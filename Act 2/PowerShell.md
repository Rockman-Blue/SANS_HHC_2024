I talk to Piney, and I'm given the context of this challenge. 

![Screenshot 2025-01-02 072558](https://github.com/user-attachments/assets/b55fbf9c-5e3c-4a94-94f8-a98ad69dba41)

Piney is locked out of the system for the snowball weaponry. Time to use PowerShell so the elves can access their system. I go the terminal to start the challenge, and am told that I can type hintme for hints.

1) There is a file in the current directory called 'welcome.txt'. Read the contents of this file

```Get-Content ./welcome.txt```

* This question is relatively straightforward. The Get-Content cmdlet in PowerShell is analogous to the cat command in Linux. It outputs the content of an item/file in a specified location. In this case I pass the path of the file, which I'm told is in the current directory, so I use ./ before the filename.

2) Geez that sounds ominous, I'm sure we can get past the defense mechanisms. We should warm up our PowerShell skills. How many words are there in the file?

```Get-Content ./welcome.txt | Measure-Object -Word```

* This question needs a pipeline. I thought that the first part of the pipeline is the command used to complete the previous question, because to find the words the computer needs the file to parse the words through. After a little research I find out about the Measure-Object cmdlet, which among other things calculates the characters, words, and lines in text files. I learn that I can use arguments of -Character, -Word, or -Line depending on what I want to calculate in the file. Here, since the question is asking for words, the right option is the -Word argument with Measure-Object. The pipeline takes the output of the file (Get-Content) and feeds it into the input of Measure-Object.

3) There is a server listening for incoming connections on this machine, that must be the weapons terminal. What port is it listening on?

```netstat -a```

* The first cmdlet I tried running was ```Get-NetTCPConnection```, but this returned the following error. This cmdlet gets TCP connections.
![Screenshot 2025-01-02 073852](https://github.com/user-attachments/assets/9721fdcd-1679-4ebb-8e5d-0bf0e567049a)
* Netstat is a CLI tool that displays active network connections. The -a argument displays all active connections, as well as the TCP and UDP ports on which the computer is listening. 

4) You should enumerate that webserver. Communicate with the server using HTTP, what status code do you get?

```Invoke-WebRequest http://localhost:1225```

* From the previous question, I know that the server listening for incoming connections on this machine is localhost:1225. When the question says to communicate with the server using HTTP, I first thought of cURL. I try running ```curl http://localhost:1225```, but get the following error.
![Screenshot 2025-01-02 074830](https://github.com/user-attachments/assets/2f7fee5d-06d2-4df3-9975-be7111c68665)
* After typing ```hintme``` I'm told to use Invoke-WebRequest, which gets content from a web page on the internet. The first thing I try is just passing the server listening for incoming connections (localhost:1225). The command runs successfully, and I get a response code of ```401 (UNAUTHORIZED)```.

5) It looks like defensive measures are in place, it is protected by basic authentication. Try authenticating with a standard admin username and password.

```$cred = Get-Credential```

* I take a hint and try to create a pipeline using both the Get-Credential and Invoke-WebRequest cmdlets in one line with ```Get-Credential -credential admin | Invoke-WebRequest http://localhost:1225```. This did not work, so I tried thinking of other ways to combine the two cmdlets. I thought of using variables, so that's what I tried next. After typing ```$cred = Get-Credential```, I'm prompted to enter the username and password. I type in admin for both. Next I run the below command, and get an error.

```Invoke-WebRequest -Uri "http://localhost:1225" -Credential $cred```

![Screenshot 2025-01-02 080943](https://github.com/user-attachments/assets/be4f245f-acdb-46a8-932b-f96e3d2e86f7)
* After reading the error, I add the needed parameter. So the two commands required to complete this challenge are below.

```$cred = Get-Credential```
```Invoke-WebRequest -Uri "http://localhost:1225" -Credential $cred -AllowUnencryptedAuthentication```


6) There are too many endpoints here. Use a loop to download the contents of each page. What page has 138 words? When you find it, communicate with the URL and print the contents to the terminal.
* 
