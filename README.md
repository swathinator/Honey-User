# Honey-User
(Antisyphon training lab from Cyber Deception/Active Defense)
## Creating Accounts
- In cmd, cd into ``` \IntroLabs ``` then run the bat file ```200-user-gen.bat```
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
- We will be using "Winter 2020" for our password spray with this command:
<pre>Invoke-LocalPasswordSpray -Password Winter2020</pre>
<img width="767" alt="Screenshot 2025-03-29 at 11 02 01 PM" src="https://github.com/user-attachments/assets/9093544e-c62b-437b-a343-ba9361b9245c" /> <br>
- There are 6 successful authentication attempts (it doesn't have to be Frank's, it just has to be an attempt)
- We can exit with ```exit``` and cleanup with ```user-remove.bat ```
- Let's check for any alerts in Event Viewer by going to Action > Refresh
<img width="919" alt="Screenshot 2025-03-29 at 11 05 48 PM" src="https://github.com/user-attachments/assets/788ca2c1-d2e5-491b-9c7e-397c695d1084" />
