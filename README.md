# Honey User
(Antisyphon training lab from Cyber Deception/Active Defense)<br><br>
Full lab explanation available on my <a href="https://medium.com/@swathitadepalli/active-defense-and-cyber-deception-antisyphon-training-44c0ee851be4#3857">Medium</a>
## Creating Accounts
- In cmd, navigate to  ```\IntroLabs``` using ```cd```, then run the batch file ```200-user-gen.bat```
- This generates a list of example accounts, including the honey user "Frank."<br><br>
<img width="283" alt="Screenshot 2025-03-29 at 6 56 21 PM" src="https://github.com/user-attachments/assets/a19a17c9-8932-47c1-96a6-8b7d5a26ec21" /><br>
## Event Viewer "SIEM"
- We will use Event Viewer to generate alerts whenever anyone logs in as Frank
- To set this up, navigate to: Windows Logs > Security > Create Custom View, then go to the XML tab and add the following:
- Ensure that "Edit Query Manually" is checked 
~~~~~~
<QueryList>
  <Query Id="0" Path="Security">
    <Select Path="Security">* [EventData[Data[@Name='TargetUserName']='Frank']]</Select>
  </Query>
</QueryList>
~~~~~~
- You can name the filter "Frank"
- We can see any events associated with Frank here <br>
<img width="956" alt="Screenshot 2025-03-29 at 7 09 28 PM" src="https://github.com/user-attachments/assets/a4dd54b2-26c9-4456-b16a-14e66d479b0e" /><br><br>
## Password Spray
- In PowerShell, run the following:
<pre>cd \IntroLabs</pre>
<pre>Set-ExecutionPolicy Unrestricted</pre>
<pre>Import-Module .\LocalPasswordSpray.ps1</pre>
- We will use "Winter 2020" for our password spray with this command:
<pre>Invoke-LocalPasswordSpray -Password Winter2020</pre>
<img width="767" alt="Screenshot 2025-03-29 at 11 02 01 PM" src="https://github.com/user-attachments/assets/9093544e-c62b-437b-a343-ba9361b9245c" /> <br>
- There are 6 successful authentication attempts (it doesnt have to be Frank's account, there just needs to be an attempt)
- We can exit with ```exit``` and cleanup with ```user-remove.bat ```
- Finally, let's check for alerts in Event Viewer by going to Action > Refresh.
<img width="919" alt="Screenshot 2025-03-29 at 11 05 48 PM" src="https://github.com/user-attachments/assets/788ca2c1-d2e5-491b-9c7e-397c695d1084" /><br><br>
<a href="https://github.com/swathinator/Homelabs">Back to Homelabs</a>
