<html>
    <body>
        <h1 class="text-center m-5 text-success">Team Profile</h1>
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
            <!--<input type="text" id="name" placeholder="Full Name">-->
            <input type="text" id="username" placeholder="GitHub Username">
            <button onclick="addStudent()">Add Student</button>
            <!--<button onclick="fetchTotalCommits()">Fetch Total Commits</button> -->
			<input type="text" id="repo" placeholder="Repository Name">
			<button onclick="addRepo()">Add Repository</button>
        </div>
		<script src="config2.js"></script>
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
                var lastUpdateCell = newRow.insertCell();
                lastUpdateCell.textContent = " ";
                var userNameCell = newRow.insertCell();
                userNameCell.textContent = userNameInput.value;
                var totalCommitsCell = newRow.insertCell();
                totalCommitsCell.textContext = 0;
                var buttonCell = newRow.insertCell();
                var fetchCommitsButton = document.createElement('button');
                fetchCommitsButton.textContent = 'Fetch Data';
                fetchCommitsButton.onclick = function() {
                fetchGitData(userNameInput.value, studentNameCell, totalCommitsCell, lastUpdateCell);
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
			var tableBody = document.getElementById('students');
			var rows = tableBody.getElementsByTagName('tr');
			var newHeaderCell = document.createElement('th');
			newHeaderCell.textContent = repoName;
			tableHeader.appendChild(newHeaderCell);
			var newHeaderCell = document.createElement('th');
			newHeaderCell.textContent = repoName;
			tableHeader.appendChild(newHeaderCell);
			//const url = `https://api.github.com/repos/rebecca-123/${repoName}/commits?author=MAnn223`;
		}
        function fetchGitData(username, studentCell, commitsCell, lastupdateCell) {
            const url = `https://api.github.com/users/${username}`;
            // var tableBody = document.getElementById('students');
            // var numRows = tableBody.getElementsByTagName('tr');
            fetch(url)
				.then(response => response.json())
				.then(data => {
				  commitsCell.textContent = data.public_repos;
				  studentCell.textContent = data.name;
				lastupdateCell.textContent = data.updated_at;
				})
				.catch(error => console.error(error));
		const repoName = document.getElementById("repo").value;
		const token = githubToken;
		const headers = {
        Authorization: `Bearer ${token}`
        };
		const repoUrl = `https://api.github.com/repos/rebecca-123/${repoName}/commits?author=${username}`
		if (repoName !== '') {		
			fetch(repoUrl, { headers })
			.then(response => response.json())
			.then(repoData => {
			const totalCommits = repoData.length; //endpoint returns all commits, loop through 
			const row = commitsCell.parentNode;
			const commitsIndex = Array.from(commitsCell.parentNode.children).indexOf(commitsCell);
		     const repoCommitsCell = commitsCell.parentNode.insertCell(commitsIndex + 1);
			  repoCommitsCell.textContent = totalCommits;
			})
		.catch(error => console.error(error));
					}
	}
            // const userName = ;
            // fetch('test.json')
            // .then(response => response.json())
            // .then(data => {
            //     let table = '<table><tr><th>Name</th><th>GitHub ID</th><th>Blog Link</th><th>GitHub Insights</th><th>GitHub Commits</th></tr>';
            //     data[0].individuals.forEach((student) => {
            //     table += <tr><td>${student.student}</td><td>${student['gh-id']}</td><td>${student.blog}</td><td>${student['gh-insights']}</td><td>${student['gh-commits']}</td></tr>;
            //     });
            //     table += '</table>';
            //     document.getElementById('table-container').innerHTML = table;
            // })
            // .catch(error => console.error(error));
        </script>
    </body>
</html>



