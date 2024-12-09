# Active-directory
this is a project that i've worked on, called Active directory.


![project](https://github.com/user-attachments/assets/78688d86-09cd-4fb4-8da1-646b97176f8a)




I’ve made an active directory project, but it was unfinished because of some unknown problems. 
I’ve ran through the process many times and couldn't figure it out. 
But because of that I know how to set the ip address, and use CLI to check on the IP address . 

I set up the VB (Virtualbox) and set up the necessary settings before launching the VB guest operator. Including setting up 2 adapters, and Connecting the IP address. I was able to make a domain and created a new forest for the internet and used the commands to check if the IP address had worked. Even though the CLI says it works but unfortunately, it didn’t respond and I wasn't able to connect the domaintory.

Here are the resources and websites i used to do this project 
Download and install VirtualBox from VirtualBox.org.
https://www.virtualbox.org/wiki/Downloads
Download Microsoft C++ Redistributable 2019 from the Microsoft website.
https://aka.ms/vs/17/release/vc_redist.x64.exe
Download Windows Server 2019 ISO (for the Domain Controller).
https://go.microsoft.com/fwlink/p/?LinkID=2195167&clcid=0x409&culture=en-us&country=US
Download Windows 10 ISO (for the client machine).
https://go.microsoft.com/fwlink/?LinkId=2265055
Even though I didn't finish this project, I know the necessary steps to make to finish the active directory. I’ve written down the instructions below

Step 6: Installing the Guest Additions
In your Server VM, click on “Devices”. This will be at the very top of your VM window. Then click on the option that says “Insert Guest Additions CD image…”. (Nothing visibly will happen.) 
From inside of your VM, click on the File Explorer icon in your taskbar (the picture of the folders) and within your CD Drive, you will see “Virtual Box….”. Double click that to open the program. From here, you will double click the ‘VBoxWindowsAdditions-amd64” to run the program. Keep clicking on “Next” until you are able to “Install” and you’re done. Choose the option to restart the VM and go to the next step after you log back in.
This will help us to drag’n drop from our real computer to the VM and more.
Step 7: Create a Client VM and Join the Domain
Create Client VM:
Create another VM in VirtualBox, name it (e.g., Superman), and use the Windows 10 ISO.
Follow the Windows 10 installation process to install. CLICK THE BOX THAT SAYS “SKIP UNATTENDED INSTALLATION”. THIS WILL ALLOW YOU TO CHOOSE YOUR OPERATING SYSTEM AND WE’RE CHOOSING WIN 10 PRO, NOT HOME.
You do not have a product key (Evaluation Copy allows 180 days before asking for a product key), so click on that option.
Choose Windows 10 Pro and choose “Custom: Install Windows only” at the next screen or two, and keep the rest of the options at the default until it is installed.
Use an offline account and limited experience when asked. It’s going to have you choose security questions and answers, you answer it but it’s not going to matter later.
Configure Client Networking:
Set the client to obtain an IP address from the DHCP server.
Verify the IP address using ipconfig /renew on the client.
Join the Domain:
Rename the client and join the domain (e.g., DCUniverse.com).
Go to settings, about and click on “Rename this PC” to change the name of it.
Back the settings home, type in “Work” in the search bar and choose the option to “Access work or school”. Click on “Connect” and towards the bottom of the screen, choose “Join this device to a local Active Directory domain”. Put your domain name in, click next.
Use domain admin credentials to complete the process.
Step 8: Create User Accounts in Active Directory
Create Organizational Units (OUs):
In Active Directory Users and Computers, create a new OU (e.g., Admins).
Go to the Start menu, expand the “Windows Administrative Tools” folder and choose Active Directory Users and Computers.
Right click on your Domain Name, hover over “New” and choose “Organizational Unit”. Name this “Admins” and click “OK”.
Click the arrow to the left of your Domain name and you’ll see the folder you just created. Right click on the new “Admins” folder and choose “User”. Put your name in the boxes and for “User logon name”, put an “A” and your name. (We’re creating a local admin account here.) When asked about a password, give it the default password “P@ssw0rd1”, uncheck the 1st checkbox and put a check in the 3rd checkbox, “Password never expires”. Click “Next” then “Finish”.
Though this account is in a folder named Admins, it’s only a user account, so we need to add this to the Admins group. Right click on your account within the “Admins” folder, choose “Properties”, click on the “Member Of” tab, click “Add” and a “Select Groups” box will pop up. In the open space, click in it and type in “domain admins”, click on “Check Names” and it will find that group. Click “OK” and now it’s a Domain Admin. Click “OK”, then “Apply” to save and “OK” to close it.
We’re going to sign out of this account and sign in as ourselves, the account we just created. Click on the Windows/Start button of your VM, NOT OF YOUR REAL COMPUTER, click on the icon of a person and sign out. Click on “Input” on the top of your VM window, hover over “Keyboard” and choose “Insert Ctrl-Alt-Del” and put in A(YourName) then the default password (P@ssw0rd1) to sign in.
We have to install RAS and NAT, so with the Server Manager window open, click on “Add roles and features”, click “Next” 4 times until you can choose the “Roles”. Select “Remote Access” and click next twice and for the “Role services”, we’re going to select “Routing” and click on “Add Features” on the next window that pops up and click “Next” until you are able to click on the “Install” button, then click on “Install”. When It’s done installing, close it and go to tools in your Server Manager Dashboard and click on “Routing and Remote Access”. Right click on your Domain and choose “Configure and Enable Routing and Remote Access”. Click “Next’’ then choose “Network address translation (NAT)” and click “Next”. It’s going to ask you which network interface you want to use and you’re going to choose your Internet adapter. Click “Next” then “Finish”. Whatever box that pops up after that, just click “OK” then “Finish” again. 

Step 9: Configuring the DHCP

Click on “Add roles and features” on the Server Manager Dashboard, click “Next” 3 times until you can choose a role. The role we are going to choose is the “DHCP Server”, then click “Next” again 3 times until you are able to click on the “Install” button to install that role. When done, click “Close”.
Within the Server Manager Dashboard, click on “Tools” to the right of the flag and choose “DHCP”. We’re going to set up the scope for the IP address. Click on your Domain and click on “IPv4” then right click “IPv4” to choose “New Scope…”. The New Scope Wizard will pop up and you’re going to click “Next” and for the name, we’re going to put in the IP address range, which is 172.16.0.100-.200 then click next. For the next screen, we’re going to put in the Start of the IP range in the first box and the End of the IP range in the second box. So, the first box will have 172.16.0.100 and the second box will have 172.16.0.200. We’re going to change the subnet mask to 255.255.255.0 then click “Next”. We're going to leave the exclusions empty so just click “Next”. We’re going to use the default of the “Lease Duration”, so just click “Next” until you see the “Finish” button and click on it to finish the configuration. Now let’s refresh our IPv4. Right click on “IPv4” and choose “Refresh”. Right click on your Domain and click on “Authorize”. Right click on your Domain again and click on “Refresh”. You will see the red arrow turn into a green check mark. Then close the DHCP window. Let’s add the users now.

Step 10: Adding Users
Create Users:
Create a user account manually or use a PowerShell script to automate user creation.
Step 10a: Adding User Accounts in Active Directory From My Script
Step 1: Access and Download the Script from GitHub
Navigate to the GitHub repository:
Visit your GitHub profile at www.github.com/bgleton1031.
Locate the repository that contains the script for adding users to Active Directory. https://github.com/bgleton1031/ActiveDirectory_PowerShell
Download the script:
Once you’ve found the correct repository, download these scripts and file to your local machine.
Generate Names User PowerShell
Create Users PowerShell
Names.txt
Typically, you would click the Code button and select Download ZIP, or you could clone the repository using Git commands if you prefer.
Step 2: Prepare the Active Directory Environment
Before running the script, ensure your domain controller and AD setup are functioning. Make sure you've promoted the server to a domain controller and created any necessary Organizational Units (OUs) where the users will be placed.
Step 3: Open PowerShell as Administrator
Launch PowerShell ISE:
Click on the Start menu and search for Windows PowerShell ISE.
Right-click on Windows PowerShell ISE and select Run as administrator.
Change the Directory to the location of your script:
Once PowerShell ISE is open, navigate to the directory where you downloaded your script using the cd (Change Directory) command:
bash
Copy code
cd "C:\Path\to\your\script"


Step 4: Inspect the Script
Open the script:
In PowerShell ISE, open the script by going to File → Open, and navigate to the downloaded script.
This will allow you to view and potentially modify it if necessary.
Check for Dependencies:
If the script references external files like a names.txt for a list of user names, ensure that the file is present in the correct path.
Make sure all required data files (like lists of usernames) are correctly formatted.
Step 5: Execute the Script
Run the Script:
In PowerShell ISE, click the Run button (green play button) or press F5 to execute the script.
If the script is designed to pull data from a file (like a list of user accounts), ensure the file path is correctly configured in the script.
Handle Security Policies:
If you encounter an error regarding script execution policies, you might need to temporarily allow scripts to run by setting the execution policy:
bash
Copy code
Set-ExecutionPolicy RemoteSigned


After running the script, you can revert the execution policy to its original state using:
	bash
	Copy code
	Set-ExecutionPolicy Restricted


Step 6: Verify User Creation
Open Active Directory Users and Computers:
After running the script, open Active Directory Users and Computers on your domain controller.
Navigate to the Organizational Unit (OU) where the users should have been added.
Check User Properties:
Inspect the newly created users to ensure their properties (such as username, passwords, and group memberships) match what you specified in the script.
Example of Script Structure
If your script uses a .txt file to create users in bulk, it might look like this:
Powershell
Copy code
# Define the path to the user list
$userList = Get-Content "C:\Path\to\names.txt"

foreach ($user in $userList) {
 	   $firstName = $user.Split(',')[0]
 	   $lastName = $user.Split(',')[1]
 	   $username = $firstName + "." + $lastName

 	   # Create a user in the specified Organizational Unit
 	   New-ADUser `
   	     -Name $username `
      	  -GivenName $firstName `
      	  -Surname $lastName `
       	 -SamAccountName $username `
      	  -UserPrincipalName "$username@dcuniverse.com" `
      	  -Path "OU=Admins,DC=dcuniverse,DC=com" `
      	  -AccountPassword (ConvertTo-SecureString "Password01" -AsPlainText -Force) `
       	 -Enabled $true
}

In this example, a file named names.txt could contain names in the format:
Copy code
John,Doe
Jane,Smith

The script will loop through each line of the names.txt file, splitting each entry into first and last names, and then creating users with those details in Active Directory.
Step 7: Troubleshooting
Error with file paths: If the script is unable to locate the text file or any external dependencies, ensure the file path is correct and accessible from the machine where you're running the script.
Script permissions: If you receive a "Permission Denied" error, verify that the account running the script has the necessary permissions to create users in AD.

Step 10: Verify Connectivity and Domain Access
Test User Login:
Attempt to log in to the client machine with a domain user account.
Ensure that the client can communicate with the domain controller.
Validate DHCP and AD Functionality:
Check the DHCP leases in DHCP Manager.
Ensure the client machine is receiving an IP address from the DHCP server.
Step 11: Final Testing and Troubleshooting
Test Domain Features:
Ensure policies can be applied and users can log into any client machine on the domain.
Verify that file sharing, login, and network connectivity are functioning properly.
Troubleshoot Common Issues:
Resolve any errors related to IP addressing, user creation, or domain joining.
Once all steps are completed, you will have a functional domain controller, DHCP server, and a client machine joined to the domain.






