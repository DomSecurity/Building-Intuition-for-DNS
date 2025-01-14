<p align="center">
<img src="https://i.imgur.com/CtGfsq8.png" height="65%" width="65%" alt="osTicket logo"/>
</p>

<h1>Building Intuition for DNS</h1>
In this lab we will be experimenting with DNS. This lab will help us have a better understanding of DNS.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- DNS

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Active Directory Virtual Machine
- Client Machine joined to your domain

<h2>Lab Steps</h2>
<p>
</p>
<p>
In this excerise, we'll be having a better understanding of A-Record, Local DNS Cache, and CNAME Record and how it works. We'll first start with A-Record by first going into Powershell on our Client-1 (Virual Machine created on Azure) and observe what takes place, once we try to ping a host, in this case "mainframe", which is not found in our Local DNS Cache, Local Host File, and DNS Server. We'll see ping request could not find host mainframe. 
</p>

<p>
<img src="https://i.imgur.com/BGQABLO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
  
Now we'll create an A-record on DC-1 for mainframe and have it point to DC-1 Private IP address. After, we'll then go back and attepmt to ping mainframe and observe that we get a reply. To create an A-record go to the AD -> Tools -> DNS -> DC-1 -> Forward lookup zones -> mydomain.com -> right click and create a new A record, title it mainframe.
<br />

<p>
<img src="https://i.imgur.com/xGu2iqq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/nDvXZP2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Now we will change the record address of "mainframe" to 8.8.8.8 if we go back to the Client-1 machine it will still ping the old adress even though we changed it. That is because we have to flush the DNS with the command ipconfig /flushdns. That will clear the DNS cache, when we attempt to ping mainframe again the address of the new record will show. 
</p>
<br />
<img src="https://i.imgur.com/WVxTfww.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  As we can see, even though we changed mainframe record IP address to 8.8.8.8, it's still reading as previous IP address 10.0.0.4. So now we will flush dns. 
</p>  
<img src="https://i.imgur.com/cdNOpG2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/DKGVhpu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
Lastly we will configure a CNAME record that points the host "search" to "www.google.com" If we ping "search" ping will not be able to find the host. We have to go back into the DNS tool on DC-1 and create the CNAME record "search". Once we create the CNAME record is created and we ping "search" it will resolve to www.google.com.
</p>
<br />
<p>
<img src="https://i.imgur.com/KKn2sGp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://i.imgur.com/CQ3drQu.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
