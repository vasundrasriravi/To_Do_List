# Ex03 To-Do List using JavaScript
## Date:

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Todo Application</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #90cee4;
      text-align: center;
    }
    header, footer {
      background-color: #1398db;
      color: white;
      padding: 15px;
      font-size: 20px;
      font-weight: bold;
    }
    .todo-container {
      max-width: 400px;
      background: white;
      margin: 30px auto;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      border: 2px solid #8ccaea;
    }
    .todo-input {
      width: 100%;
      padding: 10px;
      border: 2px solid #7fb8d1;
      border-radius: 4px;
      margin-bottom: 10px;
    }
    .filter-bar {
      margin-bottom: 10px;
    }
    .filter-bar button {
      padding: 5px 10px;
      margin: 0 5px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      background: #6fc897;
      color: #1a191b;
    }
    .filter-bar button.active {
      background: #6fc897;
      color: rgb(27, 25, 25);
    }
    .todo-list {
      list-style: none;
      padding: 0;
    }
    .todo-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px;
      margin-bottom: 5px;
      background-color: #b5f0f0;
      border: 1px solid #ddd;
      border-radius: 4px;
    }
    .todo-item.completed span {
      text-decoration: line-through;
      color: gray;
    }
    .todo-buttons button {
      padding: 5px 10px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      margin-left: 5px;
    }
    .complete-btn { background-color: #6fc897; color: rgb(23, 22, 22); }
    .delete-btn   { background-color: #e20e55; color: white; }
  </style>
</head>
<body>
  <header>Todo Application</header>
  <div class="todo-container">
    <h2>To-Do List ✅</h2>
    <input
      type="text"
      id="todo-input"
      class="todo-input"
      placeholder="Add a new task"
    />
    <div class="filter-bar">
      <button data-filter="all"    class="active">All</button>
      <button data-filter="active">Active</button>
      <button data-filter="completed">Completed</button>
    </div>
    <ul id="todo-list" class="todo-list"></ul>
  </div>
  <footer>&copy; 2025 VASUNDRA SRI R (212222230168) | All rights reserved.</footer>

  <script>
    // DOM refs
    const todoInput = document.getElementById('todo-input');
    const todoList  = document.getElementById('todo-list');
    const filterBtns = document.querySelectorAll('.filter-bar button');

    // State
    let todos = [];      // { id, text, completed }
    let filter = 'all';  // current filter

    // Init
    loadTodos();
    renderTodos();

    // Events
    todoInput.addEventListener('keypress', e => {
      if (e.key === 'Enter') {
        e.preventDefault();
        addTodo();
      }
    });
    filterBtns.forEach(btn =>
      btn.addEventListener('click', () => {
        filterBtns.forEach(b => b.classList.toggle('active', b === btn));
        filter = btn.dataset.filter;
        renderTodos();
      })
    );

    // CRUD
    function addTodo() {
      const text = todoInput.value.trim();
      if (!text) return;
      todos.push({ id: Date.now(), text, completed: false });
      saveTodos();
      renderTodos();
      todoInput.value = '';
    }

    function toggleComplete(id) {
      todos = todos.map(t =>
        t.id === id ? { ...t, completed: !t.completed } : t
      );
      saveTodos();
      renderTodos();
    }

    function deleteTodo(id) {
      todos = todos.filter(t => t.id !== id);
      saveTodos();
      renderTodos();
    }

    // Persistence
    function loadTodos() {
      const data = localStorage.getItem('todos');
      if (data) {
        try { todos = JSON.parse(data); }
        catch { todos = []; }
      }
    }
    function saveTodos() {
      localStorage.setItem('todos', JSON.stringify(todos));
    }

    // Render with filter
    function renderTodos() {
      todoList.innerHTML = '';
      todos
        .filter(t => {
          if (filter === 'active')    return !t.completed;
          if (filter === 'completed') return t.completed;
          return true;
        })
        .forEach(({ id, text, completed }) => {
          const li = document.createElement('li');
          li.className = `todo-item${completed ? ' completed' : ''}`;

          const span = document.createElement('span');
          span.textContent = text;

          const btns = document.createElement('div');
          btns.className = 'todo-buttons';

          const comp = document.createElement('button');
          comp.textContent = completed ? 'Undo' : 'Complete';
          comp.className = 'complete-btn';
          comp.onclick = () => toggleComplete(id);

          const del = document.createElement('button');
          del.textContent = 'Delete';
          del.className = 'delete-btn';
          del.onclick = () => deleteTodo(id);

          btns.append(comp, del);
          li.append(span, btns);
          todoList.appendChild(li);
        });
    }
  </script>
</body>
</html>
```

## OUTPUT


## RESULT
The program for creating To-do list using JavaScript is executed successfully.
