<html>
<head>
<style>
        #table-container th {
        color: white;
    }
      body {
            background-color: #01060d;
        }
            table {
                border-collapse: collapse;
                border-radius: 20px;
                overflow: hidden;
            }
            th, td {
                padding: 20px;
                text-align: center;
                border: 20px solid blue;
            }
            h1, h2 {
                color: #fff;
            }
        .white-text {
            color: white;
        }
    input[type="text"] {
        padding: 10px;
        border: 2px solid blue;
        border-radius: 5px;
        font-size: 16px;
        width: 200px;
        margin: 8px 5px;
            }
    button {
        padding: 10px 20px;
        background-color: #161666;
        color: white;
        border: none;
        border-radius: 5px;
        font-size: 16px;
        cursor: pointer;
        margin: 8px 5px;    }
            .input-container {
        display: flex;
        justify-content: center;
        margin-bottom: 20px;
    }
</style>
    <body>
        <h1 class="text-center m-5">Team Profile</h1>
        <div class="table-responsive mx-5">
            <table id="table-container" class="table table-hover table-bordered border-secondary mb-5">
                <h1>Big Team: Mr. R</h1>
                <h2>Period 2</h2>
                <thead>
                    <tr>
                        <th scope="col"> Student Name </th>
                        <th scope="col"> Last Github Update </th>
                        <th scope="col"> Github ID </th>
                        <!-- <th scope="col">Blog</th>
                        <th scope="col">Github Insights</th> -->
                        <th scope="col"> Number of Public Repos </th>
                        <!--<td id="username-commits"></td>-->
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="students">
                </tbody>
            </table>
        </div>
        <div>
        <div class="input-container">
            <!--<input type="text" id="name" placeholder="Full Name">-->
            <input type="text" id="username" placeholder="GitHub Username">
            <button onclick="addStudent()">Add Student</button>
            <!--<button onclick="fetchTotalCommits()">Fetch Total Commits</button> -->
        </div>
        <script>
            function addStudent() {
                // const tableBody = document.getElementById('students');
                // const username = document.getElementById('username').value;
                // const newRow = document.createElement('tr');
                // const nameCell = document.createElement('td');
                var tableBody = document.getElementById('students');
                // var nameInput = document.getElementById("name");
                var userNameInput = document.getElementById("username");
                //addToTable
                var newRow = tableBody.insertRow();
                var studentNameCell = newRow.insertCell();
                studentNameCell.textContent = " ";
                studentNameCell.classList.add("white-text");
                var lastUpdateCell = newRow.insertCell();
                lastUpdateCell.textContent = " ";
                lastUpdateCell.classList.add("white-text");
                var userNameCell = newRow.insertCell();
                userNameCell.textContent = userNameInput.value;
                userNameCell.classList.add("white-text");
                var totalCommitsCell = newRow.insertCell();
                totalCommitsCell.textContext = 0;
                totalCommitsCell.classList.add("white-text");
                var buttonCell = newRow.insertCell();
                var fetchCommitsButton = document.createElement('button');
                fetchCommitsButton.textContent = 'Fetch Data';
                fetchCommitsButton.onclick = function() {
                fetchTotalCommits(userNameInput.value, studentNameCell, totalCommitsCell, lastUpdateCell);
                };
                buttonCell.appendChild(fetchCommitsButton);
                //reset fields
                //nameInput.value = '';
                usernameInput.value = '';
                // row.insertCell(0).innerHTML = name.value;
                // row.insertCell(1).innerHTML = userName.value;
                // row.insertCell(2).innerHTML = 0;
        }
        function fetchTotalCommits(username, studentCell, commitsCell, lastupdateCell) {
            const url = `https://api.github.com/users/${username}`;
            // var tableBody = document.getElementById('students');
            // var numRows = tableBody.getElementsByTagName('tr');
            fetch(url)
    .then(response => response.json())
    .then(data => {
      commitsCell.textContent = data.public_repos;
                                commitsCell.classList.add("white-text");
      studentCell.textContent = data.name;
                                studentCell.classList.add("white-text");
    lastupdateCell.textContent = data.updated_at;
                            lastupdateCell.classList.add("white-text");
    })
    .catch(error => console.error(error));
        }
        </script>
