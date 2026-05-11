<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Lista de Tarefas com Calendário</title>

  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f2f5;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      margin: 0;
    }

    .todo-container {
      background: white;
      padding: 20px;
      width: 450px;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    h1 {
      text-align: center;
      color: #333;
      margin-bottom: 20px;
    }

    .input-group {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 20px;
    }

    input,
    button {
      padding: 10px;
      border-radius: 6px;
      font-size: 16px;
    }

    input {
      border: 1px solid #ccc;
    }

    button {
      border: none;
      background: #28a745;
      color: white;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #218838;
    }

    ul {
      list-style: none;
      padding: 0;
    }

    li {
      background: #f8f9fa;
      margin-bottom: 10px;
      padding: 12px;
      border-radius: 8px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }

    .task-info {
      display: flex;
      flex-direction: column;
    }

    .task-date {
      font-size: 13px;
      color: #666;
      margin-top: 4px;
    }

    .complete {
      text-decoration: line-through;
      color: gray;
    }

    .actions {
      display: flex;
      gap: 5px;
    }

    .complete-btn {
      background: #007bff;
    }

    .delete-btn {
      background: #dc3545;
    }

    .complete-btn:hover {
      background: #0069d9;
    }

    .delete-btn:hover {
      background: #c82333;
    }
  </style>
</head>

<body>

  <div class="todo-container">

    <h1>📅 Lista de Tarefas</h1>

    <div class="input-group">
      <input type="text" id="taskInput" placeholder="Digite uma tarefa">

      <input type="date" id="taskDate">

      <button id="addTaskBtn">
        Adicionar Tarefa
      </button>
    </div>

    <ul id="taskList"></ul>

  </div>

  <script>
    const taskInput = document.getElementById("taskInput");
    const taskDate = document.getElementById("taskDate");
    const addTaskBtn = document.getElementById("addTaskBtn");
    const taskList = document.getElementById("taskList");

    function addTask() {

      const taskText = taskInput.value.trim();
      const dateValue = taskDate.value;

      if (taskText === "") {
        alert("Digite uma tarefa!");
        return;
      }

      const li = document.createElement("li");

      // Área das informações
      const taskInfo = document.createElement("div");
      taskInfo.classList.add("task-info");

      // Texto
      const span = document.createElement("span");
      span.textContent = taskText;

      // Data
      const dateSpan = document.createElement("span");
      dateSpan.classList.add("task-date");

      if (dateValue) {
        dateSpan.textContent = "Data: " + dateValue;
      } else {
        dateSpan.textContent = "Sem data definida";
      }

      taskInfo.appendChild(span);
      taskInfo.appendChild(dateSpan);

      // Botões
      const actions = document.createElement("div");
      actions.classList.add("actions");

      // Concluir
      const completeBtn = document.createElement("button");
      completeBtn.textContent = "✔";
      completeBtn.classList.add("complete-btn");

      completeBtn.addEventListener("click", () => {
        span.classList.toggle("complete");
      });

      // Excluir
      const deleteBtn = document.createElement("button");
      deleteBtn.textContent = "✖";
      deleteBtn.classList.add("delete-btn");

      deleteBtn.addEventListener("click", () => {
        li.remove();
      });

      actions.appendChild(completeBtn);
      actions.appendChild(deleteBtn);

      li.appendChild(taskInfo);
      li.appendChild(actions);

      taskList.appendChild(li);

      // Limpar campos
      taskInput.value = "";
      taskDate.value = "";
    }

    addTaskBtn.addEventListener("click", addTask);

    taskInput.addEventListener("keypress", function(event) {
      if (event.key === "Enter") {
        addTask();
      }
    });
  </script>

</body>
</html>
