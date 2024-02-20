<h1>Welcome to the Virtual Home Lab with Active Directory Setup Project!</h1>

<h2>Overview:</h2>

<p>This project is a step-by-step guide to creating a virtual environment using VirtualBox. It features a Domain Controller (DC) acting as an Active Directory server and a User Machine for domain integration.</p>

<h2>Key Features:</h2>

<ul>
    <li><strong>Step-by-Step Setup:</strong> Follow detailed instructions to create virtual machines, configure networking, and set up the Active Directory domain.</li>
    <li><strong>Active Directory Configuration:</strong> Understand how to configure an Active Directory environment, including user accounts, group policies, and organizational units.</li>
    <li><strong>User Machine Integration:</strong> Learn to join a machine to the domain, enabling seamless user authentication and centralized management.</li>
</ul>

<h2>Getting Started:</h2>

<ol>
    <li><a href="https://www.virtualbox.org/"> Install VirtualBox</a></li>
    <img src="https://i.imgur.com/d1oVU94.png" </img>
    <li><a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019"> Install Windows Server 2019</a></li>
    <img src="https://i.imgur.com/4qo5EXF.png" </img>
    <li>Once both images are downloaded and added to VirtualBox, make sure the Network type is set to "Bridged"</li>
    <img src="https://i.imgur.com/9FHAItL.png" </img>
    <li>Boot the Domain Controller(2019 Server) vm up. You're going to have to walk through the installation steps, similarly to setting up a new OS. </li>
    <img src="https://i.imgur.com/5h0DkwK.png" </img>
    <li>Here you want to select the 4th option "Windows Server 2019 Datacenter Evaluation (Desktop Experience)"</li>
    <img src="https://i.imgur.com/eeJJmpn.png" </img>
    <li>Here you want to select the Custom Installation Option</li>
    <img src="https://i.imgur.com/tgkVlf3.png" </img>
    <li>You want to select the drive you want the Operating System installed onto and hit next. After that the Server will install.</li>
    <img src="https://i.imgur.com/B6faLg2.png" </img>
    <li>Once the installation of the Server is done, you will be prompted to enter a password for the main Admin account. Make this something memorable.</li>
    <img src ="https://i.imgur.com/KariqGs.png" </img>
    <li>Once you've logged into the account, you will see that Server Manager boots up automatically. In Server Manager you want to click on the "Local Server" tab. 
    There you want to change the Computer Name. I changed the Computer name to DC1 (Domain Controller). 
    You might be prompted to restart the computer, this can be done at a later time, so click "Restart Later" for now. </li>
    <img src="https://i.imgur.com/WLtE5rG.png" </img>
    <li>So now we want to set our ip to static. To do this you want to go to Control panel > Network and Internet > Network Connections. Here you will see the Ethernet Connection, you want to right click on it and hit "Properties". Under the Properties section, you want to double click on IPV4. By default it will be set to "Obtain an IP address automatically. You want to change this to Static. The Subnet mask and Default Gateway will remain the same. And for the DNS you want to set this to 8.8.8.8. </li>
    <img src="https://i.imgur.com/fANs9yC.png" </img>
    <img src="https://i.imgur.com/j0m0VDn.png" </img>
    <li>Once this is done, go ahead and give the VM a reboot. </li>
    <li>Now we want to move onto our test VM. This is a normal windows machine that we'll use to test our connection to the Domain Controller Server. For this, you need to boot up the VM and it should automatically log you into the "User" account. This is the default builtin Admin account. </li>
    <li>Here we want to do the same thing as the DC server. So lets change our ip address to a static. To do this you want to go to Control panel > Network and Internet > Network Connections. The only difference here will be for the DNS you want to make it the IP of the Domain controller. For me, the ip of my Domain Controller was 192.168.0.19, so I put that as the preferred DNS for my test machine.</li>
    <img src="https://i.imgur.com/5zyZcNp.png" </img>
    <li>Oce you've done that. Go ahead and give the Test VM a reboot. Once the VM has booted up again, lets enable the Network Sharing Settings. To do this you want to go to Control Panel > Network and Internet > Netowrk and Sharing Center > Change Advanced Sharing Settings. Here we want to make sure everything is enabled under "Private Networks", "Public Networks", "Domain Networks" and "All Networks". You want to do the same for the Server itself (both VMs). What this will do is allow both our Test Machine and Server to talk to each other.</li>
  <img src="https://i.imgur.com/vTRwB31.png" </img>
    <li> What we want to do now is open up both our server and test machine side by side. And we're going to try and have them ping each other. If done correctly, both Server and Test VM should be communicating with each other. If they are not, please double check the IP, DNS, and Network Sharing Settings.</li>
    <img src="https://i.imgur.com/GCII7zE.png" </img>
    <li>Now we want to hop back into the Domain Controller VM. Here what we want to do is open up Server Manager if it already isn't open. </li>
    <img src="https://i.imgur.com/AaGVuaj.png" </img>
    <li>On the top right you will see "Manage". You want to Click on Manage > Select "Add Roles and Features". Here you want to keep hitting next until you get to the "Server Roles" section. Under the Server Roles, you want to select "Active Directory Domain Services" and "DNS Server","Group Policy Management", and ".NET Framework 4.7 Features". Then your going to hit Next, and under the "Select Features" you want to leave it as is and hit Next. Then you just want to keep hitting next until it starts the installation process. Once the installation finishes, you will see the option to "Promote this Server to a Domain Controller". You want to go ahead and click that. This is where we will be creating our actual Domain that we will connect our Test VM to.</li>
    <img src="https://i.imgur.com/sih5qPY.png" </img>
    <li>You're going to select the "Add a New Forest" option. And for the Root Domain name, you're going to create the Domain name. This can be anything you'd like it to be. I set mine to "Cybersecurity.com". Once you've created the domain name, it will ask you to create the password for this. Make it something memorable and hit next. It will verify your DNS settings. You dont have to enter anything for the "NetBios domain name" it should autofill. You can hit next until the installation begins. Once the installation finishes, your VM will reboot automatically. </li>
    <img src="https://i.imgur.com/esn5JnU.png" </img>
    <img src="https://i.imgur.com/NjjXNXL.png" </img>
    <li>Once it boots up, you will see that your domain name comes up on the Admin account at the login screen.</li>
    <img src="https://i.imgur.com/0nax3PW.png" </img
    <li>We now want to login and go back into Server Manager, here is where we will be configuring AD. Go to Tools(top right) > and click on "Active Directory Users and Computers". </li>
    <img src="https://i.imgur.com/mCeMojD.png" </img>
    <li>This will open up Active Directory. Here you want to drop down your domain name, and you will see a list of folders. You want to click on the "Users" folder, this is where you can add/remove any user. For testing purposes I created a new user called "John Doe" and set his username to "JDoe", you can name yours whatever you like. This is going to be the account we use to login to the Test VM.</li>
    <img src="https://i.imgur.com/2tpDIRi.png" </img>
    <img src="https://i.imgur.com/TNyWzZD.png" </img>
    <li>Now we want to open up our Test VM. Here we will login to the default built-in "user" account first. Then you want to go to "About your PC" > Click on "Domain or Workgroup" > "Change". By default this will be set to "WORKGROUP". We want to change this to our Domain name we setup in the DC controller. Once you change it, the machine will require admin credentials. This is where you can enter the Admin credentials of the DC controller VM. Once you enter them, the machine will require a reboot, so go ahead and do that. <ins>NOTE: if Joining the domain fails, please double check the network and network sharing settings.</ins></li>
    <img src="https://i.imgur.com/RsOU51D.png" </img>
    <img src="https://i.imgur.com/KLcettZ.png" </img>
    <li>Once the Test VM boots back up, you will see a "Other User" option at the bottom. Go ahead and click on it. This will prompt you to enter a username and a password. Here we will user our John Doe account we created in Active Directory in the DC Server.</li>
    <img src="https://i.imgur.com/8PAlB7u.png" </img>
    <img src="https://i.imgur.com/IKu1ryy.png" </img>
    <li>And now if everything is done correctly, we should be logged in as our test user.</li>
    <img src="https://i.imgur.com/Cub5r3o.png" </img>

</ol>

<h2>Contribution:</h2>

<p>Contributions are welcome! Feel free to provide feedback, suggest improvements, or expand on the existing documentation through pull requests.</p>

<h2>Disclaimer:</h2>

<p>This project is for educational purposes and should be used in a controlled environment. Configurations may not be suitable for production use.</p>

<p><strong>Happy Virtual Labbing!</strong></p>
