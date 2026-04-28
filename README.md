<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Artist Scheduler</title>

<style>
body {
    font-family: Arial;
    background: #f5f5f5;
    margin: 0;
}

header {
    background: #111;
    color: white;
    padding: 15px;
    font-size: 20px;
}

.container {
    padding: 20px;
}

input, button {
    padding: 8px;
    margin: 5px;
}

button {
    background: black;
    color: white;
    border: none;
    cursor: pointer;
}

table {
    width: 100%;
    margin-top: 20px;
    border-collapse: collapse;
    background: white;
}

th, td {
    padding: 10px;
    border: 1px solid #ddd;
    text-align: left;
}

th {
    background: #222;
    color: white;
}
</style>
</head>

<body>

<header>
🎤 Artist Scheduler
</header>

<div class="container">

<h3>添加航班</h3>

<input id="artist" placeholder="乐队 / 艺人名">
<input id="flight" placeholder="航班号">
<input id="time" type="datetime-local">
<button onclick="addFlight()">添加</button>

<table id="table">
<thead>
<tr>
<th>艺人</th>
<th>航班</th>
<th>到达时间</th>
</tr>
</thead>
<tbody></tbody>
</table>

</div>

<script>
let data = [];

function addFlight() {
    let artist = document.getElementById("artist").value;
    let flight = document.getElementById("flight").value;
    let time = document.getElementById("time").value;

    if (!artist || !flight || !time) {
        alert("请填完整");
        return;
    }

    data.push({
        artist,
        flight,
        time: new Date(time)
    });

    render();
}

function render() {
    data.sort((a, b) => a.time - b.time);

    let tbody = document.querySelector("#table tbody");
    tbody.innerHTML = "";

    data.forEach(item => {
        let row = `
        <tr>
            <td>${item.artist}</td>
            <td>${item.flight}</td>
            <td>${formatTime(item.time)}</td>
        </tr>
        `;
        tbody.innerHTML += row;
    });
}

function formatTime(date) {
    return date.toLocaleString();
}
</script>

</body>
</html>
