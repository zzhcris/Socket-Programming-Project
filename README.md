a) Name: Zhihao Zhang

b) Student ID: 3662704153

c）In this project, a library management system with identity authentication is implemented. The system consists of a client server, a main server and three back-end servers. The workflow is as follows:

1. Start each server process in sequence, and then the client accepts the user name and password entered from the keyboard, and then encrypts the ciphertext and sends it to the main server for verification.

2. The main server performs verification based on the corresponding user registration information in the disk and returns the client verification information.

3. The client receives the verification information from the main server, and then chooses to let the user continue to enter the user name and password or enter the course code to query according to the situation, and then sends the code to the main server.

4. After receiving the course code, the main server forwards the message according to the first digit of the code and forwards it to the corresponding back-end server. If the first digit of the code is not one of the three types of HSL, it will directly return "Not Found".

5. After receiving the message code forwarded by the main server, the back-end server determines whether the course exists and returns information according to the situation.

6. The main server forwards the message to the client after receiving it from the backend.

7. The client presents the query results to the user.


d) 
- client.cpp: Connect to the main server over TCP. Send over the username and password to identify the user. Then, send the bookcode for the query. Show the result on the screen.
- serverM.cpp: Connect to the client over TCP. Connect to the serverH, serverL, and serverS over UDP. Get the information from the client and send it to the corresponding server and give the result back to the client.
- serverS/H/L: Query the status of the book based on the bookcode forwarded by serverM, and then forward the book status to the main server.


e) The output on the screen is the same as requested. Inside the coding files:
- client.cpp:
    - Read the username and password in string format.
    - Send to the main server in char[] format.
    - Get back the result in char[] format.
        - "0" means username not found.
        - "1" means wrong password.
        - "2" means both username and password are correct.
    - Read in bookcode in string format.
    - Send to the main server in char[] format.
    - Get back the result in char[] format.
        - "0" means book is available.
        - "1" means book is not available.
        - "2" means book does not exist.
        

- serverM:
    - map<string,int> to store user registration information
    - All the information sent or received in char[].
    - After receiving the code, if the prefix of this book is not within the HSL range, return "2" to the client.
    - Distribute the code to the corresponding backend server
    - Received result in char[] format
        - "0" means book is available.
        - "1" means book is not available.
        - "2" means book does not exist.

- serverH/S/L:
    - map<string,int> to store user registration information
    - All the information sent or received in char[].
    - According to the received code and its own map, the result is returned to the main server
        - "0" means book is available.
        - "1" means book is not available.
        - "2" means book does not exist.

g) The project works fine in regular conditions. It may crash if the user's input is too long, which is not a normal case.

h) I used some codes from Beej's guide. I also checked the Q&A from the piazza.

