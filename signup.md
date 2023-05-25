<html>
    <head>
        <style>
            .bg-success {
                background-color: #17104e;
                }
            .btn-custom {
                color: #fff;
                background-color: #193387;
                border-color: #ffffff;
            }
            .btn-custom:hover, .btn-custom:focus, .btn-custom:active, .btn-custom.active, .open>.dropdown-toggle.btn-custom {
                color: #fff;
                background-color: #157347;
                border-color: #ffffff;
            }
            /* The message box is shown when the user clicks on the password field */
            #message {
                display:none;            
                position: relative;
            }       
        </style>
        <script>
            // const signup_url = "https://mrr.rebeccaaa.tk/api/team/post";
            const signup_url = "http://localhost:8023/api/team/post";
            function signup(){
                // get user input
                var bigteam = document.getElementById("bigteam").value;
                var email = document.getElementById("username").value;
                var pwd = document.getElementById("password").value;
                var names = document.getElementById("names").value;
                var period = document.getElementById("period").value;
                // confirm requirements, matching
                securePassword();
                validatePassword();
                // store data in JavaScript object
                let data = {bigteam: bigteam, email: email, names: names, period: period, password: pwd};
                console.log(data);
                const options = {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'include',
                    headers: {
                    'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(data), // convert to JSON
                };
                fetch(signup_url, options)
                .then(response => {
                // check for response errors
                if (response.status !== 201) {
                    error('POST API response failure: ' + response.status);
                    return;
                }
                // valid response
                console.log(data);
                // redirect on successful login
                window.location.href = "{{ site.baseurl }}/clubs";
                })
                // catch fetch errors (ie Nginx ACCESS to server blocked)
                .catch(err => {
                    error(err + " " + url);
                });
            }
            // Something went wrong with actions or responses
            function error(err) {
                // log as Error in console
                console.log(err);
            }
        </script>
    </head>
    <body>
        <div class="bg-success w-50 mx-auto m-5">
            <h2 class="text-light mx-5 pt-5">SIGN UP</h2>
            <!-- 'email' is mapped to 'username' for Spring Security -->
            <div class="mb-3 px-5">
                <label class="form-label" for="username">EMAIL</label>
                <input class="form-control" type="email" id="username" name="username" size="20" required>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="password">PASSWORD</label>
                <input class="form-control" type="password" id="password" name="password" size="20" required>
                <p id="message">Password must be a minmum of 8 characters, with at least one number, one uppercase, and one lowercase letter.</p>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="password">RETYPE PASSWORD</label>
                <input class="form-control" type="password" id="confirm_password" name="password" size="20" required>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="bigteam">BIG TEAM</label>
                <input class="form-control" type="text" id="bigteam" name="bigteam" size="250" required>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="names">NAMES</label>
                <input class="form-control" type="text" id="names" name="names" size="50" required>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="period">PERIOD</label>
                <input class="form-control" type="text" id="period" name="period" size="20" required>
            </div>
            <button class="btn btn-custom text-nowrap text-light my-3 mx-5" type="submit" onclick="signup()">Sign Up</button>
            <div class="text-light mx-5 pb-3">
                <p class="login">Already registered your club? <a class="text-light" href="{{ site.baseurl }}/login">Log In</a></p>
            </div>
        </div>
        <script>
             function validatePassword(){
                if(password.value != confirm_password.value){
                    confirm_password.setCustomValidity("Passwords Don't Match"); // form won't be submitted
                } else {
                    confirm_password.setCustomValidity(''); // matching
                }
                confirm_password.reportValidity();
            }
            // Get references to the password and confirm_password input fields
            const password = document.getElementById("password");
            const confirm_password = document.getElementById("confirm_password");
            // Add an event listener to the confirm_password field that calls validatePassword() on input
            confirm_password.addEventListener("input", validatePassword);
            var myInput = document.getElementById("password");
            // When the user clicks on the password field, show the message box
            myInput.onfocus = function() {
                document.getElementById("message").style.display = "block";
            }
            // When the user clicks outside of the password field, hide the message box
            myInput.onblur = function() {
                document.getElementById("message").style.display = "none";
            }
            // When the user starts to type something inside the password field
            password.addEventListener("input", securePassword);
            function securePassword() {
                // Validate lowercase letters
                var lowerCaseLetters = /[a-z]/g;
                if(myInput.value.match(lowerCaseLetters)) {  
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
                // Validate capital letters
                var upperCaseLetters = /[A-Z]/g;
                if(myInput.value.match(upperCaseLetters)) {  
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
                // Validate numbers
                var numbers = /[0-9]/g;
                if(myInput.value.match(numbers)) {  
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
                // Validate length
                if(myInput.value.length >= 8) {
                } else {
                    myInput.setCustomValidity("Password Doesn't Meet Requirements");
                    myInput.reportValidity();
                }
            }
        </script>
    </body>

</html>
