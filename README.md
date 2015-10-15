# LittlePBX

Hosted PBX For Shared Use By Multiple Independent Organizations


LittlePBX is a simple PHP GUI to FreeSWITCH, and some installation and maintenance scripts, that allow a single FreeSWITCH instance to support multiple independent organizations without them interfering with each other. The GUI is intended for non-technical users. It does not perform system setup tasks.


The PBX GUI interface consists of a web page which lists all of the DID associated with the current organization at the top. Under this DID list is a list of all of the extensions for the organization. The GUI has controls to edit, add, or delete extensions, with simple call flow and voice mail controls next to each extension. The DID may not be edited.

IVR is not supported. Music on hold is a checkbox and an upload MP3 button. LittlePBX is intended initially as a very basic system. For more, try Elastix or FreePBX. If LittlePBX works well performance and reliability wise, more features may be added. However, LittlePBX can never allow direct user control of the underlying FreeSWITCH or use of unstable FreeSWITCH features, or the independence of the organizations would be compromised. 

LittlePBX has an Apply button, a Stop button, a Discard button, and a Reset button, to Apply whatever configuration changes have been made in the GUI after possibly waiting some time for on-going calls, Stop the current Apply operation, Discard GUI input to revert back to the current (last successfully applied) configuration, and Reset the organization's configuration back to some reasonable defaults. All input to the GUI is stored in the LittlePBX db as changes have been made in the GUI, so no save is necessary. There is an option to e-mail the organization PBX admin when the config has actually been applied if the Apply operation has to wait.

One upstream inbound and one upstream outbound SIP user/host are allowed per organization. The upstream inbound and outbound SIP user/host may be the same. Different organizations would have different upstream SIP user/host.

The upstream SIP trunk info and other organization info are not in the GUI. There is a REST interface to control SIP upstream registration info and other trunk info, DID, and other organization info including company name and logo to be displayed on the PBX web pages.

There is a second page, LittlePBXAdmin, that uses the REST interface to LittlePBX. This second page is intended for demonstration purposes. Normal Admin, such as setting passwords, configuration, and adding DID, would be done by a page on the org owning the PBX server that the particular client company would log into and use to buy DID, with a checkbox to enable LittleBOX for that client company and set the PBX password etc.

Needs a login page. If already logged in, go straight to PBX page.
Stats page if easy.
Configuration help pages for popular SIP phones. (hardphones, wireless apps, PC/MAC applications)

If the URL has the form pbx.orgname.domain, where domain is an arbitrary domain or subdomain, orgname is used to determine the organization.

The FreeSWITCH instance is controlled and configured using FreeSWITCH REST and database mechanisms. There needs to be a mechanism to either make sure no calls from any organization are affected by configuration updates, or make sure calls outside of the organization being configured are not affected and the organization's calls are handled gracefully.

LittlePBX stores its own and organization specific configuration data in a mysql database, shared by all organizations. Hopefully the FreeSWITCH db and the LittlePBX db will be run by the same mysql instance, so that transactions can be easily used for consistent state.

This repository contains the PHP source and shell scripts to set up and remove the system. These scripts contain mysql commands for the database.

This system will likely require a particular recent FreeSWITCH version or versions and perhaps a recent Debian or related version. It is hoped that someday there might be an APT package for this.

<<<< Find an open source android/iphone app implementing a SIP phone, hopefully integrated with the phone's dialer, and work with the author(s) to hook it directly to LittlePBX by specifing the LittlePBX URL, name of extension to be used, and extension password within the phone app. The phone app would then reach out to the LittlePBX for such things as SIP registration strings, using the password entered into the app for registration also. Rest/XML interface. The phone app should allow transfer/conferencing/intercom/messaging with other organization extensions using standard SIP mechanisms, hopefully supported by FreeSWITCH, getting the list of organization extensions from LittlePBX. Some way to view organization extensions.
>>>> Been looking for a stable completely open source android/iphone SIP phone app. If anybody knows of a good one, please let me know. I would add to it if it does not already have:
1. a standard office desktop phone / phone handset UI. They typically have a grid of control buttons in addition to a phone's normal dial buttons, and a little window at the top where the number or other info is displayed. For this handset app there will probably be no normal dial buttons, just the control grid, and the little window at the top may be a little bigger, with drop down if necessary, and the usual big button for answer/hangup
2. some way to temporary/lock unlock, unlock for call or  longer time, use or disable the proximity sensor lock.
3. skinning of the UI. Number of, arrangement of, position of, size of, edge shape of, the buttons and the display window. Control of fonts, colors, borders. Background graphics and foreground text, including client company logos. Skins for: normal small businesses, a more tech looking theme, a more business like theme, a more personal theme, and 'rad' if they still call it that. this skin would be configured in a LittlePBX page for the client and downloaded to the client phones. push download is best.
4. interface to an LDAP server, possibly controlled by a LittlePBX window to maintain contacts and hook up to other LDAP databases. Not sure the handset app needs to be able to edit contacts, maybe future, maybe some way to pop a LittlePBX mobile web page for contact entry in the LDAP with details on the current/last call/call about to be made such as CID or number dialed, LNAM, etc.
5. interface to the standard android or iPhone dialer and contacts.
6. programming the handset app control buttons. this would be done on a per phone basis in LittlePBX, under control of the phone user who is the LittlePBX extension user, with some master controls set up by the LittlePBX admin for the client company. A normal office phone has typically some columns of buttons associated with particular extensions on the PBX, other columns associated with particular functions such as conference, transfer, hold etc.
7. combine the selection interface to the LDAP contact list, android or iphone contacts, extensions known from LittlePBX. Eg., type a name or number into the little window in the handset app, a drop down pops with all matching names and numbers as you type, ordered using a nondeterministic algorithm that allows for spelling correction, soundex, how recently that entry has been used from that handset, and so on. Maybe the pop down just includes the ones that fit on the screen in a relatively large font, with a button to pop the full match list into a scrolling window.
8. Integrated messaging. Somewhere have an XMPP server, should support messaging between all of these handsets, as well as any other XMPP apps out there. Other protocol instead if it is more popular. Pop up a chat session if the message button is pushed instead of the dial button. Chat history, going back, on the server if that is available. Include SMS/MMS messaging. Maybe even allow IRC. Maybe even integrate general IMAP e-mail.
9. Conferences including group messaging.
10. Pop Up Display type control center.

For Future:
Explicit Call Transfer, hooks input to output by changing PSTN switching, ss7 allows this, not sure what it is called
LDAP organization phone book, integrated using open source android/iphone app into mobile devices Contacts
Mobile app version of LittlePBX, interfacing to hosted FreeSWITCH
