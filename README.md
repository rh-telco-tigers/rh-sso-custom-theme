# Steps to configure custom theme in RedHat Single Sign On

Below are steps to add custom field to an existing and using JavaScript to process data in login form

Here is the official documentation to create necessary artifications to create and load custom theme : https://docs.redhat.com/en/documentation/red_hat_single_sign-on/7.6/html/server_developer_guide/themes#creating_a_theme

In this repo, we have some sample files to create custom login theme.

1) Checkout the repo and copy ```peru-login``` folder into themes folder

2) In theme.properties file, you mention the javascript file reference and the CSS used.

3) Create the resources/js/script.js file inside themes/login folder.

4) Copy an existing ```login.ftl``` file from other themes like base. Add below code after import element ion starting of document.
    - Add custom HTML code ```<h1>HELLO WORLD!</h1>```
    - Refer to JavaScript
      ```<script type="text/javascript" src="resources/js/script.js"></script>```
    - Add below code to modify the default login page to add new elements
               
               <div class="${properties.kcFormGroupClass!}">
                    <label for="appId" class="${properties.kcLabelClass!}">${msg("appId")}</label>

                    <input tabindex="3" id="appId" class="${properties.kcInputClass!}" name="appId" type="text" autocomplete="off"
                           aria-invalid="<#if messagesPerField.existsError('username','password','appId')>true</#if>"
                    />
                    <#if usernameHidden?? && messagesPerField.existsError('username','password','appId')>
                        <span id="input-error" class="${properties.kcInputErrorMessageClass!}" aria-live="polite">
                                ${kcSanitize(messagesPerField.getFirstError('username','password','appId'))?no_esc}
                        </span>
                    </#if>
                </div>
   - Call JavaScript function on form submit in login page. Add the following ```onclick="myFunction()"``` to form submit element.

5) Update your theme in Admin Console
      ```
      Log into the Admin Console to checkout your new theme
      Select your realm
      Click Realm Settings from the menu.
      Click on the Themes tab.
      For Login Theme select peru-login and click Save.
      ```
      ![image](https://github.com/user-attachments/assets/77d55d5d-5e4b-4f91-8c15-2851c5d00910)

### New Login Page looks like with new field 'appId'

![image](https://github.com/user-attachments/assets/32a62023-8a17-4b4f-8f3c-b8f8109e239b)

### Once you click ```Sign In ```, JavaScript code is executed and login into admin console.

![image](https://github.com/user-attachments/assets/8432c835-0aef-4210-8d70-7439d75d48ca)








