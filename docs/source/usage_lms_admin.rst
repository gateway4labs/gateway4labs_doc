Usage: Moodle administrator
===========================

Since Moodle 2.x supports the `IMS LTI 1.1.1 standard <http://www.imsglobal.org/LTI/>`_
you just need to add an external tool:

.. image:: /_static/moodle_2_3_lti_external_tool.png
   :align: center

Here, you can add a Lab Manager installation, you will need a
**consumer key** and a **shared secret** from the Lab Manager administrator.
Fill in the form and save the external tool.

.. image:: /_static/moodle_2_3_lti_save_external_tool.png
   :align: center
   :width: 500px

.. note::

  You could add as many different Lab Manager installations as you
  want as long as you have the consumer and secret keys. This will allow you to
  access different laboratories on different universities each of them with a
  different Lab Manager installation.

Adding a laboratory to a course
--------------------------------

Now that you have added a Lab Manager as an external tool, it can be added to
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

You may leave the "Launch URL" blank, since the one from the selected tool will
be used.

.. image:: /_static/moodle_2_3_lti_add_to_course_form.png
   :align: center
   :width: 500px

Click the "Save and return to course" button and you should see the activity
in the section of the course. If you click it, it will go to the Lab Manager
and ask for the laboratory.

.. warning::

  TODO: Finish this. How are we going to manage the first launch? -NHI