## Examining Telnet and SSH in Wireshark
#### Objectives
- Part 1: Examine a Telnet Session with Wireshark
- Part 2: Examine an SSH Session with Wireshark
#### Background / Scenario

A router will be configured to accept SSH connectivity and use Wireshark to capture and view Telnet and SSH sessions. This will demonstrate the importance of encryption with SSH.

#### Required Resources
- CyberOps Workstation VM
  
**Part 1: Examining a Telnet Session with Wireshark**

Wireshark will be used to capture and view the transmitted data of a Telnet session.

**Step 1: Capture data.**

a. Open a terminal window and start Wireshark.
```
wireshark &
```

c. Start a Wireshark capture on the `Loopback: lo interface.`

d. Open another terminal window. Start a Telnet session to the **localhost**. 
```
telnet localhost
```

e. Stop the Wireshark capture after you have provided the user credentials.

**Step 2: Examine the Telnet session.**

a. Apply a filter that only displays Telnet-related traffic. Enter **Telnet** in the filter field and click Apply.

b. Right-click one of the Telnet lines in the Packet list section of Wireshark, and from the drop-down list, select **Follow > TCP Stream**.

![image](https://i.imgur.com/eFG9CS2.png)

c. The Follow TCP Stream window displays the data for the Telnet session with the CyberOps Workstation VM. The entire session is displayed in plaintext, including the password.

![image](https://i.imgur.com/2yQe6Xe.png)

d. Click Close.

e. Type exit at the terminal to exit the Telnet session.
```
exit
```

**Part 2: Examine an SSH Session with Wireshark**

In Part 2, an SSH session will be established with the localhost. Wireshark will be used to capture and view the data of this SSH session.

a. Start another Wireshark capture.

b. Establish an SSH session with the localhost. At the terminal prompt, enter ssh localhost. Enter yes to continue connecting. Enter the password when prompted.
```
ssh localhost
```

c. Stop the Wireshark capture.

d. Apply an SSH filter on the Wireshark capture data. Enter **ssh** in the filter field and click Apply.

e. Right-click one of the **SSHv2** lines in the Packet list section of Wireshark, and in the drop-down list, select the **Follow > TCP Stream** option.

f. Examine the Follow TCP Stream window of your SSH session. The data has been encrypted and is unreadable. 

![image](https://i.imgur.com/KqyZeZn.png)

g. Click Close.

h. Close Wireshark.

#### Conclusion

Similar to Telnet, SSH is used to access and execute commands on a remote system. However, SSH protocol allows users to communicate with remote systems securely by encrypting the communications. This prevents any sensitive information, such as usernames and passwords, from being captured during the transmission.

#### References
https://www.netacad.com
