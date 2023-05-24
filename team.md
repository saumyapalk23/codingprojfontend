<html>
    <body>
        <h1 class="text-center m-5 text-success">Scrum Teams</h1>
        <div class="table-responsive mx-5">
            <table class="table table-hover table-bordered border-secondary mb-5">
                <thead>
                    <tr>
                        <th scope="col">ID</th>
                        <th scope="col">Period</th>
                        <th scope="col">Big Team Name</th>
                        <th scope="col">Scrum Team Members</th>
                        <th scope="col">Assignments</th>
                        <th scope="col">Grades</th>
                    </tr>
                </thead>
                <tbody class="table-group-divider" id="team">
                </tbody>
            </table>
        </div>
        <script>
            // prepare fetch urls
            // const team_url = "http://localhost:8023/api/team";
            const team_url = "https://mrr.rebeccaaa.tk/api/team";
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
                    let i = 1;
                    for (const row of data) {
                        console.log(row);
                        // columns
                        const tr = document.createElement("tr");
                        const id = document.createElement("td");
                        const period = document.createElement("td");
                        const bigteam = document.createElement("td");
                        const names = document.createElement("td");
                        // url containers
                        const assignments = document.createElement("td");
                        // accessing JSON values
                        id.innerHTML = i;
                        bigteam.innerHTML = row.bigteam;
                        names.innerHTML = row.names;
                        period.innerHTML = row.period;
                        var assignments_str = "{{ site.baseurl }}/assignments?id=" + row.id;
                        assignments.innerHTML = '<a href="' + assignments_str +'">' + "Assignments for " + row.name + '</a>';
                        // add all columns to the row
                        tr.appendChild(id);
                        tr.appendChild(period);
                        tr.appendChild(bigteam);
                        tr.appendChild(names);
                        tr.appendChild(assignments);
                        // add row to table
                        teamContainer.appendChild(tr);
                        i++;
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
