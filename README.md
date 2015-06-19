# LittlePBX

====  simple multiple organization front-end to shared Asterisk  ====

Simple PHP GUI front-end to Asterisk PBX.

Allows one host with one Asterisk PBX instance to be used by multiple independent organizations. The interface consists of one web page which lists all of the DID associated with the current organization. Under this DID list is a list of all of the extensions for that organization. The GUI has controls to edit, add, or delete extensions, with simple call flow and voice mail controls next to each extension.

One upstream inbound and one upstream outbound SIP user/host are allowed per organization, they may be the same. Different organizations would have different upstream SIP user/host. The upstream SIP trunk info is not in the GUI. There is a REST interface for SIP upstream registration info and other trunk info, DID, and other organization info. There is a second page, LittlePBXAdmin, that uses this REST interface.

This system is severely limited versus using separate Asterisk instances for each organization. For instance, configuration changes are not applied until there are no calls through the Asterisk instance at all, including calls of other organizations. The extension registration strings need to be unique across the organizations.

One set of Asterisk configuration files is used for all of the organizations, since there is only one instance. Data outside of Asterisk configuration files is stored in one mysql database, shared by all organizations.

This repository contains the PHP source and shell scripts to set up and remove the system. These scripts have mysql commands for the database. It is hoped that someday there might be an APT package for this.
