Design overview
===============

Principles and decisions
~~~~~~~~~~~~~~~~~~~~~~~~

There are few principles:

1. Supporting a Learning Tool must be simple and easy.

2. The solution must be secure. A student should never be able to open a lab
   session unless the Learning Tool grants him access to it or unless the lab
   provides open access to it.

3. It must work with Learning Tools in a variety of situations, from universities
   supporting Single Sign-On solutions -such as `Shibboleth
   <http://shibboleth.net/>`_- or directory protocols -such as LDAP- to
   secondary schools with almost no IT infrastructure.

4. IT services of entities deploying gateway4labs must be able to audit quickly
   whatever involves the Learning Tools.

5. It must support multiple remote laboratories, so they can collaborate towards 
   the same shared goal. While some code must be remote laboratory dependent,
   most of the code should be common.

Given that multiple Learning Tools are targeted, ideally there should be no
Learning Tool dependent code. There are approaches that try to achieve this.
However:

* Some of them do not guarantee that any malicious user can open a lab session
  without the Learning Tool supporting it. This is in conflict with principle
  number 2.

* Some of them rely on protocols not yet supported by existing Learning Tools,
  such as relying exclusively on Shibboleth or IMS LTI. This is in conflict with
  principles number 1 (if the Learning Tool does not support it, including it becomes
  complex), 2 and 3 (if the secondary school does not support that protocol, the
  solution will not work).  Additionally, given that these protocols do not know
  what the Learning Tool itself states, certain common situations are not covered. For
  instance, instructors may want to establish which weeks lab sessions are
  available and which ones are not.

Therefore, we accept that there is some Learning Tool dependent code as the lesser
of two evils, and only if it is required. However, so as to support the
principles mentioned above, this code:

* Should be as small and simple as possible: IT services must be able to audit
  it quickly.

* Should not require upgrades too often: that will typically involve critical,
  slow processes by the IT services.

Most of the logic should therefore be located in other component. This component
has been named *labmanager*, as detailed in the following section.


Roles
~~~~~

In gateway4labs there are the following roles:

#. Remote laboratory administrator
#. LabManager administrator
#. LMS/CMS/PLE administrator
#. Teacher
#. Student

The remote laboratory administrator will create an account for each LabManager
involved, and it will grant privileges for each LabManager.

The LabManager administrator will interact with the remote laboratory
administrators to make sure that they are connected to the LabManager. He will
also sign up different Learning Management Systems from different entities.

The LMS/CMS/PLE administrator will manage from the LMS/CMS/PLE to students. There are two
versions at this moment:
* When using LTI, the LMS/CMS/PLE administrator will create teacher users in the LabManager,
  and assign them permissions on laboratories. Teachers will use these
  permissions (which contain a key and a secret unique for each teacher and
  laboratory) to add those labs to their courses. Students of those courses will
  automatically be able to use these laboratories.
* When using Basic HTTP, the LMS administrator will query courses in the
  LMS/CMS/PLE, and they will assign permissions to those courses. From that
  point, teachers will be able to upload SCORM objects refering to those courses
  and upload them to the LMS/CMS/PLE. From that point, students of those courses
  will be able to use them.

Architecture overview
~~~~~~~~~~~~~~~~~~~~~

.. image:: /_static/general_architecture.png
   :width: 500px
   :align: center

As described in the figure above, there are three main components involved:

#. The LMS/CMS/PLE (left side). If it supports IMS LTI, it will use it and no
   code will be required in the LMS/CMS/PLE. If it does not support it, it will
   have a small plug-in that communicates with the LabManager.

#. The LabManager, which will receive requests from multiple, different LMSs and
   it will understand the protocols of different RLMSs. It does not have any
   LMS dependent code, but it has RLMS dependent plug-ins.

#. The RLMS, which will support a federation protocol to process requests from
   the LabManager. The federation protocol from one RLMS to other will be
   different. It should not require anything special for being supported by the
   LabManager.

This way, if a new LMS/CMS/PLE is aimed, if it supports IMS LTI the support is
automatic. If it does not support it, a new plug-in for that LMS is required in the
LMS, but it has no impact on the rest of the RLMSs neither on the LabManager. If
a new RLMS is aimed, a new plug-in for that RLMS is required in the LabManager,
but it has no impact on the LMSs/CMSs/PLEs.

