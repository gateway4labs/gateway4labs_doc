##########################
LMS/CMS/PLE administration
##########################

The Labmanager offers two ways of interaction with the LMS/CMS/PLE.
One method uses the IMS LTI standard and the second is a custom communication schema
called Basic HTTP and relies on a separate module/block developed for each specific LMS/CMS/PLE.

In any case, you need to log in as a LMS administrator. So in the root of the LabManager, click on the link in the right at the front page:

.. image:: /_static/l4l_frontpage.png
   :width: 500px
   :align: center


And then, select which LMS you are administrating and use your credentials in that LMS.

.. image:: /_static/lms_admin_login.png
   :width: 500px
   :align: center


By clicking on Labs, you can see what permissions your LMS have. If you want to get more permissions, contact the LabManager administrator. 

.. image:: /_static/lms_admin_list_labs.png
   :width: 500px
   :align: center


And in the Users panel, you may create other users (administrators or instructors) for this LMS:

.. image:: /_static/lms_admin_create_user.png
   :width: 500px
   :align: center

*************
1. Basic HTTP
*************

In the case of Basic HTTP, we rely on **courses**: the LMS/CMS/PLE administrator
will need to add the target courses to the LabManager and grant permissions to
these courses. Then, when the student uses the plug-in in the LMS/CMS/PLE, this
plug-in will inform us whether the student is enrolled in the course or not, and
the LabManager will rely on this information to guarantee access or not.

So as to add these courses, the administrator may do this manually, or he may
use the discovery system (if implemented in the LMS/CMS/PLE). When clicking on
it, a list of courses provided by the LMS/CMS/PLE is provided, and the
administrator will register those targeted:

.. image:: /_static/lms_admin_discover.png
   :width: 500px
   :align: center

The other option is to do this manually:

.. image:: /_static/lms_admin_create_course.png
   :width: 500px
   :align: center

Once this is done, the LMS can already contact the LabManager requesting access
to laboratories. If the LMS supports SCORM, a custom SCORM package can be
downloaded from the Laboratory list.

**********
2. IMS LTI
**********

In an effort to promote tool interoperability, the IMS proposed an standard named
Learning Tool Interoperability (LTI) that is now supported by different LMS such
as Moodle (v2.2+), Sakai and Blackboard. Labmanager will act as an LTI tool provider
and allow an LMS to request access to experiments registered in the Labmanager.

Some of the benefits that the LTI alternative offers are:

* Use of OAuth v1.0 for authentication.
* No need for extra developments to work.
* No need for requirements in the LMS side (and therefore, IT services will not
  need to install anything).

LTI work-flow
=============

So as to use the LTI version, the **course** concept will not be used. Instead,
the LMS/CMS/PLE administrator will create *Instructor* users, such as:

.. image:: /_static/lms_admin_create_user.png
   :width: 500px
   :align: center

Once the user is created, you can grant permissions on them:

.. image:: /_static/lms_admin_create_permission_on_user.png
   :width: 500px
   :align: center

From this point, the LMS administrator will be able to see two self-generated
credentials for this user and laboratory:

.. image:: /_static/lms_admin_list_permissions.png
   :width: 500px
   :align: center

LMS administrator may now communicate to these instructors what are these credentials.
Once done, these instructors will be able to use these pairs of credentials in
their courses in the LMS/CMS/PLEs.
