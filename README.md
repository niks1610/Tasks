# Tasks

#index.php

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>SignUp form</title>
    <link href="css/bootstrap.min.css" rel="stylesheet">
      <link href="styling.css" rel="stylesheet">
      <link href='https://fonts.googleapis.com/css?family=Arvo' rel='stylesheet' type='text/css'>
      </head>
  <body>
    <!--Navigation Bar-->  
      <nav role="navigation" class="navbar navbar-custom navbar-fixed-top">
      
          <div class="container-fluid">
            
              <div class="navbar-header">
              
                  <a class="navbar-brand">My Website</a>
                  <button type="button" class="navbar-toggle" data-target="#navbarCollapse" data-toggle="collapse">
                      <span class="sr-only">Toggle navigation</span>
                      <span class="icon-bar"></span>
                      <span class="icon-bar"></span>
                      <span class="icon-bar"></span>
                  
                  </button>
              </div>
              <div class="navbar-collapse collapse" id="navbarCollapse">
                  <ul class="nav navbar-nav">
                    <li class="active"><a href="#">Home</a></li>
                    <li><a href="#">Help</a></li>
                    <li><a href="#">Contact us</a></li>
                  </ul>
                  <ul class="nav navbar-nav navbar-right">
                    <li><a href="#loginModal" data-toggle="modal">Login</a></li>
                  </ul>
              
              </div>
          </div>
      
      </nav>
      
      
      
      
      
      
      
      
      
      <h2 id="head">Welcome to Currency Converter..</h2>
    
    
    <div id="wrapper">
        <form method="post">
           &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
          <input type="text" name="amount" placeholder="         Enter Amount" >
            <br /><br />
             <div class="buttons">
               <select name="convert_from">
                          <option  value="USD">US Dollar</option>
                </select>
               &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                <select name="convert_to">
                <option  value="INR">Indian Rupee</option>
                    
                 <option  value="USD">US Dollar</option>
                    
                 <option  value="SGD">Singapore Dollar</option>
                    
                 <option value="EUR">Euro</option>
                    
                  <option  value="AED">UAE Dirham</option>
                </select>  

            </div>
            <br/>
         &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<input type="submit" name="convert_currency" value="Convert Currency" >
        </form>
       
    </div>
<?php

if(isset($_POST['convert_currency']))
{
    $from=$_POST['convert_from'];
    $to=$_POST['convert_to'];
    $amount=$_POST['amount'];
 $request = curl_init('http://apilayer.net/api/live?access_key=36a72f4a5ede8aeb3789dcdac7d16413&currencies='.$to.'&source=USD&format=1'); 
 
 curl_setopt ($request, CURLOPT_RETURNTRANSFER, true); 
 
 $response = curl_exec($request); 
 curl_close($request); 
 
 $converseResult=json_decode($response,true);

    $cur1=$converseResult['quotes']["USD$to"];
 
echo '<div class=list id=list>';    
echo "1 USD=$cur1 $to";
echo  '</div>';
$result = $amount*$converseResult['quotes']["USD$to"];

echo "<div class=result id=result><p>Your Amount after Conversion is=$result.</p></div>" ;

}
?>
     
      
      
      
       
      
      
    <!--Jumbotron with Sign up Button-->
<div class="jumbotron" id="myContainer">
          
           <button class="btn btn-lg green" type="button" onclick="refresh()">Refresh</button>
      
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
          <button type="button" class="btn btn-lg green signup" data-target="#signupModal" data-toggle="modal">Sign up-It's free</button>

     
