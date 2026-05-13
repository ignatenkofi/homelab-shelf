## Allowed versions 

Device mode lists in its parameters an argument called "allowed-versions". This is a list of versions which MikroTik considers as secure and which ones do not include any serious vulnerabilities which could be used by an attacker. This list can be updated to versions which includes some major changes in RouterOS below which downgrade should not be allowed. 

This setting does not depend on the installed RouterOS version and works as a separate mechanism, in order to disallow attacker to downgrade version step-by-step in order to reach some vulnerable RouterOS release. This means that if you upgrade RouterOS to a release where a newer "allowedversions" list is available, oldest list will be overwritten. If you downgrade RouterOS, "allowed-versions" list will not change and will remain updated to the latest list. 

This list is ignored, if device-mode "install-any-version" is enabled.
