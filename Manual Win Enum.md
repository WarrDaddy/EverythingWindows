Notes from https://www.fuzzysecurity.com/tutorials/16.html 

**First let's find out what OS we are connected to:**

C:\Windows\system32> 

**Next we will see what the hostname is of the box and what user we are connected as.**

C:\Windows\system32> hostname b33f 
C:\Windows\system32> echo %username% user1

**Now we have this basic information we list the other user accounts on the box and view our own user's information in a bit more detail. We can already see that user1 is not part of the local group Administrators.**

C:\Windows\system32> net users
C:\Windows\system32> net user user1

**First let's have a look at the available network interfaces and routing table.**

C:\Windows\system32> ipconfig /all
C:\Windows\system32> route print

**arp -A displays the ARP (Address Resolution Protocol) cache table for all available interfaces.**
C:\Windows\system32> arp -A

**That brings us to the active network connections and the firewall rules.**
C:\Windows\system32> netstat -ano

**The following two netsh commands are examples of commands that are not universal across OS/SP. The netsh firewall commands are only available from XP SP2 and upwards.**

C:\Windows\system32> netsh firewall show state
C:\Windows\system32> netsh firewall show config

Finally we will take a brief look at the what is running on the compromised box: scheduled tasks, running processes, started services and installed drivers.

**This will display verbose output for all scheduled tasks, below you can see sample output for a single task. **
C:\Windows\system32> schtasks /query /fo LIST /v

**The following command links running processes to started services.** 

C:\Windows\system32> tasklist /SVC
C:\Windows\system32> net start

**This can be useful sometimes as some 3rd party drivers, even by reputable companies, contain more holes than Swiss cheese. This is only possible because ring0 exploitation lies outside most peoples expertise.**

C:\Windows\system32> DRIVERQUERY

** Checking for weak permission **

We can use sc to query, configure and manage windows services.

C:\Windows\system32> sc qc Spooler

**We can check the required privilege level for each service using accesschk.** 

C:\> accesschk.exe -ucqv Spooler

#### WMIC (Windows Management Instrumentation Command-Line) separately as it is Windows most useful command line tool.
To give you an idea about the extensive options that WMIC has I have listed the available command line switches below.

C:\Windows\system32> wmic /?

The first and most obvious thing we need to look at is the patchlevel. There is no need to worry ourself further if we see that the host is badly patched. My WMIC script will already list all the installed patches but you can see the sample command line output below.

C:\Windows\system32> wmic qfe get Caption,Description,HotFixID,InstalledOn

The best strategy is to look for privilege escalation exploits and look up their respective KB patch numbers. Such exploits include, but are not limited to, KiTrap0D (KB979682), MS11-011 (KB2393802), MS10-059 (KB982799), MS10-021 (KB979683), MS11-080 (KB2592799). After enumerating the OS version and Service Pack you should find out which privilege escalation vulnerabilities could be present. Using the KB patch numbers you can grep the installed patches to see if any are missing.

C:\Windows\system32> wmic qfe get Caption,Description,HotFixID,InstalledOn | findstr /C:"KB.." /C:"KB.."

Checking for weak permissions 
We can use sc to query, configure and manage windows services.
C:\Windows\system32> sc qc Spooler

We can check the required privilege level for each service using accesschk.
C:\> accesschk.exe -ucqv Spooler
