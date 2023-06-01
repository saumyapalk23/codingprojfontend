<html>
    <body>
        <h1 class="text-center m-5 text-success">Team Profile</h1>
        <div class="table-responsive mx-5">
            <table id="table-container" class="table table-hover table-bordered border-secondary mb-5">
                <thead>
                    <tr>
                        <th scope="col"> Student Name </th>
                        <th scope="col"> Last Github Update </th>
                        <th scope="col"> Github ID </th>
                        <th scope="col"> Number of Public Repos </th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="students">
                </tbody>
            </table>
        </div>
        <div>
            <input type="text" id="username" placeholder="GitHub Username">
            <button onclick="addStudent()">Add Student</button>
            <input type="text" id="repo" placeholder="Repository Name">
            <button onclick="addRepo()">Add Repository</button>
        </div>
        <script src="config.js"></script>
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
            function addRepo(){
                var repoNameInput = document.getElementById("repo")
                var repoName = repoNameInput.value;
                var tableHeader = document.querySelector('#table-container thead tr');
                var newHeaderCell = document.createElement('th');
                newHeaderCell.textContent = repoName;
                tableHeader.appendChild(newHeaderCell);
                var tableBody = document.getElementById('students');
                var rows = tableBody.getElementsByTagName('tr');
                for (var i = 0; i < rows.length; i++) {
                    var newRepoCell = rows[i].insertCell();
                    newRepoCell.textContent = " ";
                }
            }
            function fetchGitData(username, studentCell, reposCell, lastUpdateCell) {
                const url = `https://api.github.com/users/${username}`;
                fetch(url)
                    .then(response => response.json())
                    .then(data => {
                        reposCell.textContent = data.public_repos;
                        studentCell.textContent = data.name;
                        lastUpdateCell.textContent = data.updated_at;
                    })
                    .catch(error => console.error(error));
                const repoName = document.getElementById("repo").value;
                if (repoName !== '') {		
                    fetch(`https://api.github.com/repos/${username}/${repoName}/commits`)
                        .then(response => response.json())
                        .then(repoData => {
                            const totalCommits = repoData.length;
                            var tableBody = document.getElementById('students');
                            var rows = tableBody.getElementsByTagName('tr');
                            var commitsIndex = Array.from(rows[0].children).length - 1;
                            for (var i = 0; i < rows.length; i++) {
                                var repoCommitsCell = rows[i].insertCell(commitsIndex);
                                repoCommitsCell.textContent = totalCommits;
                            }
                        })
                        .catch(error => console.error(error));
                }
            }
        </script>
    </body>
</html>
