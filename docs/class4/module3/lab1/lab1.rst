Lab 3.1: DAST Integration
-------------------------

..  |lab31-01| image:: images/lab31-01.png
        :width: 800px
..  |lab31-02| image:: images/lab31-02.png
        :width: 800px
..  |lab31-03| image:: images/lab31-03.png
        :width: 800px
..  |lab31-04| image:: images/lab31-04.png
        :width: 800px
..  |lab31-05| image:: images/lab31-05.png
        :width: 800px
..  |lab31-06| image:: images/lab31-06.png
        :width: 800px
..  |lab31-07| image:: images/lab31-07.png
        :width: 800px
..  |lab31-08| image:: images/lab31-08.png
        :width: 800px
..  |lab31-09| image:: images/lab31-09.png
        :width: 800px
..  |lab31-10| image:: images/lab31-10.png
        :width: 800px
..  |lab31-11| image:: images/lab31-11.png
        :width: 800px
..  |lab31-12| image:: images/lab31-12.png
        :width: 800px
..  |lab31-13| image:: images/lab31-13.png
        :width: 800px
..  |lab31-14| image:: images/lab31-14.png
        :width: 800px
..  |lab31-15| image:: images/lab31-15.png
        :width: 800px

ASM's DAST (Dynamic Application Security Testing) integration allows you to take the programmatic output from a vulnerability scan and use it to seed a security policy.  For this lab, we'll use output from WhiteHat's Sentinel(TM) product to create a security policy based on Sentinel's findings.



Task 1 - Create a Security Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Open Chrome and navigate to the BIG-IP management interface.  For the purposes of this lab you can find it at ``https://10.1.10.245/`` or by clicking on the **bigip01** shortcut in Chrome.

#.  Login to the BIG-IP.

#.  Create a new ASM policy by navigating to **Security -> Application Security -> Security policies**.

#.  Click **Create**, fill in the page as follows, and then click **save** as shown below.

        |lab31-01|
        |lab31-15|

#.  Once the policy is created, go to **Security -> Application Security -> Vulnerability Assessments -> Settings**.

#.  Select **WhiteHat Sentinel (US server)** from the dropdown list, then click **ok**.  **Do not** click save.

        |lab31-02|

    .. NOTE:: It's worth mentioning that ASM and Sentinel have more advanced integrations that we will not explore here, for this reason the Site Name and API Key are not used. This is mostly due to the logistics of procuring Sentinel accounts for all students attending this lab. This additional functionality provides an API key will allow you to pull in scan data directly from Sentinel into ASM as well as share ASM site mapping data back to Sentinel in order to improve scanning capabilities.

Task 2 - Import the Scan Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Select the **Vulnerabilities** tab at the top:

        |lab31-03|

#.  **Click** the **import** button:

        |lab31-04|

#.  Import the **webgoat.xml** file from **/home/f5student/WAF241** .

        |lab31-05|

#.  Ensure that the webgoat.f5 domain is selected and click **import** once more.

        |lab31-06|

#.  You should see a confirmation like the one below.  Click **close**.

        |lab31-13|

#.  You'll then be greeted by a list of vulnerability types and an indication of whether or not they are automatically resolvable by ASM:

        |lab31-07|

    .. NOTE:: Many of the vulnerabilities marked as not resolvable may yet be resolvable by ASM, but not automatically.

|

#. Under the view option, select Resolvable to hide vulnerabilities beyond the scope of this lab.

        |lab31-14|

#. Select **SQL Injection** from the bottom then click on the first **Vulnerability ID**. You'll be shown more details about the specific vulnerability such as the relevant URL and Parameter where the vulnerability is present (as in this case).

        |lab31-08|



Task 3 - Remediate some Vulnerabilities
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Select the checkbox at the top to select all of the SQL injection vulnerabilities and click **resolve**.  Note that there are a number of other options including "Resolve and Stage" which would put the changes into staging for further evaluation.

        |lab31-09|

#.  ASM then provides a list of the changes it's about to make.  Review the changes and click **resolve**.

        |lab31-10|

#.  You'll notice that the vulnerabilities you selected are now marked mitigated.

        |lab31-11|


Task 4 - Review the Output
~~~~~~~~~~~~~~~~~~~~~~~~~~

#.  Now navigate to **Security -> Application Security -> URLs -> Allowed URLs -> Allowed HTTP URLs** and you'll see that the ASM policy has been populated for you.

        |lab31-12|


#.  Now return to the Vulnerabilities dialog and explore some of the other items if you wish.  **Hint:** You can utilize **Tree View** under **Security -> Application Security -> Advanced Settings -> Tree View** to get a summary of what's in the policy.  Be sure you've selected the correct security policy in the dropdown.


    .. NOTE::  Data from a vulnerability scan can be a great way to get an ASM policy up and running quickly but you should consider that there may be vulnerabilities in the application beyond the reach of the scanner.  It is therefore a good idea in many instances to enable the Automatic Policy Builder after policy creation to help refine the policy and tighten security over time.

|
|

**This concludes module 3.**
