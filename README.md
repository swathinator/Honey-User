# Honey-User
(Antisyphon training lab from Cyber Deception/Active Defense)
## Creating Accounts
- cd into ```cd \IntroLabs ``` then run the bat file ```200-user-gen.bat```
- This is a list of example accounts with the honey user "Frank"<br><br>
<img width="283" alt="Screenshot 2025-03-29 at 6 56 21 PM" src="https://github.com/user-attachments/assets/a19a17c9-8932-47c1-96a6-8b7d5a26ec21" /><br>
## Event Viewer "SIEM"
- We will be using Event Viewer to get alerts on when anyone logs in as Frank
- We do this by navigating to Windows logs > Security > Create Custom View and adding this under the XML tab:
- Ensure "Edit Query Manually" is checked 
~~~~~~
<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">* [EventData[Data[@Name='TargetUserName']='Frank']]</Select>
  </Query>
</QueryList>
~~~~~~
- You can name filter the "Frank"
- We can see any events associated with Frank here <br>
<img width="956" alt="Screenshot 2025-03-29 at 7 09 28 PM" src="https://github.com/user-attachments/assets/a4dd54b2-26c9-4456-b16a-14e66d479b0e" /><br><br>
## Password Spray
- In PowerShell, run the following:
<pre>cd \IntroLabs</pre>
<pre>Set-ExecutionPolicy Unrestricted</pre>
<pre>Import-Module .\LocalPasswordSpray.ps1</pre>