</div>
      

    <!--Login form-->    
      <form method="post" id="loginform">
        <div class="modal" id="loginModal" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <button class="close" data-dismiss="modal">
                    &times;
                  </button>
                  <h4 id="myModalLabel">
                    Login: 
                  </h4>
              </div>
              <div class="modal-body">
                  
                  <!--Login message from PHP file-->
                  <div id="loginmessage"></div>
                  

                  <div class="form-group">
                      <label for="loginemail" class="sr-only">Email:</label>
                      <input class="form-control" type="email" name="loginemail" id="loginemail" placeholder="Email" maxlength="50">
                  </div>
                  <div class="form-group">
                      <label for="loginpassword" class="sr-only">Password</label>
                      <input class="form-control" type="password" name="loginpassword" id="loginpassword" placeholder="Password" maxlength="30">
                  </div>
                                 
              </div>
              <div class="modal-footer">
                  <input class="btn green" name="login" type="submit" value="Login">
                <button type="button" class="btn btn-default" data-dismiss="modal">
                  Cancel
                </button>
                <button type="button" class="btn btn-default pull-left" data-dismiss="modal" data-target="signupModal" data-toggle="modal">
                  Register
                </button>  
              </div>
          </div>
      </div>
      </div>
      </form>

    <!--Sign up form--> 
      <form method="post" id="signupform">
        <div class="modal" id="signupModal" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <button class="close" data-dismiss="modal">
                    &times;
                  </button>
                  <h4 id="myModalLabel">
                    Sign up today and Start using my Website today! 
                  </h4>
              </div>
              <div class="modal-body">
                  
                  <!--Sign up message from PHP file-->
                  <div id="signupmessage"></div>
                  
                  <div class="form-group">
                      <label for="username" class="sr-only">Username:</label>
                      <input class="form-control" type="text" name="username" id="username" placeholder="Username" maxlength="30">
                  </div>
                  <div class="form-group">
                      <label for="email" class="sr-only">Email:</label>
                      <input class="form-control" type="email" name="email" id="email" placeholder="Email Address" maxlength="50">
                  </div>
                  <div class="form-group">
                      <label for="password" class="sr-only">Choose a password:</label>
                      <input class="form-control" type="password" name="password" id="password" placeholder="Choose a password" maxlength="30">
                  </div>
                  <div class="form-group">
                      <label for="password2" class="sr-only">Confirm password</label>
                      <input class="form-control" type="password" name="password2" id="password2" placeholder="Confirm password" maxlength="30">
                  </div>
              </div>
              <div class="modal-footer">
                  <input class="btn green" name="signup" type="submit" value="Sign up">
                <button type="button" class="btn btn-default" data-dismiss="modal" data-refresh="true">
                  Cancel
                </button>
              </div>
          </div>
      </div>
      </div>
      </form>

        <!-- Footer-->
      <div class="footer">
          <div class="container">
              <p>Develop with Nikhil &copy; 2020-<?php $today = date("Y"); echo $today?>.</p>
          </div>
      </div>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <script src="js/bootstrap.min.js"></script>
    <script src="javascript.js"></script>
  </body>
</html>

#javascript.php

//Ajax Call for the sign up form 
//Once the form is submitted
$("#signupform").submit(function(event){ 
    //prevent default php processing
    event.preventDefault();
    //collect user inputs
    var datatopost = $(this).serializeArray();
//    console.log(datatopost);
    //send them to signup.php using AJAX
    $.ajax({
        url: "signup.php",
        type: "POST",
        data: datatopost,
        success: function(data){
            if(data){
                $("#signupmessage").html(data);
            }
        },
        error: function(){
            $("#signupmessage").html("<div class='alert alert-danger'>There was an error with the Ajax Call. Please try again later.</div>");
            
        }
    
    });

});

//Ajax Call for the login form
//Once the form is submitted
$("#loginform").submit(function(event){ 
    //prevent default php processing
    event.preventDefault();
    //collect user inputs
    var datatopost = $(this).serializeArray();
//    console.log(datatopost);
    //send them to login.php using AJAX
    $.ajax({
        url: "login.php",
        type: "POST",
        data: datatopost,
        success: function(data){
            if(data == "success"){
                window.location = "index.php";
            }else{
                $('#loginmessage').html(data);   
            }
        },
        error: function(){
            $("#loginmessage").html("<div class='alert alert-danger'>There was an error with the Ajax Call. Please try again later.</div>");
            
        }
    
    });

});

