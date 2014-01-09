.. _toctree-directive:

REST API for RLMS
=================

Right now, different RLMSs require a plugin written in Python so that the RLMS can be used by the LabManager. In this moment, plugins for three RLMS have been implemented, namely:

    #. Weblab Deusto, available `here <https://github.com/gateway4labs/rlms_weblabdeusto>`_.
    #. FCEIA, Universidad Nacional del Rosario, available `here <https://github.com/gateway4labs/rlms_unr>`_.
    #. MIT iLabs, available `here <https://github.com/gateway4labs/rlms_ilabs/>`_.

In order to provide a versatile way to include new RLMSs, a RESTful interface is being implemented (this is `issue 30 <https://github.com/gateway4labs/labmanager/issues/30>`_). This interface would consume a REST service offering the RLMS. The advantages of using such interface are:

    #. No need to implement a plugin in Python for new RLMSs -- any programming language (LabVIEW, Java, ...) could be used. 
    #. No hard-coded stuff in the LabManager -- no need to modify the code of LabManager for every new type of RLMS that is going to be supported. 
    #. Same functionality and power as the plugins approach.

Creation of a new RLMS in the LabManager
----------------------------------------

Right now, the creation of a new RLMS in the Labmanager involves the selection of the RLMS type (among those RLMSs whose plugins are installed). After that, several pieces of information must be inserted depending on the RLMS, and this is hard-coded in the LabManager code. As an example, the creation of a Weblab Deusto RLMS is depicted in the figure, which requires the insertion of the location, base URL, login, password, and mappings (other RLMSs, such iLabs, will require different parameters). 

	.. image:: /_static/labmanager_create_rlms.png

When the REST API is ready, the creation of RLMSs in the LabManager will be a three steps procedure, as follows:


    #. **Selection of the RLMSs type.**  Along with the existing RLMSs based on plugins, a new kind called *HTTP* will be added. A *Continue* button will be placed in this view.
    
    #. **Initial insertion of information.**  Based on the RLMS type selected in the previous step, a view requesting the necessary information for each RLMS type will be presented.
 
        * In the case of the plugins based RLMSs, this screen will ask for the same information as the current creation procedure, and will be the last step in this procedure. A *Finish* button will be placed in this view, once it is clicked, the RLMS will be inserted in the database.

        * In the case of the new *HTTP* RLMS kind, this second step will ask for the URL, user and password of the laboratory server. This information will be used on the next step to obtain the list of parameters this RLMS requires to work properly. A *Continue* button will be placed in this view.

    #. **Final insertion of information.** This step will only be executed in the case that the *HTTP* kind has been selected in the first step. For this step, the LabManager will ...

        #. get the list of parameters needed by the RLMS, by querying the REST service implemented by the RLMS. For example, in the case of Weblab Deusto, this list of parameters would include location, base URL, login, password, and mappings.
        #. create a view in which the LabManager admin is asked to provide values  for these parameters.

    A *Finish* button will be placed in this view. Once this button is clicked, the aforementioned parameters will be checked, and the LabManager admin will be informed whether they are correct or not. If they are correct, the new RLMS will be inserted in the database; otherwise, the Labmanager admin will be asked to fix them, or cancel the RLMS creation.
    
API functionalities
-------------------

In order to implement this new feature, RLMSs should implement the following list of functions:

    #. get_rlms_param_list: Returns the list of parameters needed by the RLMSs to work properly.
    #. get_lab_list: Returns the list of laboratories.
    #. get_lab_capacities: Returns the list of capacities of a given lab.
    #. get_lab_version: Returns the version of a given lab.
    #. reserve_lab: Performs the reservation of a lab.




