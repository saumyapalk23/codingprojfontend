<html>
<style>
        #table-container th {
        color: white;
    }
    #table-container td {
    color: white;
}
        h1, h2, h3{
                color: #fff;
            }
       body {
            background-color: #01060d;
        }
                    </style>
<body>
        <h1 class="text-center m-5">Team Profile</h1>
        <div class="table-responsive mx-5">
            <table id="table-container" class="table table-hover table-bordered border-secondary mb-5">
                <thead>
                    <tr>
                        <th scope="col">Student Name </th>
                        <th scope="col">Github ID</th>
                        <th scope="col">Blog</th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="clubs">
                </tbody>
            </table>
        </div>
        <script>
            const urlParams = new URLSearchParams(window.location.search);
            const teamId = urlParams.get('id');
            // prepare fetch urls
            const team_url = `https://mrr.rebeccaaa.tk/api/team/${teamId}`;
            const get_url = team_url + "/";
            const teamContainer = document.getElementById("team");
            // prepare fetch GET options
            const options = {
                method: 'GET', // *GET, POST, PUT, DELETE, etc.
                // mode: 'cors', // no-cors, *cors, same-origin
                cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
                // credentials: 'same-origin', // include, same-origin, omit
                headers: {
                'Content-Type': 'application/json'
                // 'Content-Type': 'application/x-www-form-urlencoded',
                },
            };
            // fetch the API
            fetch(get_url, options)
                // response is a RESTful "promise" on any successful fetch
                .then(response => {
                // check for response errors
                if (response.status !== 200) {
                    error('GET API response failure: ' + response.status);
                    return;
                }
                // valid response will have JSON data
                response.json().then(data => {
                    const users = data.names;
                    for (const user of users) {
                        console.log(user);
                        // columns
                        const tr = document.createElement("tr");
                        const name = document.createElement("td");
                        const ghid = document.createElement("td");
                        const blog = document.createElement("td");
                        // url containers
                        // accessing JSON values
                        name.innerHTML = user.name;
                        ghid.innerHTML = user.githubId;
                        blog.innerHTML = user.blog;
                        tr.appendChild(name);
                        tr.appendChild(ghid);
                        tr.appendChild(blog);
                        // add row to table
                        teamContainer.appendChild(tr);
                    }
                })
            })
            // catch fetch errors (ie Nginx ACCESS to server blocked)
            .catch(err => {
                error(err + " " + get_url);
            });
            // Something went wrong with actions or responses
            function error(err) {
                // log as Error in console
                console.error(err);
                // append error to resultContainer
                const tr = document.createElement("tr");
                const td = document.createElement("td");
                td.innerHTML = err;
                tr.appendChild(td);
                teamContainer.appendChild(tr);
            }
        </script>
    </body>
</html>
