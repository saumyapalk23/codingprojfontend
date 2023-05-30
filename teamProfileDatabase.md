<html>
<style>
    #table-container th {
        color: white;
    }
    #table-container td {
        color: white;
    }
    h1, h2, h3 {
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
            <tbody class="table-group-divider" id="clubs"></tbody>
        </table>
    </div>
    <script>
        fetch('test.json')
            .then(response => response.json())
            .then(data => {
                let table = '';
                data[0].individuals.forEach((student) => {
                    table += `<tr>
                        <td>${student.student}</td>
                        <td>${student['gh-id']}</td>
                        <td>${student.blog}</td>
                        <td>${student['gh-insights']}</td>
                        <td>${student['gh-commits']}</td>
                    </tr>`;
                });
                document.querySelector('#table-container tbody').innerHTML = table;
            })
            .catch(error => console.error(error));
    </script>
</body>

</html>
