## WebFig login page 

The WebFig login page is a customized default RouterOS login interface that appears when accessing the router's IP address. This page can be customized to meet branding or functional requirements. 

Customization Files: 

      - **`/index2.html`** : Main template for the login page. 

      - **`/assets/style.css`** :  MikroTik RouterOS stylesheet. 

- **`/assets/script.js`** is responsible for handling the login functionality and contains code that gives the button interactivity. 

- Required Elements for the **`script.js`** : 

   1. Form for Login: 

      - `<form id="login">` 

   2. Username Field: 

      - `<input id="name" data-defaultuser="admin">` 

         - The `admin` value can be changed to another username or left blank. 

   3. Password Field: 

```
<input id="password">
```

4. Error Display Section: `<div id="error">` 

210 

Here is an example of a user-customized login page with a "Show Password" button, achieved using a modified **`index2.html`** along with additional css and  files.js 

The HTML file must be named "index2.html" and should use properly nested HTML to ensure compatibility with all browsers. 

The uploaded images or JavaScript files must reference to the same path as the index file, no custom folder names can be used.
