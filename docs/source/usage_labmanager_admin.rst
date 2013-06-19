Usage: LabManager administrator
===============================

The LabManager administrator can do three different things: administrating which
remote laboratories are available from it, administrating which LMSs can access
it, and assigning remote laboratories to each LMS.

So as to enter in the LabManager, click on the link in the middle in the front page:

.. image:: /_static/l4l_frontpage.png
   :width: 500px
   :align: center

And then log in as a LabManager administrator (default credentials: *admin* as
username and *password* as password).

.. image:: /_static/labmanager_login.png
   :width: 500px
   :align: center
   

RLMS Administration
~~~~~~~~~~~~~~~~~~~

In the LabManager, you will configure the connection of the LabManager with the
different RLMSs. In the following example, three RLMSs have been deployed:
one WebLab-Deusto, one FCEIA-UNR and one MIT iLabs (support under development).

.. image:: /_static/labmanager_rlms.png
   :width: 500px
   :align: center

You may add more. For example, if you deploy a new WebLab-Deusto instance in
your institution (or you have created one hosted in Deusto by the `wCloud system
<https://cloud.weblab.deusto.es/>`_), you may add it. So as to do this, complete
the following form by clicking on *Create*:

.. image:: /_static/labmanager_create_rlms.png
   :width: 500px
   :align: center

Once you've done this, you may want to register some laboratories. So as to do
this, in the list of RLMSs click on ``list``. You will see the following screen,
listing the laboratories available in that RLMS and which ones are registered in
the LabManager. You will be able to grant permission to LMS/CMS/PLEs only on
those registered laboratories. So select the ones you want to use, and click on
the register button.

.. image:: /_static/labmanager_admin_external_labs.png
   :width: 500px
   :align: center

From this point, you will be able to see (or remove) the registered labs in the
proper panel:

.. image:: /_static/labmanager_admin_registered_labs.png
   :width: 500px
   :align: center


LMS Administration
~~~~~~~~~~~~~~~~~~

The LabManager administrator can also add LMSs/CMSs/PLEs so they can use this
LabManager. The LabManager distinguishes among two types of LMSs/CMSs/PLEs:
those supporting IMS LTI and those who do not support it. If IMS LTI is
supported, this approach highly recommended. The rest will require a plug-in to
be installed in the LMS/CMS/PLE.

So as to add a LMS, you have to go to the LMS management side and create a new
LMS. When creating it, in the case of using the Basic HTTP approach (as opposed
to the IMS LTI approach), you will need to add credentials. These include: LMS
login (the username that the LMS will use in the LabManager), LMS password (the
password used by the LMS in the LabManager), the LMS URL (pointing to the
lms4labs/list method), and the username and password of the LabManager in the
LMS. The URL will be a URL pointing to the listing service. For
instance, in Moodle, it will point to something like:

   http://localhost/lms/moodle/2.3/blocks/lms4labs/lms/list.php


.. image:: /_static/labmanager_admin_lms_list.png
   :width: 500px
   :align: center

.. image:: /_static/labmanager_admin_add_lms.png
   :width: 500px
   :align: center

After this, you can configure which permissions this LMS will have. For example,
you may configure that it only has permission to a subset of the laboratories.
When adding these permissions, you will define a unique identifier for that
laboratory in that LMS/CMS/PLE.

.. image:: /_static/labmanager_admin_add_lms_permission.png
   :width: 500px
   :align: center


Finally, the LabManager can create different LMS users, identifying who is
administrating each LMS. From this point, you can contact the LMS administrator
and give them these credentials.

.. image:: /_static/labmanager_admin_add_lms_user.png
   :width: 500px
   :align: center


