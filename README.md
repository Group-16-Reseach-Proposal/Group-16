- [USER AUTHENTICATION MECHANISM FOR TECH HEADS PROJECT ON ONLINE MARKETTING FOR ELECTRONICS](#user-authentication-mechanism-for-tech-heads-project-on-online-marketting-for-electronics)
  - [Modules Explanation](#modules-explanation)
  - [1. REGISTRATION SYSTEM](#1-registration-system)
    - [a). Building the Database](#a-building-the-database)
    - [b). Config file by adding PHP](#b-config-file-by-adding-php)
    - [c). Registration page](#c-registration-page)
  - [2.LOGIN SYSTEM](#2login-system)
    - [a). Creating a Login Page](#a-creating-a-login-page)
    - [b). User Online Page](#b-user-online-page)
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
2. Login Page System
3. Logout Script
4.Online user page
5. Password Reset Feature.

Several programming tools are used whencoming up with the system. Tech heads project for user authentication mechanism will use:

1. PHP
2. MYSQL
3. HTML
4. CSS
5. Bootstrap.

After the login system is succesfully built, a welcome page will be displayed to the user on the screen once they login to their respective accounts.
Users will be able to surf through the products and select their preferred products. After they are done with placing their orders and payments are made, they can log out of the system and they will be redirrected to the browser's home page.
We are going to create a CSS Stylesheet that will link our work with design and tidy using CSS.
The CSS file will be saved as style.css so that we can link back to it whenever we need to. An example of the style sheet is given as: body { font-family: arial; font-size: 10pt; } table { font-size: 10pt; margin: 0 auto; } #border { border: 2px solid #999; background: #CCC;
padding: 15px; margin: 0 auto; width: 300px; }

## Modules Explanation

The following discussion is about the procedure we'll be using to create the modules to their implementation finally to deployment.

## 1. REGISTRATION SYSTEM

This section will allow new users to create a new accouns by filling out their credentials to the website account creation page.
They will be able to fill in their credentials and a table will be created automatically by the sytem.

Their are different sub-modules under the Registration system module.

### a). Building the Database

A  database table is file that will store users details in the background. It will hold all the user data once they create their respective account in the Online Electronic System. SQL will majorly be used to create the table inside the MYSQL database to store all the information about each of our users, what types of data are we storing and a default value is also needed.
A plan to achieve all these is needed. Here is our plan:

1.We need to store a username for the user which will be a varchar.
2.We need a password to which will also be a varchar
3.We will need an email for our email activation function this can be varchar too
4.A field telling is if the account has been activated or not, this will be an integer
5.A field giving information about whether the user is online or not, this will be an integer
6.Finally, a field giving us a time the user registered, this is also an integer

We will create a database called login. In this database, we will run an SQL query that will contain a primary key. A primary key is used to uniquely identify each row in the table. The SQL query that we will use is “CREATE TABLE `users` ( `id` int(11) autoincrement, `username` varchar(32), `password` varchar(32),
`online` int(20)default ‘0', `email` varchar(100), `active` int(1)default ‘0', `rtime` int(20) default ‘0', PRIMARY KEY (`id`) ) ENGINE=MyISAM DEFAULT
CHARSET=utf8;”
Here is an example of the database and the user: INSERT INTO `users` (`id`, `username`, `password`, `online`, `email`, `active`, `rtime`) VALUES (1, ‘Techheads’, ‘Techheads4’, 0,
‘techheads4@gmail.com’, 0, 0);

### b). Config file by adding PHP

First things first we need to think about security and how secure is this login form going to be. To help prevent SQL Injection which is a very common form of database hacking we are going to make a function that will protect all strings stored in the database. This we will put in an external file called functions.php. Here is the source –
<?php
function protect($string) {
 $string = trim(strip_tags(addslashes($string))); return $string;
}
?>
This function will trim our string (cut off any white space at the beginning or end of the string), strip tags (remove all html and PHP tags in the string), and then add slashes to the string escaping speech marks (’) and quotation marks (").

### c). Registration page

There are a whole bunch of new functions that we’ll be using in coming up the register page. Firstly, the strlen() function, this returns the number of characters in a string allowing us to check how long strings are. Then the preg_match() function, this checks to see if the formatting of a string matches the formatting you specify (in this case being an email format). Finally, the mail() function, this sends an email from the server to any email of your choice, containing anything you want. This file will be saved as “register.php”
For users to ensure their accounts are secured, a PHP's inbuilt "password_hash() function is used to create a password hash from the password string entered by the user using a process called salting.
This function creates a password hash using one-way hashing algorithm. This means that if two or more users has the same password, their password hashess are different and they will be able to access their accounts without inconveniences.

For a secure login system, the user will be required to verify their account pages using their emails They will activate their accounts as they will a mail with verify account prompt. The source of this page will be “activate.php”

There are two new things in this file, we use the GET method instead of POST and also we use a while() loop. The get method simply gets data from the address bar at the top of the user's browser (in this case being the code sent with the email to their email address). The while() loop is perfecting for checking through multiple rows of data selected from the database (in this case to see if there is a match with the codes). The following will be usedin creating the users’ registration profile.
<link rel="stylesheet" type="text/css" href="README.md/style.css">
  
 You need to fill in all of the required fields!"; }else{ //if all were filled in continue checking
  
 //Check if the wanted username is more than 32 or less than 3 characters long if(strlen($username) > 32 || strlen($username) < 3){ //if it is display error message echo "<center>Your <strong>Username/Email</strong> must be between 5 and 35 characters long!</center>"; }else{ //if not continue checking
  
 //select all the rows from out users table where the posted username matches the username stored $res = mysql_query("SELECT * FROM `users` WHERE `username` = '".$username."'"); $num =
mysql_num_rows($res);
  
 //check if there is a match if($num == 1){ //if yes the username is taken so display error message echo "<center>The <strong>Username</strong> you have chosen is already taken!</center>"; }else{
//otherwise continue checking
  
 //check if the password is less than 5 or more than 32 characters long if(strlen($password) < 5 || strlen($password) > 32){ //if it is display error message echo "<center>Your <strong>Password</strong> must be between 5 and 32 characters long!</center>"; }else{ //else continue checking
  
 //check if the password and confirm password match if($password != $passconf){ //if not display error message echo "<center>The <strong>Password</strong> you supplied did not match the confirmation password!</center>"; }else{ //otherwise continue checking
  
 //Set the format we want to check out email address against $checkemail = "/^[a-z0-9]+([_\\.-][a-z0-9]+)*@([a-z0-9]+([\.-][a-z0-9]+)*)+\\.[a-z]{2,}$/i";
  
 //check if the formats match if(!preg_match($checkemail, $email)){ //if not display error message echo "<center>The <strong>E-mail</strong> is not valid, must be name@server.tld!</center>"; }else{ //if they do, continue checking
  
 //select all rows from our users table where the emails match $res1 = mysql_query("SELECT * FROM `users` WHERE `email` = '".$email."'"); $num1 = mysql_num_rows($res1);
  
 //if the number of matches is 1 If($num1 == 1){
 //the email address supplied is taken so display error message echo "<center>The <strong>E-mail</strong> address you supplied is already taken</center>";
}else{ //finally, otherwise register their account
  
 //time of register (unix) $registerTime = date('U');
  
 //make a code for our activation key $code = md5($username).$registerTime;
  
 //insert the row into the database $res2 = mysql_query("INSERT INTO `users` (`username`, `password`, `email`, `rtime`)
VALUES('".$username."','".$password."','".$email."','".$registerTime."')");
  
 //send the email with an email containing the activation link to the supplied email address mail($email, $INFO['chatName'].' registration confirmation', "Thank you for registering to us".$username.",\n\nHere is your activation link. If the link doesn't work copy and paste it into your browser address bar.\n\n<https://www.yourwebsitehere.co.uk/activate.php?code>=".$code, 'From:noreply@youwebsitehere.co.uk');
  
 //display the success message echo "<center>You have successfully registered, please visit you email inbox to activate your account!</center>"; } } } } } } } }
  
 ?>
 <div id="border">
 <form action="register.php" method="post">
 <table border="0" cellpadding="2" cellspacing="0">
 <tbody>
<tr>
<td>Username: </td>
 <td>
<input name="username" type="text">
</td>
</tr>
<tr>
 <td>Password: </td> <td><input name="password" type="password">
</td>
</tr>
<tr>
 <td>Confirm Password: </td>
 <td>
<input name="passconf" type="password">
</td>
 </tr>
<tr>
 <td>Email: </td>
<td>
<input name="email" size="25" type="text">
</td>
</tr>
<tr>
<td colspan="2" align="center"><input name="submit" value="Register" type="submit">
</td>
 </tr>
<tr>
<td colspan="2"
align="center"><a href="login.php">Login</a> | <a href="forgot.php">Forgot Password</a>
</td>
 </tr>
 </tbody>
</table>
</form>
</div>
?>

## 2.LOGIN SYSTEM

During login, the system will verify the given passwords with hash password stored in database using PHP passord_verify() function.
Password salting is a technique used to widely secure paswwords by randomizing the password hashes.

The user will be able to enter either their passwords or emails and then passwords to be granted authority to access their account. When the submit their forms, their inputs will be verified against the credentials stored in database. If username or email matches their password, they will be authorized and granted to access their site, otherwise, login attempt will be rejected.

Creating a login system has sub modules will be followed for a succesful login site. We will be discussing the procedure below.

### a). Creating a Login Page

A file named "login.php" will be created. Then the login form code will be placed inside the file. Tools used in creating the form are: HTML, CSS and PHP.
The code that we’ll be using in our case is : <link rel="stylesheet" type="text/css" href="README.md/style.css">
  <?php
 <form action="login.php" method="post"> <div id="border"> <table border="0" cellpadding="2" cellspacing="0">
 <tbody>
<tr>
<td>Username/Email:</td>
 <td>
<input name="username/email" type="text">
</td>
</tr>
<tr>
<td>Password:</td>
 <td>
<input name="password" type="password">
</td>
 </tr>
<tr>
<td colspan="2" align="center">
<input name="submit" value="Login" type="submit">
</td>
 </tr>
 <tr>
<td colspan="2" align="center">
<a href="register.php">Register</a> | <a href="forgot.php">Forgot Password </a>
</td>
</tr>
</tbody>
</table>
</div>
</form>

 This login function won’t function correctly because we have not told the page what to do with the login form if it is submitted by the user.

We will need to plan on how the page is going to e checking when the form is submitted. Her is a list of what will we are going to be checking:
 1.That both the username or email and password boxes have been filled in.
2.That the username or email supplied exists in our database
3.That if the username exists in our database, the password matches the one for the username
4.Finally, that the user has activated their account

If all the four points are answered by PHP, then the user will be logged in successfully.
Now we have a place to store and check user information from, a function to protect strings being passed to the database, and a nice-looking layout for our login page. Below you can see the commented code for our login.php file with the newly added PHP-
<link rel="stylesheet" type="text/css" href="techeads/style.css">
  
 You need to fill in a <strong>Username/Email</strong> and a <strong>Password</strong>!"; }else{ //if the were continue checking
  
 //select all rows from the table where the username matches the one entered by the user $res = mysql_query("SELECT * FROM `users` WHERE `username` = '".$username."'"); $num =
mysql_num_rows($res);
  
 //check if there was not a match if($num == 0){ //if not display an error message echo "<center>The <strong>Username/Email</strong> you supplied does not exist!</center>"; }else{ //if there was a match
continue checking
  
 //select all rows where the username and password match the ones submitted by the user $res = mysql_query("SELECT * FROM `users` WHERE `username` = '".$username."' AND `password` =
'".$password."'"); $num = mysql_num_rows($res);
  
 //check if there was not a match if($num == 0){ //if not display error message echo "<center>The <strong>Password</strong> Incorrect Password, Please confirm Password</center>"; }else{ //if
there was continue checking
  
 //split all fields from the correct row into an associative array $row = mysql_fetch_assoc($res);
  
 //check to see if the user has not activated their account yet if($row['active'] != 1){ //if not display error message echo "<center>Please <strong>Activate</strong> your account to Proceed!</center>";
}else{ //if they have log them in
  
 //set the login session storing their id - we use this to see if they are logged in or not $_SESSION['uid'] = $row['id']; //show message echo "<center>Login Successful! </center>";
  
 //update the online field to 50 seconds into the future $time = date('U')+50; mysql_query("UPDATE `users` SET `online` = '".$time."' WHERE `id` = '".$_SESSION['uid']
  
 //redirect them to the users online page header('Location: usersOnline.php

<form action="login.php" method="post">
<div id="border"> <table border="0" cellpadding="2" cell-spacing="0">
<tbody>
<tr>
<td>Username:</td>
 <td>
 <input name="username/email" type="text"></td>
</tr>
<tr>
 <td>Password:</td>
 <td>
 <input name="password" type="password"></td>
 </tr>
<tr>
<td colspan="2" align="center">
<input name="submit" value="Login" type="submit">
</td>
</tr>
<tr>
 <td colspan="2" align="center">
 <a href="register.php">Register</a> | <a href="forgot.php">Forgot Password</a>
</td>
</tr>
</tbody>
</table>
 </div>
</form>

Most of this is explained by the commenting but one part I didn't explain is the online field. When you successfully login, we updated the online field to 50 seconds ahead of now. The date('U') function gives us the number of seconds since January 1 1970 00:00:00 GMT (Unix epoch). This means that date('U') will never get smaller, the value will always increase. If we set the online field to 50 seconds ahead of now then when the Users Online page is loaded, we can check to find all the users where the online value is more than the time when the page is loaded, if this is the case then display each of their names.

### b). User Online Page

A welcome page is where the user will be redirected onc e they succesfully login into their account.
We create a file named "welcome.php"
It welcomes the user to the account for online shopping for electronics.
The user online page section of the website is where the user will need to be logged in to view. This website is different because we need to check if the user is logged in or not to view their page. If they are not logged in and try to view the page, an error message saying "You need to be logged in to view this page!", will be shown or they will be redirect them back to the login page.

We  will use the following usersOnline.php source code to create the code

<link rel="stylesheet" type="text/css" href="README.md file/style.css">

You need to be logged in to user this feature!"; }else{ //otherwise continue the page.

//this is out update script which should be used in each page to update the users online time $time = date('U')+50; $update = mysql_query("UPDATE `users` SET `online` = '".$time."' WHERE `id` = '".$_SESSION['uid']."'");
<?php
  <div id="border">
  <table width="100%" border="0" cellpadding="2" cellspacing="0">
   <tbody>
   <tr>
    <td>
    <strong>Users Online:</strong>
    </td>
     <td> '".date('U')."'");

//loop for each row while($row = mysql_fetch_assoc($res))
{
     //echo each username found to be online with a dash to split them echo $row['username']
</td>
 </tr>
  <tr>
  <td colspan="2" align="center">
  <a href="logout.php">Logout</a>
  </td>
   </tr>
    </tbody>
    </table>
</div>
In this section we not only ensure that the users' are logged in, but we update the online time keeping the online field ahead of the current time. Each time a page is loaded with that script, it will update to put them online.

## LOGOUT

### c). Creating a Logout Script

A "logout.php" file is created. This is the commented code for the file. This is when a user is finished with the business they were doing on the site. When they click on the logout or sighn out link, they will be redirected back to login page and the script inside the file destroys the session.
The following code will create a logout script for the user.
<link rel="stylesheet" type="text/css" href="README.md files/style.css">

You need to be logged in to log out!"; }else
{
     //if it does continue checking

//update to set this users online field to the current time mysql_query("UPDATE `users` SET `online` = '".date('U')."' WHERE `id` = '".$_SESSION['uid']."'");

//destroy all sessions canceling the login session session_destroy();

//display success message echo <center>"You have successfully logged out!"</center>

## PASSWORD RECOVERY

### d). Adding a Password Reset Feature

A system is much better when it has a password reset feature. This I where the account holder(user) forgets the password and they are barred from accessing their accounts. The password reset feature enables them to reset their passwords by verifying the registration details in the database. A password reset utility added will be added to our login system.
When the feature is used, users can instantly reset their own passwords for their accounts.
We will create a file name called "forgot.php" then place the code inside.
 If the user forgets their password, we can email it to them now we know that they supplied a real email address because of the activation. 
 <link rel="stylesheet" type="text/css" href="tut_files/style.css"> 
  
 You need to fill in your <strong>E-mail</strong> address!"; 
 }
 else{ 
     //else continue checking 
  
 //set the format to check the email against $checkemail = "/^[a-z0-9]+([_\\.-][a-z0-9]+)*@([a-z0-9]+([\.-][a-z0-9]+)*)+\\.[a-z]{2,}$/i"; 
  
 //check if the email doesnt match the required format if(!preg_match($checkemail, $email)){ //if not then display error message echo "<center><strong>E-mail</strong> is not valid, must be name@server.tld!</center>"; }else{ //otherwise continue checking 
  
 //select all rows from the database where the emails match $res = mysql_query("SELECT * FROM `users` WHERE `email` = '".$email."'"); $num = mysql_num_rows($res); 
  
 //check if the number of row matched is equal to 0 if($num == 0){ //if it is display error message echo "<center>The <strong>E-mail</strong> adreess you added can not be found</center>"; }else{ //otherwise complete forgot password function 
  
 //split the row into an associative array $row = mysql_fetch_assoc($res); 
  
 //send email containing their password to their email address mail($email, 'Forgotten Password', "Reset Password: ".$row['password']."\n\nkeep your password safe and private", 'From: noreply@yourwebsitehere.co.uk
  
 //display success message echo "<center>An email has been sent to your email for pasword recovery, please check out.</center>

  <div id="border">
   <form action="forgot.php" method="post"> 
   <table border="0" cellpadding="2" cellspacing="0"> 
   <tbody>
   <tr>
    <td>Email: </td>
     <td>
     <input name="email" type="text">
     </td>
      </tr> 
<tr>
 <td colspan="2" align="center">
 <input type="submit" value="Submit" name="submit">
 </td>
  </tr>
   <tr>
    <td colspan="2" align="center">
    <a href="register.php">Register</a> | <a 
href="login.php">Login</a>
</td>
 </tr>
  </tbody>
  </table>
   </form>
    </div>
