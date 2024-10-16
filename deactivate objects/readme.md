download deactivate_objects.zip... extract and import the xml file into the root folder of your AE.

Changes to be made...

Update VARA_DECOMM_CONFIG... use a share path for export if you have multiple AE servers, update angent with a windows agent and login with the login object name

Update CALL_GET_CONFIRMATION recipients, remove USERGROUP and add you user group for notification, the flow waits till you accept this request when running

Execute the flow OBJECT_DECOMM and enter the name of agent to be decommissioned in the prompt set

