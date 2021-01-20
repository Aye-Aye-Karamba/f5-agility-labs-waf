Lab 1.2: Credential Stuffing
----------------------------

..  |lab2-11| image:: images/lab2-11.png
        :width: 800px
..  |lab2-1| image:: images/lab2-1.png
        :width: 800px
..  |lab2-2| image:: images/lab2-2.png
        :width: 800px
..  |lab2-3| image:: images/lab2-3.png
        :width: 800px
..  |lab23-5| image:: images/lab23-5.png
        :width: 800px
..  |lab23-6| image:: images/lab23-6.png
        :width: 800px
..  |lab23-7| image:: images/lab23-7.png
        :width: 800px
..  |lab41-01| image:: images/lab41-01.png
        :width: 800px

Credential stuffing is a type of brute force attack that leverages stolen credentials from another source. This source is most commonly the breach of a widley used online service.  These leaked credentials are then levered in an attempt to compromise higher value targets in instances where users used the same credentials across multiple services. BIG-IP now has the capability to detect these types of attacks by employing a database of credentials that are known to have been compromised in a previous breach. The credentials are stored as one-way hashed usernames and passwords to protect them from further disclosure. Also note that we've chosen CAPTCHA as mitigation for this lab because it provides immediate feedback to the student.  In a production environment, Client Side Integrity Defense (or both), may be a more effective form of mitigation during an actual attack.  Feel free to experiment with this in the lab.




Task 1 - Configure Credential Stuffing Detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Open the BIG-IP GUI interface. 
    
#.  Navigate to **Security -> Application Security  -> Brute Force Attack Prevention**.

#.  Click on the /WebGoat/login configuration created earlier.

#.  Configure **Credential Stuffing** detection within the **Distributed Brute Force Protection** Section as follows:

    |lab2-11|

#.  Click **Save** .

    
#.  Click **Apply Policy**.


Task 2 - Test Credential Stuffing Detection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    
#.  Open a new Private Browsing window in **Firefox** .

#.  Go to the to WebGoat login page at ``https://insecureapp1.f5.demo/WebGoat/login`` 

#.  Attempt to login using the username ``demo33@fidnet.com`` and password ``mountainman01``.  On the second attempt, you should receive a CAPTCHA because this configured mitigation for credentials matching the credential stuffing database.


#.  Examine the most recent requests in the event log by navigating to Security -> Event Logs -> Applications -> Requests

    |lab2-1|

    Take note of the username field.  The request was matched as a potential credential stuffing attack.

#.  Near the **Brute force: Maximum Login Attempts are exceeded** header at the top of the event window click on the number under **Occurrences**:

    |lab2-2|

    The message indicates the number of login attempts that matched the internal database.

#.  Now check out the reporting under **Event Logs -> Application -> Brute Force Attacks**:

    |lab2-3|

#.  Click on one of the attack entries to get some more detail about the attack:

    |lab23-7|

#.  For fun, head over to ``https://haveibeenpwned.com/`` and put in the email address of the account we used in the lab to get some details.  It may also be interesting to put in your own account(s) to see if any of your credentials have been breached.  You could also try some of your old username/password combinations against the credential stuffing database on the F5.  While on the main page explore some of the breach data on the bottom to get a sense of how big this problem is.

   

#.  In order to release any blocking that's currently in place, navigate to **Security -> Application Security -> Brute Force Attack Prevention** and **Delete** the Brute Force configuration we created previously.

#. Click **Apply Policy** .

#.  Navigate to **Local Traffic > Virtual Servers > Virtual Server List > insecureApp1_vs > Security > Policies** and ensure that the **insecureApp1_asmpolicy** policy and the **Log All requests** log profile are enabled on the **insecureApp1_vs** virtual server as shown below removing the **Bot Profile**.

    |lab41-01|



|
|


**This concludes Lab 1.2**