.. 
    Let's detail a typical scenario. *University A* uses Moodle (LMS), WebLab-Deusto
    (RLMS 1) and MIT iLabs (RLMS 2). They will deploy a LabManager in
    *labmanager.universitya.edu*.

    Then, they will install the gateway4labs plug-in for Moodle in their Moodle system.
    While installing the plug-in, they will have to configure three arguments:

    #. LabManager URL, pointing to the Lab Manager. Example:
       *http://labmanager.universitya.edu/gateway4labs/*
    #. LabManager credentials, which will be used by the LabManager to
       identify itself in the LabManager. Example: 'lm_uniA' and password:
       'imthelabmanager'.
    #. LMS username and password, which will be used by the LMS to identify itself
       in the LabManager. Example: 'lms_uniA' and password: 'imthelms'.

    From this point, the LabManager can grant permissions on the RLMSs to the LMSs,
    detailing which LMS can use which laboratories from which RLMS, customizing the
    permissions. For instance, the RLMS may grant the credentials used by the
    LabManager to access for half an hour to a laboratory. However, the LabManager
    can customize that a particular LMS can access only for half an hour while other
    can access for twenty minutes. This customization is particular of each
    particular RLMS, but the key idea is that the reservations are managed by the
    LabManager with the RLMS, not by the LMS with the RLMS.

    .. image:: /_static/labmanager_rlms_lms.png
       :align: center

    Once a LMS has permissions to use certain RLMSs through the LabManager, the LMS
    can access the LabManager and select which courses are used in the LMS. In order
    to do this, the LabManager will query a web service provided by the gateway4labs
    plug-in for Moodle. The plug-in will return the list of courses created in 
    moodle.

    .. image:: /_static/labmanager_lms_courses.png
       :align: center

    To each of these particular courses, the LMS administrator will be able to grant
    and revoke permissions to those laboratories granted to the LMS. This way, the
    LMS administrator can define that only the students of electronics can use an
    electronics laboratory, while only the robotics classes can access the robotics
    laboratories. Additionally, once again the LMS administrator can customize the
    permissions of these classes. For instance, there could be 2 electronics
    classes. The first class may be granted 20 minutes to a particular laboratory
    while the other class is granted only 10 minutes but with a higher priority.

    At this point, all the permissions and registrations have been stored. To sum
    up:

    #. The LabManager has configured the RLMS.
    #. The LabManager has registered the LMS.
    #. The LMS has registered the LabManager.
    #. The LabManager has registered which courses are in the LMS.
    #. The LabManager has registered which courses of the LMS can access which
       laboratories in which RLMSs.

    Finally, the last layer is the consumption of the RLMS by the final user. So as
    to do this, a small JavaScript library has been written which can be attached to
    plain HTML files uploaded to the LMS or to SCORM objects. An examples of usage
    of this JavaScript would be::

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <script src="gateway4labs.js" type="text/javascript"></script>

            <script>
                function startLab() {
                   // Create an instance of the laboratory. By default, it uses "/". You can
                   // pass other path, such as "/fake_lms/" in the example.
                   var lab = new Laboratory("/moodle/blocks/"); 

                   // Load the experiment "robot".
                   lab.load("robot");
                   // Authenticate as a LMS administrator (if it is a LMS administrator) in the 
                   // Lab manager
        //           lab.authenticate();
                }
            </script>
        </head>
        <body onload="javascript:startLab();">
            <div id="gateway4labs_root"></div>
        </body>
        </html>

    In this case, the *load("robot")* method will call the gateway4labs Moodle plug-in,
    requesting a reservation for the laboratory identified by *'robot'*. The
    gateway4labs plug-in will check who is the user (he must be logged in) and send the
    user and the courses where the user is enrolled to the LabManager. The
    LabManager will check what is that identifier for that LMS (e.g. *'robot'* is
    the *robot@Robot experiments* laboratory of the WebLab-Deusto deployed in the
    University of Deusto), and if the student can access that laboratory through the
    courses where he is enrolled. If the student has permissions, then the
    LabManager will perform the request to the RLMS, and will forward the
    reservation to the LMS. There, the JavaScript library will load the laboratory:

    .. image:: /_static/gateway4labs_lms.png
       :width: 500px
       :align: center

    To sum up the interactions:

    #. The LabManager has a plug-in for each RLMS which interacts with the RLMS.
    #. The LabManager contacts the LMS with a generic API. This API is implemented
       by the gateway4labs plug-in of the LMS (e.g. a Moodle plug-in). It uses it to
       retrieve the list of courses.
    #. The LMS contacts the LabManager to perform a reservation request.
    #. The LMS contacts the LabManager to perform an authentication request: the LMS
       knows who is an administrator of the LMS, and can contact the LabManager
       providing the LMS credentials to say "I have one user called 'John' who is
       an administrator and who wants to open the LabManager administration panel
       for this LMS".

LMS to LabManager protocol
~~~~~~~~~~~~~~~~~~~~~~~~~~

This only applies when the non IMS LTI version is targeted. Sample reservation request::

    POST /gateway4labs/labmanager/requests/ HTTP/1.0
    Authorization: Basic ASDFASDF (LMS token)

    {
       "user-id"    : "jsmith",
       "full-name"  : "John Smith",
       "is-admin"   : true, 
       "user-agent" : "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:12.0) Gecko/20100101 Firefox/12.0",
       "origin-ip"  : "192.168.1.1",
       "referer"    : "http://.../", 
       "courses"    : {
            "01"    : "s",
            "02"    : "s",
            "03"    : "t", // "t" = teacher, "s" = student
            "04"    : "s", 
       },
       "request-payload" : "SOMETHING-THAT-SCORM-SENDS"
    }

Sample authentication request::

    GET /gateway4labs/lms/authenticate HTTP/1.0

    POST /gateway4labs/labmanager/lms/admin/authenticate/ HTTP/1.0
    Authorization: Basic ASDFASDF (LMS token)

    {
        "full-name" : "John Smith"
    }

Sample course listing request (q=text to filter, start=0 to go to the first page)::

    GET /gateway4labs/lms/list?q=elect&start=0 HTTP/1.1
    Authorization: Basic ASDFASDF (LabManager token)

Sample course listing response::

    {
       "start"    :   150,
       "number"   : 34000,
       "per-page" :    10,
       "courses" : [

         {
            "id"   : "3465", 
            "name" : "Computers Architecture"
         },
         {
                    "id"   : "2854",
                    name"  : "Electronics Laboratory"
         },
         {
            "id"   : "2854", 
            "name" : "IEEE Student Branch"
         },
       ],
    }

