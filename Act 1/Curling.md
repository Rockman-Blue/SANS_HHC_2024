# Silver Trophy

After clicking on "Go to Act I" in the story section of the game menu, I go left to talk to Bow Ninecandle to learn more about the cURLing challenge. 

![Screenshot 2024-12-24 101046](https://github.com/user-attachments/assets/3859ef6b-a885-4a26-9931-0e3a668b10b9)

Bow explains the basic concept of curl, a tool that transfers data to and from a server using URLs. I get two hints after talking to Bow:
*  Using the cURL man page at https://curl.se/docs/manpage.html
*  To use cURL's "--path-as-is" option. This controls a default behavior. 

By clicking on the curling setup, I access and interact with the challenge via a terminal. After typing y and hitting enter to start the challenge, I am presented with the first question. I am told that I can run "hint" to get a hint if I am stuck on a specific question.

![Screenshot 2024-12-24 101527](https://github.com/user-attachments/assets/be8dd99e-2cfd-41de-a21a-0f707c0362d0)

Below are the questions, solutions, and explanations:

1. Unlike the defined standards of a curling sheet, embedded devices often have web servers on non-standard ports. Use curl to retrieve the web page on host "curlingfun" port 8080.
* ```bash
* curl http://curlingfun:8080```
* This first question is pretty straightforward. You can retrieve a webpage on a specific host by specifying the port after a :, the generic format in this case would be curl hostname:port_number.

2. Embedded devices often use self-signed certificates, where your browser will not trust the certificate presented.  Use curl to retrieve the TLS-protected web page at https://curlingfun:9090/

```curl -k https://curlingfun:9090/```
* This second question was a bit harder. Initially, I tried the command above without the -k argument. When I ran that, I got the error below:
'''curl: (60) SSL certificate problem: self-signed certificate'''
* In the same error message, there was a link to a cURL documentation page at https://curl.se/docs/sslcerts.html. I read the documentation and saw an option to skip certificate verification with the -k/--insecure flag. I then used that argument to find the right command.

3. Working with APIs and embedded devices often requires making HTTP POST requests. Use curl to send a request to https://curlingfun:9090/ with the parameter "skip" set to the value "alabaster", declaring Alabaster as the team captain.

```curl --insecure --data "skip=alabaster" https://curlingfun:9090/```
* The --data option allows you to send the specified data in a HTTP POST request. The generic format is --data "name=value". Like the previous question, I use the -k/--insecure option since the certificate is self signed (URL has https not http, which wouldn't need -k/--insecure due to the lack of a cert).

 4. Working with APIs and embedded devices often requires maintaining session state by passing a cookie.  Use curl to send a request to https://curlingfun:9090/ with a cookie called "end" with the value "3", indicating we're on the third end of the curling match.  

```curl --insecure --cookie "end=3" https://curlingfun:9090/```
* After struggling for a bit and typing hint to get a hint, the hint tells me to use the --cookie option to pass cookies. I use that hint to make the right command. Like the previous two questions, I still need the -k/--insecure option since the certificate for the HTTPS protected page is self signed. Without that option I'd get an error. 

5. Working with APIs and embedded devices sometimes requires working with raw HTTP headers.  Use curl to view the HTTP headers returned by a request to https://curlingfun:9090/

```curl --insecure -v https://curlingfun:9090/```
* The --insecure option is still neeeded since the the HTTPS page uses a self-signed certificate. The -v/--verbose option tells cURL to return more information, including the HTTP headers involved in the request to the URL I specified.

6. Working with APIs and embedded devices sometimes requires working with custom HTTP headers.  Use curl to send a request to https://curlingfun:9090/ with an HTTP header called "Stone" and the value "Granite"

```curl --insecure -H "Stone: Granite" https://curlingfun:9090/```
* The -H/--header option is used to work with custom HTTP headers. The -k/--insecure option is still needed as it is for previous questions for the same reason. The generic format for the -H/--header option is -H "HeaderName: HeaderValue".

7. curl will modify your URL unless you tell it not to.  For example, use curl to retrieve the following URL containing special characters: https://curlingfun:9090/../../etc/hacks

```curl --insecure --path-as-is https://curlingfun:9090/../../etc/hacks```
* Earlier before question 1, I get two hints for this challenge in the event. One of them is to use cURL's "--path-as-is" option. This controls a default behavior. In this case the default behavior is how cURL will modify your URL unless you tell it not to. I use that argument/option, and the --insecure option is still needed.

![Screenshot 2024-12-25 125344](https://github.com/user-attachments/assets/6ae0013e-5fc6-4b76-8a9b-d4500782bfac)

That's the last question to get the silver trophy for this challenge. Let's see what's required for the gold trophy in this challenge. 

![Screenshot 2024-12-25 125655](https://github.com/user-attachments/assets/679e9be1-0db9-41f0-9a86-4500caf438f9)

The trick here is to craft one command that fits all of those requirements/conditions. To do this, I must combine some of the arguments I learned how to use in the previous questions for the silver trophy into one command. 

First, I know I need to use the -k/--insecure option, since I'm making a request to the same HTTPS page that uses a self-signed request. This was covered in question 2.

Next, I notice that since it's an HTTP post request, this will require the --data argument in the format --data "name=value". The parameter is "skip" and the value is "bow", so the argument will look like --data "skip=bow". This concept was covered in question 3 above. 

Then, since the requirement mentions using a cookie, I know I need to use the --cookie option. The generic format is --cookie "Name=Value", or in this case --cookie "end=10". This was covered in question 4.

Lastly, the requirement mentions using an HTTP header. The -H/--header option is used to work with custom HTTP headers. The generic format for the -H/--header option is -H "HeaderName: HeaderValue". This was covered in question 6. In this case, the argument would be -H "Hack: 12ft". Combining all of these pieces together, I arrive at the command below. 

```curl --insecure --data "skip=bow" --cookie "end=10" -H "Hack: 12ft" https://curlingfun:9090/```

This command works successfully, and I see the following output to make a new complex command.

![Screenshot 2024-12-25 130526](https://github.com/user-attachments/assets/3fa06564-2d5a-42b9-a740-2cf3b5fae062)

This question will require the "--path-as-is" option. This controls a default behavior, where cURL will modify your URL unless you tell it not to. I use this argument/option, and the --insecure option is still needed. This is covered in question 7 above. 

# Gold Trophy

```curl --insecure --path-as-is https://curlingfun:9090/../../etc/button```

The command works successfully and I get the last question for the gold trophy in this challenge. 

![Screenshot 2024-12-25 130827](https://github.com/user-attachments/assets/41befc2a-2fc0-4fb0-8c35-52f235ac94bb)

When I read this question, redirects is the keyword that stuck out to me. I searched for "curl url redirection" and found out about the -L/--location option, which allows cURL to follow a redirect. I still need the -k/--insecure option.

```curl --insecure --location https://curlingfun:9090/GoodSportsmanship```

This last question gives me the gold badge for this challenge. Now I move onto the Frosty Keypad challenge. 

![Screenshot 2024-12-25 131204](https://github.com/user-attachments/assets/74c15405-4020-4200-8634-4a4b12b6e671)

Next Challenge: 
* [Hardware Hacking - Silver](https://github.com/Rockman-Blue/SANS_HHC_2024/blob/a8a920e4ff7106041084d52cfadcc38fa654accb/Act%201/Hardware-Hacking.md)
