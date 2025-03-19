<!DOCTYPE html>
<html>
<head>
    <title>X User Directory</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 20px;
            background-color: #f0f8ff;
            color: #333;
        }

        h1 {
            text-align: center;
            color: #2c3e50;
            margin-bottom: 20px;
            animation: fadeIn 1s ease-out; /* Fade-in animation */
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        form {
            background-color: #fff;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            margin-bottom: 25px;
            border: 1px solid #e0e0e0;
            transition: transform 0.3s ease; /* Subtle hover effect */
        }

        form:hover {
            transform: translateY(-5px);
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #555;
        }

        input[type="text"] {
            width: calc(100% - 22px);
            padding: 12px;
            margin-bottom: 20px;
            border: 1px solid #d1d1d1;
            border-radius: 6px;
            box-sizing: border-box;
            font-size: 16px;
            transition: border-color 0.3s ease; /* Input focus effect */
        }

        input[type="text"]:focus {
            border-color: #3498db;
        }

        button {
            background-color: #3498db;
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            width: 100%;
            font-size: 16px;
            font-weight: 600;
            transition: background-color 0.3s ease, transform 0.2s ease; /* Hover effect */
        }

        button:hover {
            background-color: #2980b9;
            transform: scale(1.05);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            border: 1px solid #e0e0e0;
            animation: slideIn 1s ease-out; /* Slide-in animation */
        }

        @keyframes slideIn {
            from { transform: translateX(-50px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        th, td {
            border: 1px solid #e0e0e0;
            padding: 15px;
            text-align: left;
            font-size: 16px;
        }

        th {
            background-color: #ecf0f1;
            font-weight: 600;
            color: #333;
        }

        a {
            color: #3498db;
            text-decoration: none;
            transition: color 0.3s ease;
        }

        a:hover {
            text-decoration: underline;
            color: #2980b9;
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
        // JavaScript remains the same
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
