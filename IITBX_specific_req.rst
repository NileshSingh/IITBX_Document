Specific Requirements
=====================



**External Interface Requirements**

- Login interface

.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/login_interface.png
Fig.


- Registration interface
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/registration_interface.png
Fig.

- User Dashboard
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/User_Dashboard.png
Fig.	

- Courseware interface
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/courseware_interface.png
Fig.

- Wiki-edit interface
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/wiki_edit_inter.png
Fig.

- Wiki-view interface
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/wiki_view.png
Fig.

- Edit information interface
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/edit_info_inter.png 
Fig.

**Functional Requirements**

**The functional requirements of LMS are as follows:**
- Sign up

The user can sign up on the website to enroll into a course.

- Course enrollment

The user can register for any course of interest which is currently going on or is scheduled for future. The
user may re-take IITBX courses as often as he/she wish. Each offering of a course is assessed independently. 					The user may unregister from an IITBX course at any time, there are absolutely no penalties associated with 					incomplete IITBX studies, and may register for the same course (provided we it is still offered) at a later 					time.

- View courseware

After enrolling into a course, user can see the ongoing activities in the course. The registered user can view 					lecture videos available for the course, solve problem sets, assignments etc.

- Downloadable videos

The registered user can download the videos in many formats as available for the course.

- Take a quiz

The registered user can take up the quiz as available for the course.

- Discussion forum

The registered user can use this forum to connect with fellow students, professors and teaching assistants.
Also he/she can search for a particular post, edit previous posts, like the comments/ posts by fellow members 					etc.

- View grades

Once the course is finished and grades are released the registered use can view his/her grades.
- Wiki-based collaborative learning
The registered user can wiki edit some of the contents (on the basis of the rights provided by the author), 					addarticles 
- Calendar based scheduling
Each course is scheduled i.e. it has a start and finish date. Few assignments have deadlines. All this is 					managed by the course instructor.
- Find Courses
The user can search for the courses according to the university or simply local search engine by using 					keywords.
- Progress report
The registered user can check his/her progress report on the basis of test assessments and assignment 					evaluation on the basis of homework, lab assignments, midterm &final exams with the help of graphs and 					numerical scores.
- Online test and assignments
The registered user can take tests and online assessments for the course for which he/she has registered.
- Video transcripts
The registered user can use the facility of video transcripts to skip parts of videos which he/she doesn’t 					want. He/she can also download the transcripts.
- Merge wiki-edit versions
The registered user can use this feature to merge concurrent wiki-edits.
			
**The functional requirements of CMS are the following:**
- Sign up and login (instructor)
				
This feature is the same as that in LMS feature 3.2.1
- New course

The registered instructor can create a new course in which he/she can specify the course name, course 					organization and course number. In the course he/she can create new sections and subsections, set the course 					release date or view the course live.

- Schedule course
				
The registered instructor can schedule the course by specifying the course start and end date, time and the 					enrollment start and end date time.

- Course overview

The registered instructor can provide the course overview of the course created by him in which he/she can 					specify course description, prerequisites, course-staff and other information.

- Grading
				
The registered instructor can define the grading rules and policies for the course authored by him/her.
- Create assignment

The registered instructor can define the type of assignment for e.g. homework, midterm exams etc., its 					weightage and the number of assignments.

- Add/delete instructors
			
The registered instructor can add/delete users to manage the course team.

- Course updates

The registered instructor can make announcements or notifications that he/she wants to share with the class. 					Other course authors can them for important exam/date reminders, change in schedules, and to call out any 					important steps students need to be aware of.

- Add static pages
		
The registered instructor can add static pages. Static Pages are additional pages that supplement courseware. 					Other course authors can use them to share a syllabus, calendar, handouts, and more.

- Import course
	
The registered instructor can import a course in gzippedformat (tar.gz) and must contain a minimum of 					course.xml file.

- Export a course

The registered instructor can export the course designed by him/her in gzipped format.

**Behavior requirements**
				
- Use case view

- User
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/user.png
Fig.


- Instructor use case
.. image::
  https://raw.github.com/NileshSingh/IITBX_Documentb/master/images/instructor_usecase.png
Fig.

- Activity diagrams
.. image::
  

- User registration

Initially user is made to fill all mandatory fields filled in registration form. Once the user clicks create 					an IITBX account, the username is verified. If the username is already present, then the user is again taken 					back, so that he can change the username. If the username is not present then it checks for password and 					remaining mandatory fields. If any of the mandatory field is left empty or filled incorrect, then the user is 					informed to enter the correct values. Once all these verifications are succeeded, then the registration is 					done and a confirmation mail is sent.
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/user_resgistration.png
Fig.

- User login activity

User is made to enter the username and password, and then entered values are verified. If it is a valid 				username and password, then the user is logged in, or else he/she is asked to re-enter the values.
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/user_login_activity.png
Fig.

- Find courses
.. image::
  https://raw.github.com/NileshSingh/IITBX_Document/master/images/find_course.png
Fig.

- Discussion forum activity
.. image::
https://raw.github.com/NileshSingh/IITBX_Document/master/images/discussion_forum_activity.png
Fig.

- Check progress activity
.. image::
https://raw.github.com/NileshSingh/IITBX_Document/master/images/check_progress_activity.png
Fig.

			











