# Sysmon Events

<h2>Description</h2>
In this task, I installed sysmon and configured it with powershell and explored the different sysmon logs using specific sysmon event ids to observe a reverse tcp connection form notmalware.exe.  

<h2>Languages and Utilities Used</h2>

- <b>Sysmon</b>
- <b>POwershell</b>
- <b>Event Viewer</b>

<h2>Environments Used</h2>

- <b>Windows 10 Enterprise</b>
- <b>Ubuntu</b>

<br />
<br />
Using powershell to isntall sysmon with  the switftonsecurity sysmon-config from: https://github.com/SwiftOnSecurity/sysmon-config 

![1) installing sysmon64 with github config](https://github.com/user-attachments/assets/2e73554b-7768-4a1e-8bfd-4d8f9d4cb233)

<br />
<br />
Re-establishing a reverse tcp connection on windows vm.

![2) reinfecting windows with reverse tcp shell](https://github.com/user-attachments/assets/788c41b0-1af4-4c86-b2b3-45c806219830)

<br />
<br />  
On event viewer, filtering for sysmon event id 3 shows the network connection and other artifacts to my reverse tcp Ubuntu attacker VM. 

![3) observe network connection for sysmon event id 3](https://github.com/user-attachments/assets/cdb5e148-8f92-420e-bd88-6dfb53ecc573)

<br />
<br />
Filtering for sysmon event id 1 and process id 7004 shows the process created from notmalware. 

![4) filtering for event id 1 and finding process id 7004 shows the specifc process creation for the malware](https://github.com/user-attachments/assets/ba622134-774c-47a4-9928-a86dcdc99fcf)

<br />
<br />
Downloading mimikatz from parrotsec github. 

![5) downloading mimikatz from github](https://github.com/user-attachments/assets/9e60cd8a-e915-48fa-865c-90feb39adaee)

<br />
<br />
Filtering for sysmon event id 11 shows the file download of mimikatz from microsoft edge. 

![6) sysmon event id 11 file creation shows mimikatz](https://github.com/user-attachments/assets/b8e9ace8-50f4-4d00-a647-a67a015a5a87)

<br />
<br />
Filtering for sysmon event id 15 shows the filecreate stream hash. 

![7) sysmon event id 15 shows hashes](https://github.com/user-attachments/assets/8e48fecb-9f07-4558-a4f7-dd5ece90fb03)

<br />
<br />
Using "get-winevent -filterhashtable @{logname= "microsoft-windows-sysmon/operational"; id=3} -maxevents 1 | format-list *" to retrieve the most recent Sysmon Event ID 3 (network connection) and display all its properties in a list format. When executed, it will show detailed information about the latest network connection event logged by Sysmon, including:
TimeCreated: The timestamp of the network connection event,
ProcessId: The ID of the process that initiated the connection,
Image: The full path of the executable that made the connection,
User: The user account under which the process was running,
Protocol: The network protocol used (TCP or UDP),
SourceIp and SourcePort: The local IP address and port,
DestinationIp and DestinationPort: The remote IP address and port,
SourceHostname and DestinationHostname: The hostnames, if resolved,
Initiated: Whether the connection was initiated by the local process.

![8) powershell sysmon event query](https://github.com/user-attachments/assets/031c59aa-5400-4fe7-83c3-989fb442a057)

<br />
<br />
