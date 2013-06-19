Usage: Moodle
~~~~~~~~~~~~~


**********
1. IMS LTI
**********

Once the Moodle Administrator added a Lab Manager as an external tool, it can be added to
the courses.

You need to go into the course and click the "*Turn editing on*" button on the
top right.

Then click on the "Add an activity or resource" on the section of the course
where the laboratory will be used. Select the "External Tool" option and click
the "Add" button.

.. image:: /_static/moodle_2_3_lti_add_to_course.png
   :align: center
   :width: 500px

Fill out the form and select the Lab Manager installation you want to add in
the "External tool type" field. Notice that the options listed here are the
names of the Lab Manager installations you added previously. So adding a it is
always better to add a descriptive name when adding the Lab Manager tool.

You need to show the advanced features, and then fill the consumer key and the
secret as the LMS Administrator has detailed (there is one consumer key and
secret per instructor and laboratory).

You may leave the "Launch URL" blank, since the one from the selected tool will
be used.

.. image:: /_static/instructor_lms_lti.png
   :align: center
   :width: 500px

Click the "Save and return to course" button and you should see the activity
in the section of the course. If you click it, it will go to the Lab Manager
and ask for the laboratory.


****************
2. SCORM Package
****************
A teacher needs a SCORM object per laboratory. So as to gather it, the LMS
administrator needs to provide the SCORM object to the teacher. The teacher can
optionally modify it (adding laboratory information, course information, etc.).
Then, the teacher can upload it as a SCORM object to a particular week, make it
visible for students, etc.

So, granted that the LMS administrator has sent a SCORM object to the teacher:

.. image:: /_static/moodle_authentication.png
   :width: 500px
   :align: center

.. image:: /_static/moodle2_3_upload_scorm.png
   :width: 500px
   :align: center

From that point, the SCORM object is just another SCORM object:

.. image:: /_static/moodle2_3_use_laboratory1.png
   :width: 500px
   :align: center

And whenever a student enrolled in that course opens the SCORM object, a
reservation will be performed, and the student can open the reservation:

.. image:: /_static/moodle2_3_use_laboratory2.png
   :width: 500px
   :align: center

.. image:: /_static/moodle2_3_use_laboratory3.png
   :width: 500px
   :align: center


