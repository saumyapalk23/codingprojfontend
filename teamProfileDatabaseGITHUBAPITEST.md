<html>
    <body>
        <h1 class="text-center m-5 text-success">Team Profile</h1>
        <div class="table-responsive mx-5">
            <table id="table-container" class="table table-hover table-bordered border-secondary mb-5">
                <h1>Big Team: Mr. R</h1>
                <h2>Period 2</h2>
                <thead>
                    <tr>
                        <th scope="col">Student Name</th>
                        <th scope="col">Github ID</th>
                        <th scope="col">Blog</th>
                        <th scope="col">Github Insights</th>
                        <th scope="col">Github Commits</th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="clubs">
                </tbody>
            </table>
        </div>
        <div>
            <input type="text" id="username" placeholder="GitHub username">
            <button onclick="addStudent()">Add Student</button>
            <button onclick="fetchTotalCommits()">Fetch Total Commits</button>
        </div>
        <script>
            const userName = ;
            fetch('test.json')
            .then(response => response.json())
            .then(data => {
                let table = '<table><tr><th>Name</th><th>GitHub ID</th><th>Blog Link</th><th>GitHub Insights</th><th>GitHub Commits</th></tr>';
                data[0].individuals.forEach((student) => {
                table += <tr><td>${student.student}</td><td>${student['gh-id']}</td><td>${student.blog}</td><td>${student['gh-insights']}</td><td>${student['gh-commits']}</td></tr>;
                });
                table += '</table>';
                document.getElementById('table-container').innerHTML = table;
            })
            .catch(error => console.error(error));
        </script>
    </body>
</html>
