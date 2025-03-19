<!DOCTYPE html>
<html>
<head>
    <title>X User Directory</title>
    <style>
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
    </style>
</head>
<body>
    <h1>X User Directory</h1>

    <form id="userForm">
        <label for="name">Name:</label><br>
        <input type="text" id="name" name="name"><br><br>

        <label for="xUsername">X Username (@):</label><br>
        <input type="text" id="xUsername" name="xUsername"><br><br>

        <label for="xProfileLink">X Profile Link:</label><br>
        <input type="text" id="xProfileLink" name="xProfileLink"><br><br>

        <button type="button" onclick="addUser()">Add User</button>
    </form>

    <br>

    <table id="userTable">
        <thead>
            <tr>
                <th>Name</th>
                <th>X Username</th>
                <th>X Profile Link</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>

    <script>
        function addUser() {
            const name = document.getElementById("name").value;
            const xUsername = document.getElementById("xUsername").value;
            const xProfileLink = document.getElementById("xProfileLink").value;

            if (name && xUsername && xProfileLink) {
                const user = { name, xUsername, xProfileLink };
                let users = JSON.parse(localStorage.getItem("xUsers")) || [];
                users.push(user);
                localStorage.setItem("xUsers", JSON.stringify(users));
                displayUsers();
                document.getElementById("userForm").reset(); //clear form
            } else {
                alert("Please fill in all fields.");
            }
        }

        function displayUsers() {
            const users = JSON.parse(localStorage.getItem("xUsers")) || [];
            const tableBody = document.getElementById("userTable").getElementsByTagName("tbody")[0];
            tableBody.innerHTML = ""; // Clear existing rows

            users.forEach(user => {
                const row = tableBody.insertRow();
                const nameCell = row.insertCell(0);
                const xUsernameCell = row.insertCell(1);
                const xProfileLinkCell = row.insertCell(2);

                nameCell.textContent = user.name;
                xUsernameCell.textContent = user.xUsername;
                xProfileLinkCell.innerHTML = `<a href="${user.xProfileLink}" target="_blank">${user.xProfileLink}</a>`;
            });
        }

        // Display users when the page loads
        displayUsers();
    </script>
</body>
</html>
