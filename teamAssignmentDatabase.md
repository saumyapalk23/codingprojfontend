<html>
<style>
        button {
        padding: 10px 20px;
        background-color: #161666;
        color: white;
        border: none;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
        margin: 8px 5px;    }
        input[type="text"] {
        padding: 10px;
        border: 2px solid blue;
        border-radius: 5px;
        font-size: 16px;
        width: 200px;
        margin: 8px 5px;
            }
                .input-container {
        display: flex;
        justify-content: center;
        margin-bottom: 20px;
    }
        #table-container th {
        color: white;
    }
    #table-container td {
    color: white;
}
        h1, h2, h3{
                color: #fff;
                position: center;
            }
       body {
            background-color: #01060d;
        }
                    </style>
<body>
        <h1 class="text-center m-5">Team Assignments</h1>
        <div class="table-responsive mx-5">
            <table id="table-container" class="table table-hover table-bordered border-secondary mb-5">
                <thead>
                    <tr>
                        <th scope="col">Assignment </th>
                        <th scope="col">Score</th>
                        <th scope="col">Ticket</th>
                        <th scope="col">Comments</th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="users">
                </tbody>
            </table>
        </div>
        <div>
            <h2 class="text-center m-5">ADD AN ASSIGNMENT</h2>
        <div class="input-container">
            <form id="create-user-form">
                <input type="text" id="assignment" placeholder="Assignment" name="assignment" required>
                <input type="text" id="score" placeholder="Score" name="score" required>
                <input type="text" id="ticket" placeholder="Ticket" name="ticket" required>
                <input type="text" id="comments" placeholder="Comments" name="comment" required>
                <button onclick="addUser()">Create</button>
            </form>
        </div>
        <script>
            const urlParams = new URLSearchParams(window.location.search);
            const teamId = urlParams.get('id');
            // prepare fetch urls
            const team_url = `https://mrr.rebeccaaa.tk/api/review/${teamId}`;
            const get_url = team_url + "/";
            const teamContainer = document.getElementById("users");
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
                        const assignment = document.createElement("td");
                        const score = document.createElement("td");
                        const ticket = document.createElement("td");
                        const comments = document.createElement("td");
                        // url containers
                        // accessing JSON values
                        assignment.innerHTML = user.assignment;
                        score.innerHTML = user.score;
                        ticket.innerHTML = user.ticket;
                        comments.innerHTML = user.comments;
                        tr.appendChild(assignment);
                        tr.appendChild(score);
                        tr.appendChild(ticket);
                        tr.appendChild(comments);
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
            function addUser() {
                const urlParams = new URLSearchParams(window.location.search);
                const teamId = urlParams.get('id');
                const assignment = document.getElementById('assignment').value;
                const score = document.getElementById('score').value;
                const ticket = document.getElementById('ticket').value;
                const comments = document.getElementById('comments').value;
                const user = {
                    assignment: assignment,
                    score: score,
                    ticket: ticket,
                    comments: comments,
                };
                const endpoint = `https://mrr.rebeccaaa.tk/api/review/post/${teamId}`;
                      fetch(endpoint, {
                    method: 'POST',
                    headers: {
                    'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(user)
                })
                    .then(response => response.json())
                    .then(data => {
                    console.log('User creation response:', data);
                    // Handle the response from the server
                    // You can perform further actions based on the response
                    })
            }        </script>