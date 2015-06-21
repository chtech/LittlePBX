# LittlePBX

====  simple multiple organization front-end to shared Asterisk  ====

Simple PHP GUI front-end to Asterisk PBX

Allows one host with one Asterisk PBX instance to be used by multiple independent organizations. The PBX interface consists of one web page which lists all of the DID associated with the current organization at the top. Under this DID list is a list of all of the extensions for that organization. The GUI has controls to edit, add, or delete extensions, with simple call flow and voice mail controls next to each extension. The DID may not be edited.

There would be an Apply button, a Stop button, a Discard button, and a Reset button, to Apply whatever configuration changes have been made after possibly waiting some time for on-going calls, Stop the current Apply operation, Discard input to revert back to the current (last successfully applied) configuration, and Reset the organization's configuration back to some reasonable defaults. All input to the GUI is stored in the LittlePBX db as it is entered, so no save is necessary. There is an option to e-mail the organization PBX admin when the config has actually been applied if the Apply operation has to wait.

IVR is not supported. Music on hold is a checkbox and an upload MP3 button. LittlePBX is intended initially as a very basic system. For more, try Elastix or FreePBX. If LittlePBX works well performance and reliability wise, more features may be added. However, LittlePBX can never allow direct control of the underlying Asterisk or the independence of the organizations would be compromised.

One upstream inbound and one upstream outbound SIP user/host are allowed per organization. The upstream inbound and outbound SIP user/host may be the same. Different organizations would have different upstream SIP user/host.

The upstream SIP trunk info and other organization info are not in the GUI. There is a REST interface for SIP upstream registration info and other trunk info, DID, and other organization info.

There is a second page, LittlePBXAdmin, that uses the LittlePBX REST interface. This second page is intended for demonstration purposes.

Needs a login page. If already logged in, go straight to PBX page.
Stats page if easy.
Configuration help pages for popular SIP phones. (hardphones, wireless apps, PC/MAC applications)

The Asterisk instance is controlled and configured using relatively recent Asterisk REST and database mechanisms. There needs to be a mechanism to either make sure no calls from any organization are affected by configuration updates, or make sure calls outside of the organization being configured are not effected and the organization's calls are handled gracefully.

LittlePBX stores its own and organization specific configuration data in a mysql database, shared by all organizations. Hopefully the Asterisk db and the LittlePBX db will be run by the same mysql instance, so that transactions can be easily used for consistent state.

This repository contains the PHP source and shell scripts to set up and remove the system. These scripts have mysql commands for the database.

This system will likely require a recent Asterisk version and perhaps a recent Debian or related version. It is hoped that someday there might be an APT package for this. This system should be designed to support FreeSWITCH as well as Asterisk, selecting the PBX type at installation.
