<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory: Account Lockouts & Management</h1>
This tutorial outlines examples of using Active Directory with account lockouts, enabling/disabling accounts, and observing logs.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Group Management Console (GPMC)
- Powershell

<h2>Operating Systems Used </h2>

- Windows Server 2022 (Domain Controller - DC-1)
- Windows 10 (21H2) (Client Machine - Client-1)

<h2>High-Level Deployment and Configuration Steps</h2>

- Dealing with Account Lockouts
- Enabling and Disabling Accounts
- Observing Logs

<h2>Deployment and Configuration Steps</h2>

<h3 align="center"> Dealing with Account Lockouts </h3>

<h4 align="center">Configure Group Policy to Lockout the account after 5 attempts:</h4>
<p align="center">
Open Group Policy Management Console (GPMC) after logging into DC-1 by clicking Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.
</p>
<br/>
<p>
<img src="https://i.imgur.com/x5GUlbA.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">In the GPMC, navigate to the Group Policy Objects section.
"Default Domain Policy" right click and edit it. 
</p>
<br/>
<p>
<img src="https://i.imgur.com/P9jOXyp.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">In the Group Policy Management Editor, expand the following: Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
</p>
<br/>
<p>
<img src="https://i.imgur.com/u39hRe9.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">Set account lockout duration to be 30 min. Account lockout threshold should automatically set to 5 invalid logon attempts. If not then configure account lockout threshold.
</p>
<br/>
<p>
<img src="https://i.imgur.com/fwgdLmW.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">Update group policy by forcing an update immediately (for the account lockout threshold to take affect right away). Done by logging into client (can be done by logging in as Jane Doe > powershell > "gpupdate /force"
</p>
<br/>
<p>
<img src="https://i.imgur.com/MTurp1U.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">Verify the Policy to make sure it actually updated. Run Command Prompt as administrator > "gpresult /r" run > rsop.msc then look at the applied settings. You should see that the Applied Group Policy Objects include: Default Domain Policy
</p>
<br/>
<p>
<img src="https://i.imgur.com/roPc5tr.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">Pick a random user account you created previously and attempt to log in (into client-1) with it 6 times with a bad password. 6 because that is one more than the account lockout threshold allows (the policy we edited)
</p>
<br/>
<p>
<img src="https://i.imgur.com/YAyJlvw.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center"> Observe that the account has been locked out within Active Directory users and computers. Look for the user you purposely locked out. Account Properties > Account > click "unlock account". Attempt to login with it to see the changes. You should be able to login with that user now.
</p>
<br/>
<p>
<img src="https://i.imgur.com/boOkVNQ.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center"> Reset the users password and then attempt to login. Active Directory Users and Accounts > right click user we used before > reset password
</p>
<br/>
<p>
<img src="https://i.imgur.com/YihEOtc.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center">Enabling and Disabling Accounts</h3>

<p align="center">
Disable the same account in Active Directory. Active Directory Users and Accounts > right click user we used before > disable account
</p>
<br/>
<p>
<img src="https://i.imgur.com/uxT44SV.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Attempt to login with it, observe the error message
</p>
<br/>
<p>
<img src="https://i.imgur.com/9VPS8V6.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p align="center">
Re-enable the account and attempt to login with it.
</p>
<br/>
<p>
<img src="https://i.imgur.com/QqbFYaC.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<h3 align="center">Observing Logs</h3>

<p align="center">
Observe the logs in the Domain Controller. Windows search bar "eventvwr.msc". Windows Logs > Security right click and find: user with failed logon attempts we used.
</p>
<p align="center">
You can mess around with it and find more events in the logs but this is just an introduction.
</p>
<br/>
<p>
<img src="https://i.imgur.com/Mi0bv81.png" height="75%" width="100%" alt="Disk Sanitization Steps"/>
</p>
<br/>

<p>In this lab, we explored Active Directory account management by configuring account lockout policies, enabling and disabling user accounts, and analyzing security logs. We learned how to enforce security measures through Group Policy, respond to account lockouts, and monitor authentication events—essential skills for system administration and cybersecurity operations.
</p>


