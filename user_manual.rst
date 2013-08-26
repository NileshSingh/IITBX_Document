User Manual
===========

CMS user manual
---------------
	**Link for CMS documentation**
		http://help.edge.edx.org/kb/beta-users/edx-studio-documentation

	**CodeJailConfiguration**

		Unsafe code cannot be allowed to run on a server otherwise the hackers may run malicious codes to cripple the server. Codejail 			basically provides the facility of running unsafe code in secured sandboxes.
		By default the Codejail is configured for Python code execution but with little modification it can be configured to execute 			code in any language.
		The security is imposed with the aid of AppArmor but if the Operating System does not support AppArmor it won't impose any 			security measures.
				
	**Configuration:**
	
		- Create a new virtual environment alongside the main project’s virtual environment but the name of the virtual environment 			being appended with “-sandbiox”.		
		**$ sudovirtualenv<SANDENV>**								
		If virtual environment wrapper is installed use 
		**$ mkvirtualenv<SANDENV>**
		e.g. mkvirtualenvmooc-edx

		-  If some specific packages need to be made available to the sandbox install them in the virtual environment.
		**$ source <SANDENV>/bin/activate**
		**$ sudo pip install -r sandbox-requirements.txt**

		- If wrapper is installed then
		**$ workon<SANDENV>**
		**$ sudo pip install -r sandbox-requirements.txt**
		
		- Add the user sandbox- the under priviledged user who actually executes the code in the sandbox.
		**$ sudoaddgroup sandbox**
		**$ sudoadduser --disabled-login sandbox --ingroup sandbox**

		- Let the web server run the sandboxed Python as Sandbox. Create the file /etc/sudoers.d/01-sandbox using
		$ visudo -f /etc/sudoers.d/01-sandbox
		**<WWWUSER> ALL=(sandbox) NOPASSWD:<SANDENV>/bin/python**
		**<WWWUSER> ALL=(ALL) NOPASSWD:/usr/bin/pkill**
	
		Note: <WWWUSER> is the user running the LMS

		- Edit an AppArmor profile. This is a text file specifying the limits on the sandboxed Python executable. The file must be in 			  etc/apparmor.d and must be named based on the executable, with slashes replaced by dots. For example, if your sandboxed 			  Python is at /home/el3ktr0n/.virtualenvs/mooc-sandbox/bin/python, then your AppArmor profile must be /etc/apparmor.d/	
	          home.el3ktr0n..virtualenvs.mooc-sandbox.bin.python:

		
		$ sudo vim 
		/etc/apparmor.d/home.el3ktr0n..virtualenvs.mooc-sandbox.bin.python

		#include <tunables/global>

		<SANDENV>/bin/python {
   		#include <abstractions/base>
   		#include <abstractions/python>

		<SANDENV>/** mr,
   		# If you have code that the sandbox must be able to access, add lines
  		 # pointing to those directories:
   		/the/path/to/your/sandbox-packages/** r,

		/tmp/codejail-*/ rix,
   		/tmp/codejail-*/** rix,
		}

		- Parse the profile
		$ sudoapparmor_parser<APPARMOR_FILE>
		- Reactivate the main project’s virtual environment.

	**Integration into Edx:**

		- Open the file ~/edx_all/edx-platform/lms/envs/common.py
		- Set 'ENABLE_DEBUG_RUN_PYTHON' to True
		- Find the “Python Sandbox” section and make the following changes:
		
			- Provide the path to the python library of <SANDENV> in python_bin(e.g. python_bin: ‘/home/el3ktr0n/.virtualenvs/mooc-
			  sandbox/bin/python’) 
			- Provide the course ids as the regular expressions for which you want to allow unsafe code execution.

	**Email Integration**

		The IITBX platform has to send e-mails to users for registration-activation, for changing user’s password and to notify about 			various course deadlinesupdates etc.

		For the platform, we use the mail server of IIT Bombay. The settings for the same can be found in common.py files in the 			‘envs’ folder for the respective runtime (cmsor lms).
		This document will guide you through the process of configuring the mailing settings.

	**To change the IITBX studio mailing  settings:**

		- Change your directory to   ~/edx_all/edx-platform/cms/envs
		- Open the file common.py  .
		- Jump to the part which looks like this.

		- Change the above env variables to the values you wish.
		- Note the  EMAIL_HOST, EMAIL_PORT and  EMAIL_USE_TLS  should remain the same unless you want to change the smtpserver.These 			  are settings for the smtpserver.Once the site is live , the smtp server you change to is working , users will not receive 			  any mail .

		- If the you want the emails to appear on the console , then change the EMAIL_BACKEND variable to 
      		  django.core.mail.backends.console.EmailBackend .With this setting ,mails will not be sent to the user ,instead will appear
                  on the console ,on which the server is running.

		- Change the DEFAULT_FROM_EMAIL to whatever from address you want the user to see.It need not be a valid email address.But if 			  it is not ,better let the user know that is a no-reply address.(Let the name be something like no-reply@iitbx.org).There is 			  another downside if you use a unregistered domain name like iitbx.org ,then most likely the mails will go into the users 			  spam mail.
		
		- SERVER_EMAIL - This is used as the from address for mails to the admin when the server crashes.
		  The admins variable will be used for mailing all the admins at one go. List email addresses of all the admins in here.
		- See that all mails which you expect the user to reply back to should be valid email addresses. 


	**To change the IITBX LMS  mailing  settings:**

		- Change your directory to    ~/edx_all/edx-platform/lms/envs
		- Open the file common.py.
		- Follow the steps we did for the studio mailing settings.

	**To change the content of the emails sent to user :**
	
		- For LMS:
			- Change your directory to  ~/edx_all/edx-platform/lms/templates/emails
			- Use a text-editor to change the concerned email text.

		- For IITBX studio:
			- Change your directory to  ~/edx_all/edx-platform/cms/templates/emails
			- Use a text-editor to change the concerned email text.


	**Discussion Forum**
		- Ruby Installation
			- http://blog.coolaj86.com/articles/installing­ruby­on­ubuntu­12­04.html
			- Visit the above link to install ruby­rvm
			- CS_COMMENT_SERVICE
			- Installcs_comment_service
			- Requirements:Successfullyinstalledruby-rvm& ruby1.9.3.Fullyfunctional edx-platform.
			- InstallElasticSearchfordebugging
		- wget--http-user=$http_user--http-password=$http_password
		  https://download.elasticsearch.org/elasticsearch/elasticsearch/elasticsearch-0.90.1.deb
		  Replace$http_userwithyourldapidand$http_passwordwithyourldappassword

		- sudodpkg –i elasticsearch-0.90.1.deb
		- sudoserviceelasticsearchstart
		- workonedx-platform
		- cd$HOME/edx_all/
		- git clone https://github.com/edx/cs_comments_service.git
		- cdcs_comments_service/
		- rvmuse1.9.3@cs_comments_service--create
		- bundleinstall
		- bundleexecrakedb:init
		- bundleexecrakedb:seed

		ThenenteryourAPIkeyinconfig/application.ymlfile(Arandomkeysay
		“0u3ru93u398rq3083u0u83”).Enterthesamekeyinedx-platform/lms/envs/dev.py
		tothevariableCOMMENTS_SERVICE_KEY="PUT_YOUR_API_KEY_HERE"
		To run the discussion forum
		- rubyapp.rb

LMS user manual
---------------
**Introduction**

Learning Management System is a part of IITBX platform. IITBX is a massive open on-line course platform created 
by modifying the existing edX platform
**Purpose**
The main purpose of this document is “how to use IITBX MOOC website LMS to utilize world class video lectures, reading 			materials and quizzes.”

**How to use Learning Management System of IITBX website**
- Requirements
- He need to have any of the System (PC, Laptop etc.)
- Internet Facility needed.
- IITBX account is necessary to register courses.
- Registration of course is necessary to use course resources.

**Registration for IITBX account**
- Open www.iitbx.org website to create an account.
- When you open the website it looks as below except red mark.	
- Click the REGISTER NOW button to create an account at IITBx website to get access to IITBX resources.

click  to register

.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/usermanual_image/usermanual_registration.png
Fig.

- When you click on the REGISTER NOW button, you will get a page like shown in 

**Registration Page**
- Registration page to create an account.

**Instructions**
- Enter a valid email address because it will send an activation email to your email account.
- Enter correct details and check the I agree to the Terms of Service and I agree to the Honor Code to continue.
- Click on create my iitbx account so you get an activation link to your entered email
- Then you will get a message saying thanks for registering
- The new page displayed like this

.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/usermanual_image/instruction.png
Fig.

**Finding Course**
- To see what are the course available click on Find Courses now.
- Then new will be displayed like this.
Fig.
- You can search course in the search box and then click submit Query.
- So it displays all related courses.

**Registering a Course**
- Click on the course you are interested.
Fig.
- After clicking on the course you will get a page asking to register that course.
Fig.
- Click on REGISTER FOR IAP2013 (here )	
- Then you are registered the course.
- To view the course Just Click on View Course.
Fig.
- When you Click on view course to view videos, reading materials and quizsetc
- The page looks like this
Fig.
**Accessing Course Contents**
Here click on Course info  or It is default which shows any update news and information about the course
Click  on Courseware to view all videos, reading materials etc
When we click on Courseware it shows the sections of course as week1, week2 and so on.
And The one that you recently used.
Click on week1 to get week1 material.
To get the corresponding things click on its subsections
e.g. Introduction to Android Programming here
Fig.
- Then it shows the units it have e.g. here video
Fig.
**Multiple Choice Questions**
- Click on the option to give your answer
- Then click on check to check your answer
Fig.
- Click on Show Answer to see the explanation of the answer

**Usage of Buttons on the bar**

- When we click on below things the first red mark it will give the video.
- The second marked one gives the Discussion forum.
Fig.
**Multiple components in the same unit**
- For example, a unit can have one or more components i.e. quiz, video and reading material components 
  can be displayed in same unit.
Fig.

**To go to profile**
- First login to your account
- click on this on top-left corner of page (home button)
- To go to your profile just click the button which looks like this

**To change password and full name and Email**

- click on reset password (for password change)
- click on edit for changing name or email
- When you click on Reset password a new pop up kind of a thing appears showing some information
- Then check your email and follow the steps in the email

Fig.
Fig.

**Logout**
Fig.

**Help, Contact, Team**
- See the bottom of the page which looks like this
Fig.

**FAQ**
Fig.

**About page**
- When you click on about it will display a page like this
- It gives information about the IITBX
Fig.

**Conact page**
- When you click on the contact page you will get this page
- You can use the emails to contact respective person
Fig.

Bibliography
============
https://github.com/edx
https://docs.djangoproject.com
http://docs.python.org
http://docs.mongodb.org/manual/






	

	
	
	

















