//clear data in modal
$("#signupModal").on('hidden.bs.modal',function(){
    $('#signupform')[0].reset();
    $('#signupmessage').empty();
});

$("#loginModal").on('hidden.bs.modal',function(){
    $('#loginform')[0].reset();
    $('#loginmessage').empty();
});


function refresh(){
    $('#list').empty();
    $('#result').empty();
}

$(window).onload(function(event){
   event.preventDefault(); 
});




#styling.css

html{
    position: relative;
    min-height: 100%;
}

/*Background Image*/
body{
    font-family: Arvo, serif;
    background: url("image.png") no-repeat center center;
    background-attachment: fixed;
    background-size: cover;
}


/*Style Jumbotron*/
.jumbotron{
    background-color: transparent;
    text-align: center;
    letter-spacing: 2.5px;
    padding: 10px;
    margin-top: 50px;
}

/*buttons*/
.signup{  
    text-align: center;
    align-items: center;
}

.green{
    background-color: rgba(114,190,35,0.8);   
}

.green:hover{
    background-color: rgb(114,190,35);   
}

/*Style the footer*/
.footer{
    position: absolute;
    bottom: 0;
    text-align: center;
    width: 100%;
    padding-top: 10px;
}

/*Navigation bar*/
.navbar-custom, .footer {
  background-color: #62aacf;
  border-color: #499cc7;
  background-image: -webkit-gradient(linear, left 0%, left 100%, from(#89bfdb), to(#62aacf));
  background-image: -webkit-linear-gradient(top, #89bfdb, 0%, #62aacf, 100%);
  background-image: -moz-linear-gradient(top, #89bfdb 0%, #62aacf 100%);
  background-image: linear-gradient(to bottom, #89bfdb 0%, #62aacf 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff89bfdb', endColorstr='#ff62aacf', GradientType=0);
}
.navbar-custom .navbar-brand {
  color: #ffffff;
}
.navbar-custom .navbar-brand:hover,
.navbar-custom .navbar-brand:focus {
  color: #e6e6e6;
  background-color: transparent;
}
.navbar-custom .navbar-text {
  color: #ffffff;
}
.navbar-custom .navbar-nav > li:last-child > a {
  border-right: 1px solid #499cc7;
}
.navbar-custom .navbar-nav > li > a {
  color: #ffffff;
  border-left: 1px solid #499cc7;
}
.navbar-custom .navbar-nav > li > a:hover,
.navbar-custom .navbar-nav > li > a:focus {
  color: #c0c0c0;
  background-color: transparent;
}
.navbar-custom .navbar-nav > .active > a,
.navbar-custom .navbar-nav > .active > a:hover,
.navbar-custom .navbar-nav > .active > a:focus {
  color: #c0c0c0;
  background-color: #499cc7;
  background-image: -webkit-gradient(linear, left 0%, left 100%, from(#499cc7), to(#70b1d3));
  background-image: -webkit-linear-gradient(top, #499cc7, 0%, #70b1d3, 100%);
  background-image: -moz-linear-gradient(top, #499cc7 0%, #70b1d3 100%);
  background-image: linear-gradient(to bottom, #499cc7 0%, #70b1d3 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ff499cc7', endColorstr='#ff70b1d3', GradientType=0);
}
.navbar-custom .navbar-nav > .disabled > a,
.navbar-custom .navbar-nav > .disabled > a:hover,
.navbar-custom .navbar-nav > .disabled > a:focus {
  color: #cccccc;
  background-color: transparent;
}
.navbar-custom .navbar-toggle {
  border-color: #dddddd;
}
.navbar-custom .navbar-toggle:hover,
.navbar-custom .navbar-toggle:focus {
  background-color: #dddddd;
}
.navbar-custom .navbar-toggle .icon-bar {
  background-color: #cccccc;
}
.navbar-custom .navbar-collapse,
.navbar-custom .navbar-form {
  border-color: #479bc7;
}
.navbar-custom .navbar-nav > .dropdown > a:hover .caret,
.navbar-custom .navbar-nav > .dropdown > a:focus .caret {
  border-top-color: #c0c0c0;
  border-bottom-color: #c0c0c0;
}
.navbar-custom .navbar-nav > .open > a,
.navbar-custom .navbar-nav > .open > a:hover,
.navbar-custom .navbar-nav > .open > a:focus {
  background-color: #499cc7;
  color: #c0c0c0;
}
.navbar-custom .navbar-nav > .open > a .caret,
.navbar-custom .navbar-nav > .open > a:hover .caret,
.navbar-custom .navbar-nav > .open > a:focus .caret {
  border-top-color: #c0c0c0;
  border-bottom-color: #c0c0c0;
}
.navbar-custom .navbar-nav > .dropdown > a .caret {
  border-top-color: #ffffff;
  border-bottom-color: #ffffff;
}
@media (max-width: 767) {
  .navbar-custom .navbar-nav .open .dropdown-menu > li > a {
    color: #ffffff;
  }
  .navbar-custom .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-custom .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #c0c0c0;
    background-color: transparent;
  }
  .navbar-custom .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-custom .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-custom .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #c0c0c0;
    background-color: #499cc7;
  }
  .navbar-custom .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-custom .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-custom .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #cccccc;
    background-color: transparent;
  }
}
.navbar-custom .navbar-link {
  color: #ffffff;
}
.navbar-custom .navbar-link:hover {
  color: #c0c0c0;
}
/* style converter*/


#head{
    height: 100px;
    width:100%;
    font-size: 30px;
    text-align: center;
    color: white;
    margin-top: 80px;
}

#wrapper{
    text-align: center;
}

.buttons{
    margin-left: 70px;
}

.result{
    margin-top: 40px;
    height: 20px;
    color: white;
    text-align: center;
    font-size: 20px;
}
.list{
    margin-top: 40px;
    color: white;
    font-size: 20px;
    text-align: center;
}

#refresh{
    text-align: center;
}


#login.php

<?php
//Start session
session_start();
//Connect to the database
$link = mysqli_connect("localhost", "dreamcha_login", "nikhil", "dreamcha_login");
if(mysqli_connect_error()){
    die('ERROR: Unable to connect:' . mysqli_connect_error()); 
    echo "<script>window.alert('Hi!')</script>";
}

//Check user inputs
    //Define error messages
$missingEmail = '<p><stong>Please enter your email address!</strong></p>';
$missingPassword = '<p><stong>Please enter your password!</strong></p>'; 
    //Get email and password
    //Store errors in errors variable
if(empty($_POST["loginemail"])){
    $errors .= $missingEmail;   
}else{
    $email = filter_var($_POST["loginemail"], FILTER_SANITIZE_EMAIL);
}
if(empty($_POST["loginpassword"])){
    $errors .= $missingPassword;   
}else{
    $password = filter_var($_POST["loginpassword"], FILTER_SANITIZE_STRING);
}
    //If there are any errors
if($errors){
    //print error message
    $resultMessage = '<div class="alert alert-danger">' . $errors .'</div>';
    echo $resultMessage;   
}else{
    //else: No errors
    //Prepare variables for the query
    $email = mysqli_real_escape_string($link, $email);
$password = mysqli_real_escape_string($link, $password);
$password = hash('sha256', $password);
        //Run query: Check combinaton of email & password exists
$sql = "SELECT * FROM users WHERE email='$email' AND password='$password'";
$result = mysqli_query($link, $sql);
if(!$result){
    echo '<div class="alert alert-danger">Error running the query!</div>';
    exit;
}
        //If email & password don't match print error
$count = mysqli_num_rows($result);
if($count !== 1){
    echo '<div class="alert alert-danger">Wrong Username or Password</div>';
}
else {
    //log the user in: Set session variables
    $row = mysqli_fetch_array($result, MYSQLI_ASSOC);
    $_SESSION['user_id']=$row['user_id'];
    $_SESSION['username']=$row['username'];
    $_SESSION['email']=$row['email'];
    
           echo "success";
    
}
    }





#signup.php


 <?php
//<!--Start session-->
session_start();

$link = mysqli_connect("localhost", "dreamcha_login", "nikhil", "dreamcha_login");
if(mysqli_connect_error()){
    die('ERROR: Unable to connect:' . mysqli_connect_error()); 
}


//<!--Check user inputs-->
//    <!--Define error messages-->
$missingUsername = '<p><strong>Please enter a username!</strong></p>';
$missingEmail = '<p><strong>Please enter your email address!</strong></p>';
$invalidEmail = '<p><strong>Please enter a valid email address!</strong></p>';
$missingPassword = '<p><strong>Please enter a Password!</strong></p>';
$invalidPassword = '<p><strong>Your password should be at least 6 characters long and inlcude one capital letter and one number!</strong></p>';
$differentPassword = '<p><strong>Passwords don\'t match!</strong></p>';
$missingPassword2 = '<p><strong>Please confirm your password</strong></p>';
//    <!--Get username, email, password, password2-->
//Get username
if(empty($_POST["username"])){
    $errors .= $missingUsername;
}else{
    $username = filter_var($_POST["username"], FILTER_SANITIZE_STRING);   
}
//Get email
if(empty($_POST["email"])){
    $errors .= $missingEmail;   
}else{
    $email = filter_var($_POST["email"], FILTER_SANITIZE_EMAIL);
    if(!filter_var($email, FILTER_VALIDATE_EMAIL)){
        $errors .= $invalidEmail;   
    }
}
//Get passwords
if(empty($_POST["password"])){
    $errors .= $missingPassword; 
}elseif(!(strlen($_POST["password"])>6
         and preg_match('/[A-Z]/',$_POST["password"])
         and preg_match('/[0-9]/',$_POST["password"])
        )
       ){
    $errors .= $invalidPassword; 
}else{
    $password = filter_var($_POST["password"], FILTER_SANITIZE_STRING); 
    if(empty($_POST["password2"])){
        $errors .= $missingPassword2;
    }else{
        $password2 = filter_var($_POST["password2"], FILTER_SANITIZE_STRING);
        if($password !== $password2){
            $errors .= $differentPassword;
        }
    }
}
//If there are any errors print error
if($errors){
    $resultMessage = '<div class="alert alert-danger">' . $errors .'</div>';
    echo $resultMessage;
    exit;
}

//no errors

//Prepare variables for the queries
$username = mysqli_real_escape_string($link, $username);
$email = mysqli_real_escape_string($link, $email);
$password = mysqli_real_escape_string($link, $password);

$password = hash('sha256', $password);
//If username exists in the users table print error
$sql = "SELECT * FROM users WHERE username = '$username'";
$result = mysqli_query($link, $sql);
if(!$result){
    echo '<div class="alert alert-danger">Error running the query!</div>';

    exit;
}
$results = mysqli_num_rows($result);
if($results){
    echo '<div class="alert alert-danger">That username is already registered. Do you want to log in?</div>';  exit;
}
//If email exists in the users table print error
$sql = "SELECT * FROM users WHERE email = '$email'";
$result = mysqli_query($link, $sql);
if(!$result){
    echo '<div class="alert alert-danger">Error running the query!</div>'; exit;
}
$results = mysqli_num_rows($result);
if($results){
    echo '<div class="alert alert-danger">That email is already registered. Do you want to log in?</div>';  exit;
}

//Insert user details  in the users table

$sql = "INSERT INTO `users` (`username`, `email`, `password`) VALUES ('$username', '$email', '$password')";
$result = mysqli_query($link, $sql);
if(!$result){
    echo '<div class="alert alert-danger">There was an error inserting the users details in the database!</div>'; 
    exit;
}
else{
    echo "<div class='alert alert-success'>Thank for your registering!";
}
        
        ?>

