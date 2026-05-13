## Designing skins 

If the user has sufficient permissions (the group has the policy "policy" and "sensitive" to edit permissions) Design Skin button becomes available. Pressing that toggle button will open interface editing options. 

To prevent the user from accessing the Design Skin menu, disable policy "policy" and "sensitive" under the user group configuration. 

Possible operations are: 

Hide menu - this will hide all items from the menu and its submenus; 

- Hide submenu - only certain submenu will be hidden; Hide tabs - if submenu details have several tabs, it is possible to hide them this way; Rename menus and items - make certain features more obvious or translate them into your language; Add a note to the item (in detail view) - to add comments on the field; 

- Make item read-only (in detail view) - for user safety very sensitive fields can be made read only; Hide flags (in detail view) - while it is only possible to hide a flag in detail view, this flag will not be visible in list view and in detailed view; Add limits for the field - (in detail view) where it is the list of times that are comma or newline separated list of allowed values: 

   - number interval '..' example: 1..10 will allow values from 1 to 10 for fields with numbers, for example, MTU size. field prefix (Text fields, MAC address, set fields, combo-boxes). If it is required to limit prefix length $ should be added to the end. For example, limiting the wireless interface to "station" only, "Add limit" will contain "station$" 

**==> picture [505 x 10] intentionally omitted <==**

- Add Tab - will add a gray ribbon with an editable label that will separate the fields. Ribbon will be added before the field it is added to; Add Separator - will add a low height horizontal separator before the field it is added to. 

**==> picture [13 x 13] intentionally omitted <==**

Note: Number interval cannot be set to extend limitations set by RouterOS for that field 

**==> picture [13 x 13] intentionally omitted <==**

Note: Set fields are arguments that consist of a set of check-boxes, for example, setting up policies for user groups, RADIUS "Service" 

**==> picture [13 x 13] intentionally omitted <==**

Note: Limitations set for combo-boxes will also limit the values selectable from the dropdown
