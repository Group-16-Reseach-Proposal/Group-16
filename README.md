- [USER AUTHENTICATION MECHANISM FOR TECH HEADS PROJECT ON ONLINE MARKETTING FOR ELECTRONICS](#user-authentication-mechanism-for-tech-heads-project-on-online-marketting-for-electronics)
  - [Modules Explanation](#modules-explanation)
  - [1. REGISTRATION SYSTEM](#1-registration-system)
    - [a). Database Table](#a-database-table)
    - [b). Config file](#b-config-file)
    - [c). Registration Form](#c-registration-form)
  - [2.LOGIN SYSTEM](#2login-system)
    - [a). Creating a Login Form](#a-creating-a-login-form)
    - [b). Creating a Welcome Page](#b-creating-a-welcome-page)
  - [LOGOUT](#logout)
    - [c). Creating a Logout Script](#c-creating-a-logout-script)
  - [PASSWORD RECOVERY](#password-recovery)
    - [d). Adding a Password Reset Feature](#d-adding-a-password-reset-feature)

# USER AUTHENTICATION MECHANISM FOR TECH HEADS PROJECT ON ONLINE MARKETTING FOR ELECTRONICS

This documentation is about implementing user's authentication mechanism for Online marketting for electronics.
User Authentication is a security mechanism used to restrict unauthorized access to member only areas and tools on a given site.
Various considerations are followed when developing a user authentication mechanism.
In our project, we considered creating the mechanism by using certain modules. This modules include:

1. Registration System.
2. Login System
3. Logout Script
4. Password Reset Feature.

Several programming tools are used whencoming up with the system. Tech heads project for user authentication mechanism will use:

1. PHP
2. MYSQL
3. HTML
4. CSS
5. Bootstrap.

After the login system is succesfully built, a welcome page will be displayed to the user on the screen once they login to their respective accounts.
Users will be able to surf through the products and select their preferred products. After they are done with placing their orders and payments are made, they can log out of the system and they will be redirrected to the browser's home page.

## Modules Explanation

The following discussion is about the procedure we'll be using to create the modules to their implementation finally to deployment.

## 1. REGISTRATION SYSTEM

This section will allow new users to create a new accouns by filling out their credentials to the website account creation page.
They will be able to fill in their credentials and a table will be created automatically by the sytem.

Their are different sub-modules under the Registration system module.

### a). Database Table

A  database trable is file that will store users details in the background. It will hold all the user data once they create their respective account in the Online Electronic System. SQL will majorly be used to create the table inside the MYSQL database. 

During registering, users will be required to fill their details beginning with their  first and last names, username for the site, their emails, phone numbers, location, age(18+) and ofcourse their account password.

### b). Config file

After the table is created, a PHP script is needed in order to connect MYSQL database server.
We will create a file then place a code iside. The file's name will be "config.php".

Data will be placed according to the MYSQL server settings. We will name our database as Online shop for electronics.

### c). Registration Form

On the registration form, a different PHP file named "register.php" will be created. We will come up with a code that will create a web form that allows user to register themselves succesfully.

For users to ensure their accounts are secured, a PHP's inbuilt "password_hash() function is used to create a password hash from the password string entered by the user using a process called salting. 
This function creates a password hash using one-way hashing algorithm. This means that if two or more users has the same password, their password hashess are different and they will be able to access their accounts without inconviniences.

During login, the system will verify the given passwords with hash password stored in database using PHP passord_verify() function.
Password salting is a technique used to widely secure paswwords by randomizing the password hashes.

## 2.LOGIN SYSTEM

The user will be able to enter either their passwords or emails and then passwords to be granted authority to access their account. When the submit their forms, their inputs will be verified against the credentials stored in database. If username or email matches their password, they will be authorized and granted to access their site, otherwise, logi attempt will be rejected.

Creating a login system has sub modules will be followed for a succesful login site. We will be discussing the procedure below.

### a). Creating a Login Form

A file named "login.php" will be created. Then the login form code will be placed inside the file. Tools used in creating the form are: HTML, CSS and PHP.

### b). Creating a Welcome Page

A welcome page is where the user will be redirected onc they succesfully login into their account.
We create a file named "welcome.php"
It welcomes the user to the account for online shopping for electronics.

## LOGOUT

### c). Creating a Logout Script

A "logout.php" file is created. This is when a user is finished with the business they were doing on the site. When they click on the logout or sighn out link, they will be redirrected back to login page and the script inside the file destroys the session.

## PASSWORD RECOVERY

### d). Adding a Password Reset Feature

A system is much better when it has a password reset feature. This I where the account holder(user) forgets the password and they are barred from accessing their accounts. The password reset feature enables them to reset their passwords by verifying the registration details in the database. A password reset utility added will be added to our login system.
When the feature is used, users can instantly reset their own passwords for their accounts.
We will create a file name called "reset-password.php" then place the code inside.
