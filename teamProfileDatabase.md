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
                        <!-- <th scope="col">Staff Advisor</th>
                        <th scope="col">Meeting Time and Location</th>
                        <th scope="col">Additional Info</th>
                        <<th scope="col">Official Club?</th> -->
                        <!-- Links -->
                        <!-- <th scope="col">Meeting Minutes</th>
                        <th scope="col">Reviews</th> -->
                    </tr>
                    <tr>
                        <td>Rohan Gaikwad</td>
                        <td>RohanG326</td>
                        <td>link</td>
                        <td>30</td>
                        <td>200</td>
                    </tr>
                    <tr>
                        <td>Shreya Ahuja</td>
                        <td>shreya-ahujaa</td>
                        <td>link</td>
                        <td>32</td>
                        <td>198</td>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="clubs">
                </tbody>
            </table>
        </div>
        <script>
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
