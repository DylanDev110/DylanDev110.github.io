<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Task Reminder</title>
  <style>
    /* Global Styles */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #121212;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      overflow: hidden; /* Hide body overflow until intro is done */
    }

    .container {
      width: 90%;
      max-width: 500px;
      text-align: center;
      display: none; /* Hide main content initially */
    }

    h1 {
      color: #fff;
      font-size: 36px;
      margin-bottom: 20px;
    }

    /* Task Input Section */
    .task-input {
      display: flex;
      justify-content: space-between;
      margin-bottom: 20px;
    }

    .task-input input {
      width: 80%;
      padding: 10px;
      background-color: #333;
      color: #fff;
      border: none;
      border-radius: 5px;
      font-size: 16px;
    }

    .task-input button {
      width: 18%;
      padding: 10px;
      background-color: #28a745;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .task-input button:hover {
      background-color: #218838;
    }

    /* Task List */
    .task-list {
      list-style: none;
      padding: 0;
    }

    .task-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px;
      margin-bottom: 10px;
      background-color: #333;
      border-radius: 5px;
    }

    .task-item span {
      font-size: 18px;
    }

    .task-item button {
      background-color: transparent;
      border: none;
      color: #f44336;
      cursor: pointer;
      font-size: 18px;
    }

    .task-item button:hover {
      color: #d32f2f;
    }

    .task-item.completed {
      text-decoration: line-through;
      color: #888;
    }

    /* Task Completed Button */
    .completed-btn {
      background-color: #4caf50;
      color: #fff;
      border: none;
      padding: 8px 15px;
      cursor: pointer;
    }

    .completed-btn:hover {
      background-color: #388e3c;
    }

    /* Intro Screen */
    .intro-screen {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.8);
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 10;
    }

    .intro-screen img {
      width: 150px;
      height: 150px;
      border-radius: 50%;
      margin-bottom: 20px;
    }

    .intro-screen p {
      color: #fff;
      font-size: 18px;
    }

  </style>
</head>
<body>
  <!-- Intro Screen -->
  <div id="introScreen" class="intro-screen">
    <img src="https://i.imgur.com/xl6xyVM.png" alt="Logo" id="introLogo" />
    <p>Made by Dylan.U</p>
  </div>

  <div class="container">
    <h1>Task Reminder</h1>
    <div class="task-input">
      <input type="text" id="taskInput" placeholder="Enter your task..." />
      <button onclick="addTask()">Add Task</button>
    </div>

    <ul id="taskList" class="task-list">
      <!-- Tasks will be dynamically added here -->
    </ul>
  </div>

  <script>
    // Function to hide the intro screen after a set time
    window.onload = function() {
      setTimeout(function() {
        const introScreen = document.getElementById('introScreen');
        introScreen.style.display = 'none'; // Hide intro screen
        const container = document.querySelector('.container');
        container.style.display = 'block'; // Show main content
        document.body.style.overflow = 'auto'; // Allow scrolling again
      }, 3500); // 3.5 seconds
    };

    // Function to add a task
    function addTask() {
      const taskInput = document.getElementById("taskInput");
      const taskText = taskInput.value.trim();

      if (taskText === "") return;

      const taskList = document.getElementById("taskList");

      const taskItem = document.createElement("li");
      taskItem.classList.add("task-item");

      taskItem.innerHTML = `
        <span>${taskText}</span>
        <div>
          <button class="completed-btn" onclick="toggleComplete(this)">Mark as Complete</button>
          <button onclick="deleteTask(this)">Delete</button>
        </div>
      `;

      taskList.appendChild(taskItem);
      taskInput.value = ""; // Clear the input
    }

    // Function to toggle the task's completion
    function toggleComplete(button) {
      const taskItem = button.closest(".task-item");
      taskItem.classList.toggle("completed");
      const statusButton = taskItem.querySelector(".completed-btn");
      if (taskItem.classList.contains("completed")) {
        statusButton.textContent = "Undo Completion";
      } else {
        statusButton.textContent = "Mark as Complete";
      }
    }

    // Function to delete a task
    function deleteTask(button) {
      const taskItem = button.closest(".task-item");
      taskItem.remove();
    }
  </script>
</body>
</html>
