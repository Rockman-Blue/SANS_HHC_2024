After clicking on "Go to Act I" in the story section of the game menu, I go left to talk to Bow Ninecandle to learn more about the cURLing challenge. 

![Screenshot 2024-12-24 101046](https://github.com/user-attachments/assets/3859ef6b-a885-4a26-9931-0e3a668b10b9)

Bow explains the basic concept of curl, a tool that transfers data to and from a server using URLs. I get two hints after talking to Bow:
*  Using the cURL man page at https://curl.se/docs/manpage.html
*  To use cURL's "--path-as-is" option. This controls a default behavior. 

By clicking on the curling setup, I access and interact with the challenge via a terminal. After typing y and hitting enter to start the challenge, I am presented with the first question. I am told that I can run "hint" to get a hint if I am stuck on a specific question.

![Screenshot 2024-12-24 101527](https://github.com/user-attachments/assets/be8dd99e-2cfd-41de-a21a-0f707c0362d0)

Below are the questions and solutions:

1. Unlike the defined standards of a curling sheet, embedded devices often have web servers on non-standard ports. Use curl to retrieve the web page on host "curlingfun" port 8080.

```curl http://curlingfun:8080```
* This first question is pretty straightforward. You can retrieve a webpage on a specific host by specifying the port after a :. The generic format in this case would be curl <hostname>:<port number>

2. Embedded devices often use self-signed certificates, where your browser will not trust the certificate presented.  Use curl to retrieve the TLS-protected web page at https://curlingfun:9090/

