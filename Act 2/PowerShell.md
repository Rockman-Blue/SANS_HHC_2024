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
* From the Invoke-WebRequest command above, in the Links section of the output, I see the many endpoints. The elipses indicates there are more endpoints than listed. 
![Screenshot 2025-01-02 081504](https://github.com/user-attachments/assets/7439168f-af90-405d-9c07-128e2e95e9e4)
* After looking through the command output, there are four endpoints with the following links:
1) http://localhost:1225/endpoints/1
2) http://localhost:1225/endpoints/2
3) http://localhost:1225/endpoints/3
4) http://localhost:1225/endpoints/4
* After looking at some documentation, I find out that the Invoke-WebRequest cmdlet supports the -OutFile parameter, where I can specify a location to store the files download with Invoke-WebRequest. Instead of using a loop, I just use a command for each endpoint since it's only four of them:

```Invoke-WebRequest -Uri http://localhost:1225/endpoints/1 -OutFile endpoint1```

```Invoke-WebRequest -Uri http://localhost:1225/endpoints/2 -OutFile endpoint2```

```Invoke-WebRequest -Uri http://localhost:1225/endpoints/3 -OutFile endpoint3```

```Invoke-WebRequest -Uri http://localhost:1225/endpoints/4 -OutFile endpoint4```

* Now, I have the content of each endpoint page. Like in question 2, I will use Get-Content in a pipeline with Measure-Object to see how many words each file has by running ```Get-Content ./<endpoint#> | Measure-Object -Word``` for each endpoint I've found so far.

![Screenshot 2025-01-02 084050](https://github.com/user-attachments/assets/729ca696-c7e6-4d0d-ae1d-f65a949a67a6)

* So far, none of the endpoints I have downloaded have 138 words. It's time to download the other endpoints with Invoke-WebRequest and count the words using Get-Content and Measure-Object. I do this for each endpoint until I find the one with 138 words. 

![Screenshot 2025-01-02 084310](https://github.com/user-attachments/assets/fd998cd1-43d3-460d-b88a-d2a868a129ee)

* Now I know that the endpoint 13 page has 138 words, I have to communicate with the URL and print the contents to the terminal. After searching for "invoke web request print contents" on Google, I find a stack overflow page that tells me how to use Invoke-WebRequest to display all content. To do this, I use a pipeline starting with Invoke-WebRequest, and pipe it to Select-Object. The -Expand Content command allows me to view all content returned by the Invoke-WebRequest command earlier in the pipeline. 

```Invoke-WebRequest -Uri http://localhost:1225/endpoints/13 | Select-Object -Expand Content```

7) There seems to be a csv file in the comments of that page. That could be valuable, read the contents of that csv-file!

![Screenshot 2025-01-02 085029](https://github.com/user-attachments/assets/dc3d79c8-e02d-40e0-94c2-33fe9692df01)

* Reading the output of the above command, I see where the CSV file is. Like for question 6, I can use the Invoke-WebRequest cmdlet in a pipeline with Select-Object to retrieve the content of the page. When I try doing that, I get an error. 

![Screenshot 2025-01-02 085640](https://github.com/user-attachments/assets/316180b3-4d20-48c8-a6f9-10058718bc94)

* Like in question 5, there are defensive measures in place. To bypass them, I use the credentials in question 5, admin/admin. After using Get-Credential with Invoke-WebRequest I can see the csv using the following commands. After typing the first command, I type admin for the username and password. The second command needs the -Credential argument to bypass the authorization requirement, and the -AllowUnencryptedAuthentication argument is needed to not get an error (like the same one I got in question 5). Finally, Select-Object is used in a pipeline to return all of the content on that page. 

```$cred = Get-Credential```

```Invoke-WebRequest -Uri "http://127.0.0.1:1225/token_overview.csv" -Credential $cred -AllowUnencryptedAuthentication | Select-Object -Expand Content```

8) Luckily the defense mechanisms were faulty! There seems to be one api-endpoint that still isn't redacted! Communicate with that endpoint!

* From the output of the csv file, there's two key pieces of information. First, there's a verification endpoint still active. That endpoint URL needs a SHA256 sum, which is present near the bottom of the output.

![Screenshot 2025-01-02 090335](https://github.com/user-attachments/assets/2f2369aa-bc40-4565-b105-ee8a5661b5d5)

* Going by the information in the output, the correct URL would be ```http://127.0.0.1:1225/tokens/4216B4FAF4391EE4D3E0EC53A372B2F24876ED5D124FE08E227F84D687A7E06C```. 

* I have to use that URI wit Invoke-WebRequest to communicate with the endpoint. I do that with the below command to answer the question.

```Invoke-WebRequest -Uri "http://127.0.0.1:1225/tokens/4216B4FAF4391EE4D3E0EC53A372B2F24876ED5D124FE08E227F84D687A7E06C" -Credential $cred -AllowUnencryptedAuthentication```

9) It looks like it requires a cookie token, set the cookie and try again.
    
* To set the cookie, I think to myself that there must be an argument to use with Invoke-WebRequest to set and store cookies. After looking at the Microsoft documentation for the cmdlet, I learn about the -WebSession argument, where the syntax is ```-WebSession <WebRequestSession>```. Before I use that argument in a Invoke-WebRequest command, I need to find out what to pass to the argument.
* I search to find how to get a session cookie with PowerShell, and I find out I have to use Microsoft.PowerShell.Commands.WebRequestSession. I find a Stack Overflow page that has an example. I try applying the commands used in that post to this challenge, but it doesn't work.
* I look to the Discord for some help, and someone mentioned using [this PowerShell script]((https://gist.github.com/lawrencegripper/6bee7de123bea1936359) to help them solve this question. After experimenting with it, I am run the following commands in succession. 

```powershell
$cred = Get-Credential
$session = New-Object Microsoft.PowerShell.Commands.WebRequestSession
$cookie = New-Object System.Net.Cookie
$cookie.Name = "token"
$cookie.Value = "5f8dd236f862f4507835b0e418907ffc"
$cookie.Domain = "127.0.0.1"
$session.Cookies.Add($cookie)
```

* After typing the first line, I input the credentials admin/admin. The second line above creates a new WebRequestSession to store the cookie. Lines 3-6 create the cookie. Line 6 adds the cookie to the current session.
* After this setup I had some trouble crafting the final command to communicate with the endpoint. After talking to someone in the Discord server to get a hint, I run the following command to complete this question.

```powershell
(Invoke-WebRequest -Uri http://127.0.0.1:1225/tokens/4216B4FAF4391EE4D3E0EC53A372B2F24876ED5D124FE08E227F84D687A7E06C -Headers $Headers -WebSession $session -Credential $cred -AllowUnencryptedAuthentication).content
```

10) Sweet we got a MFA token! We might be able to get access to the system. Validate that token at the endpoint!

* After experimenting with the script and adding the necessary values, I get this error. 

![Screenshot 2025-01-02 103404](https://github.com/user-attachments/assets/d6fe7c01-e30a-4d05-bc2b-719d45243630)

* I talked to someone in the Discord server who had the same issue. They said I have to automate the extraction of the MFA token. The reason I have to automate the extraction is because there are two cookies, and one of them changes. The two cookies are the one from question 9, but the other one (mfa token) changes. So I need to use a script to automate the extraction of the MFA token to account for it changing. 
