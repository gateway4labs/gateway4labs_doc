############################
How to connect to Labmanager
############################

Labmanager offers two ways of interaction with Learning Management Systems (LMS).
One method uses the IMS LTI standard and the second is a custom communication schema
that uses SCORM packages and relies on a separate module/block developed for each
specific LMS.

****************
1. SCORM Package
****************

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

LTI work-flow
=============
Three main actors appear in a basic configuration of a tool for an LMS, a Labmanager
administrator (*LabAdmin*), an LMS administrator (*LMSAdmin*) and the *Instructor*.

**1.** A *LabAdmin* creates an account for the LMS and provides the *LMSAdmin* with a URL
and a pair of OAuth Consumer Key and secret.
* The *LabAdmin* will also grant access this LMS access to the experiments.


**2.** *LMSAdmin* creates a General tool. This steps varies depending on the LMS, but will
normally require and administrator to provide custom parameters about launching the
tool. Labmanager only requires the OAuth credentials.


**3.** The *Instructor* adds the LTI tool as an activity or resource and selects the desired
tool provider (in case of having more than one Labmanager).


**4.** The *Instructor* needs to request access to the experiments. A list of available
experiments is available when launching the tool.

.. note::
        Access to experiments from the Labmanager is given course-wide.
        If an Instructor wants to have access to the same laboratory from
        another course, is necessary to request access from that course.


**5.** *LMSAdmin* has to access the Labmanager to Grant or Deny the *Instructors*'s access
requests to the laboratories.
