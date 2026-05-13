## Configuration Export and Import 

RouterOS allows exporting and importing parts of the configuration in plain text format. This method can be used to copy bits of configuration between different devices, for example, clone the whole firewall from one router to another. 

An export command can be executed from each menu (resulting in configuration export only from this specific menu and all its sub-menus) or from the root menu for complete config export and is available for CLI only. 

**==> picture [13 x 13] intentionally omitted <==**

The Export command does not export system user passwords, installed certificates, SSH keys, Dude, or a User-manager database. 

Installed certificates, Dude, and User-manager databases must be manually exported and imported into a new device. System user passwords and user SSH keys can not be exported. 

**==> picture [13 x 13] intentionally omitted <==**

During config import, we suggest using the same RouterOS version used during config export to prevent cases when some of the commands do not exist in one or another RouterOS version.
