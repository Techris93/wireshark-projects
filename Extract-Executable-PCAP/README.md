## Objectives

Part 1: Analyze Pre-Captured Logs and Traffic Captures

Part 2: Extract Downloaded Files from PCAP

### Background / Scenario

Analyzing logs is crucial, but it is equally important to comprehend the process of network transactions at the packet level. In this lab, we will examine the traffic within a preexisting PCAP file and extract an executable from it.

### Required Resources

- CyberOps Workstation virtual machine
- Wireshark
  
### Instructions

**Part 1: Analyze Pre-Captured Logs and Traffic Captures**

In Part 2, we will work with the nimda.download.pcap file. Captured in a previous lab, nimda.download.pcap contains the packets related to the download of the Nimda malware.

a. Change directory to the support.files/pcaps folder, and get a listing of files using the `ls –l` command.
```
cd lab.support.files/pcaps
ls -l
```

b. Issue the command below to open the download.pcap file in Wireshark.
```
wireshark nimda.download.pcap &
```
![image](https://i.imgur.com/ONHkZ1b.png)

c. The download.pcap file contains the packet capture related to the malware download performed in a previous lab. The pcap contains all the packets sent and received while tcpdump was running. Select the fourth packet in the capture and expand the Hypertext Transfer Protocol to display as shown below.

![image](https://i.imgur.com/SOEzZ51.png)

d. Packets one through three are the TCP handshake. The fourth packet shows the request for the malware file. Confirming what was already known, the request was done over HTTP and sent as a GET request.

e. Because HTTP runs over TCP, it is possible to use Wireshark’s Follow TCP Stream feature to rebuild the TCP transaction. Select the first TCP packet in the capture, a SYN packet. Right-click it and choose Follow > TCP Stream.

f. Wireshark displays another window containing the details for the entire selected TCP flow.

![image](https://i.imgur.com/aGCxNEa.png)

**Note:**
- The symbols are the actual contents of the downloaded file. Because it is a binary file, Wireshark does not know how to represent it. The displayed symbols are Wireshark’s best guess at making sense of the binary data while decoding it as text.
- There are a few readable words spread among the symbols. Those are strings contained in the executable code. Usually, these words are part of messages provided by the program to the user while it runs. While more of an art than a science, a skilled analyst can extract valuable information by reading through these fragments.
- Despite the W32.Nimda.Amm.exe name, this executable is not the famous worm. For security reasons, this is another executable file that was renamed as W32.Nimda.Amm.exe. Using the word fragments displayed by Wireshark’s Follow TCP Stream window, Scrolling down on that window reveals that this is the Microsoft Windows cmd.exe file.
  
![image](https://i.imgur.com/SAOLBFi.png)

**Part 2: Extract Downloaded Files from PCAP**

Because capture files contain all packets related to traffic, a PCAP of a download can be used to retrieve a previously downloaded file. 

Follow the steps below to use Wireshark to retrieve the Nimda malware.

a. In that fourth packet in the download.pcap file, notice that the HTTP GET request was generated from 209.165.200.235 to 209.165.202.133. The Info column also shows this is in fact the GET request for the file.

b. With the GET request packet selected, navigate to File > Export Objects > HTTP, from Wireshark’s menu.

c. Wireshark will display all HTTP objects present in the TCP flow that contains the GET request. In this case, only the Nimda.Amm.exe file is present in the capture.

![image](https://i.imgur.com/cJpzJqm.png)

**Note:**
- W32.Nimda.Amm.exe is the only file in the capture because the capture was started right before the download and stopped right after. No other traffic was caught while the capture was active.

d. In the HTTP object list window, select the Nimda.Amm.exe file and click Save As at the bottom of the screen.

e. Click the left arrow until you see the Home Click Home and then click the analyst folder (not the analyst tab). Save the file there.

f. Return to your terminal window and ensure the file is saved. Change directory to the /home/analyst folder and list the files in the folder using the ls -l
```
cd /home/analyst
ls –l
```

g. The file command gives information on the file type. Use the file command to learn a little more about the malware, as show below:

```
file W32.Nimda.Amm.exe
```

![image](https://i.imgur.com/ukMugF1.png)

As seen above, W32.Nimda.Amm.exe is indeed a Windows executable file.

### Conclusion
- The next step in the malware analysis process for a security analyst would be to identify the type of malware and analyze its behavior. This involves moving the malware file to a controlled environment and executing it to observe its behavior. Malware analysis environments often use virtual machines and are sandboxed to prevent damage to non-test systems. These environments typically include tools for monitoring malware execution, such as resource usage, network connections, and operating system changes.
- There are also a few Internet-based malware analysis tools. VirusTotal (virustotal.com) is one example. Analysts upload malware to VirusTotal, which in turn, executes the malicious code. After execution and some other checks, VirusTotal returns a report to the analyst.

### References 
https://contenthub.netacad.com/cyberops/
