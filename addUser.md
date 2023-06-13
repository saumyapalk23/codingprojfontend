<html>
    <head>
        <style>
        body {
            background-color: #01060d;
        }
            .bg-color{
                background-color: #161666;
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
            const urlParams = new URLSearchParams(window.location.search);
            const teamId = urlParams.get('id');
            const signup_url = `https://mrr.rebeccaaa.tk/api/team/addMember/${teamId}`;
            function addUser(){
                // get user input
                var name = document.getElementById("name").value;
                var ghid = document.getElementById("ghid").value;
                var blog = document.getElementById("blog").value;
                // store data in JavaScript object
                let data = {"name": name, "githubId": ghid, "blog": blog};
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
        <div class="bg-color w-50 mx-auto m-5">
            <h2 class="text-light mx-5 pt-5">Add User to Team</h2>
            <!-- 'email' is mapped to 'username' for Spring Security -->
            <div class="mb-3 px-5">
                <label class="form-label" for="name">Name</label>
                <input class="form-control" type="text" id="name" name="name" size="250" required>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="names">Github ID</label>
                <input class="form-control" type="text" id="ghid" name="ghid" size="50" required>
            </div>
            <div class="mb-3 px-5">
                <label class="form-label" for="period">Blog link</label>
                <input class="form-control" type="text" id="blog" name="blog" size="20" required>
            </div>
            <button class="btn btn-custom text-nowrap text-light my-3 mx-5" type="submit" onclick="addUser()">Add User</button>
        </div>
    </body>

</html>