Foreword
========

gateway4labs is a pragmatic approach targeting the integration of multiple RLMSs
(Remote Laboratory Management Systems) in different digital learning
environments, such as Learning Management Systems (LMSs), Content Management
Systems (CMSs) or Personal Learning Environments (PLEs). There are few
principles:

1. Supporting a new LMS/CMS/PLE or LMS/CMS/PLE version must be simple and easy.

2. The solution must be secure. A student should never be able to open a lab
   session unles the LMS/CMS/PLE grants him access to it.

3. It must work with LMSs/CMSs/PLEs used by users, as opposed to only supporting
   future versions of LMSs/CMSs/PLEs with standards not yet implemented.

4. It must work with LMSs/CMSs/PLEs in a variety of situations, from universities
   supporting Single Sign-On solutions -such as `Shibboleth
   <http://shibboleth.net/>`_- or directory protocols -such as LDAP- to
   secondary schools with almost no IT infrastructure.

5. IT services of entities deploying gateway4labs must be able to audit quickly
   whatever involves the LMS/CMS/PLE.

6. It must work with multiple RLMSs, so they can collaborate towards the same
   shared goal. While some code must be RLMS-dependent, most of the code should
   be common and RLMS-independent.

Given that multiple LMSs/CMSs/PLEs are targeted, ideally there should be no
LMS/CMS/PLE dependent code. There are approaches that try to achieve this.
However:

* Some of them do not guarantee that any malicious user can open a lab session
  without the LMS/CMS/PLE supporting it. This is in conflict with principle
  number 2.

* Some of them rely on protocols not yet supported by existing LMSs/PLEs/CMSs,
  such as relying exclusively on Shibboleth or IMS LTI. This is in conflict with
  principles number 1 (if the LMS/CMS/PLE does not support it, including it becomes
  complex), 3 and 4 (if the secondary school does not support that protocol, the
  solution will not work).  Additionally, given that these protocols do not know
  what the LMS/CMS/PLE itself states, certain common situations are not covered. For
  instance, instructors may want to establish which weeks lab sessions are
  available and which ones are not.

Therefore, we accept that there is some LMS/CMS/PLE-dependent code as the lesser
of two evils, and only if it is required. However, so as to support the
principles mentioned above, this code:

* Should be as small and simple as possible: IT services must be able to audit
  it quickly.

* Should not require upgrades too often: that will typically involve critical,
  slow processes by the IT services.

Most of the logic should therefore be located in other component. This component
has been named *labmanager*, as detailed in the following section.

