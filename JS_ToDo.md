# Build a Simple To‑Do App — Step‑by‑Step (DIY)

> A student-friendly, copy‑pasteable guide that walks you through building a single‑file JavaScript To‑Do app. Each step explains *why* you do it, what JS concepts it teaches, and includes small exercises.

---

## Overview

This guide builds a tiny To‑Do app that demonstrates the core concepts of JavaScript used in real web apps:

* variables, arrays, objects
* functions
* loops and array methods
* conditions
* DOM manipulation
* events
* localStorage (persistence)

By the end you'll have a working app you can open in the browser and extend with extra features.

---

## Prerequisites

* A modern browser (Chrome, Firefox, Edge)
* A text editor (VS Code, Notepad++, Sublime, etc.)
* Basic HTML & CSS familiarity (not required, but helpful)

---

## Step 0 — Create a project folder

1. Create a new folder on your computer called `todo-js`.
2. Inside that folder create a file named `index.html`.

Why: Keeping files organized makes it easy to share and teach.

---

## Step 1 — Add the HTML skeleton

Open `index.html` and paste the following skeleton:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Simple To-Do App</title>
  <style>
    /* We'll add minimal CSS later — leave this empty for now */
  </style>
</head>
<body>
  <div class="app">
    <h1>To-Do App</h1>

    <form id="todo-form">
      <input id="todo-input" type="text" placeholder="Add a task" required />
      <button type="submit">Add</button>
    </form>

    <div class="filters">
      <button data-filter="all">All</button>
      <button data-filter="active">Active</button>
      <button data-filter="completed">Completed</button>
    </div>

    <ul id="todo-list"></ul>
    <div id="empty-msg" hidden>No tasks — add one above ✨</div>
    <div id="todo-count"></div>

    <button id="clear-completed">Clear completed</button>
    <button id="reset">Reset (clear all)</button>
  </div>

  <script>
    // JS will go here in later steps
  </script>
</body>
</html>
```

**What this teaches:** the HTML structure you'll manipulate with JavaScript later.

---

## Step 2 — Add simple CSS (optional, but helpful for students)

Inside the `<style>` tag copy this CSS to make the UI readable:

```css
body { font-family: system-ui, Arial; background:#f7f7fb; display:flex; align-items:center; justify-content:center; min-height:100vh; margin:0; }
.app { width:100%; max-width:480px; background:white; padding:16px; border-radius:10px; box-shadow:0 8px 20px rgba(0,0,0,0.06); }
form { display:flex; gap:8px; margin-bottom:12px; }
input { flex:1; padding:10px; border-radius:8px; border:1px solid #e2e6ef; }
button { padding:10px 12px; border-radius:8px; border:0; background:#3b82f6; color:white; cursor:pointer; }
ul { list-style:none; padding:0; margin:0; }
li { display:flex; align-items:center; justify-content:space-between; padding:8px 0; border-bottom:1px solid #f0f2f7; }
.small { font-size:12px; color:#6b7280; }
```

**Why:** Visual feedback helps students map actions to UI changes.

---

## Step 3 — Add the app state and DOM references (variables + arrays)

Inside the `<script>` tag, replace the comment with the code below. This creates the `todos` array (the app's memory) and saves references to HTML elements we will update.

```js
// App state
let todos = []; // array of todo objects
let currentFilter = 'all';

// DOM nodes
const form = document.getElementById('todo-form');
const input = document.getElementById('todo-input');
const list = document.getElementById('todo-list');
const countEl = document.getElementById('todo-count');
const emptyMsg = document.getElementById('empty-msg');
const filterButtons = document.querySelectorAll('.filters [data-filter]');
const clearCompletedBtn = document.getElementById('clear-completed');
const resetBtn = document.getElementById('reset');
```

**Tip:** `todos` is an array (list). Each element will be an object like `{id, title, completed}`.

---

## Step 4 — Utility helpers (id generator + save/load)

Below the previous code add helper functions for generating IDs and saving/loading to `localStorage`.

```js
function generateId() {
  return Date.now().toString(36) + Math.random().toString(36).slice(2,7);
}

function saveTodos() {
  localStorage.setItem('teaching_todos_v1', JSON.stringify(todos));
}

function loadTodos() {
  const raw = localStorage.getItem('teaching_todos_v1');
  if (raw) {
    try { todos = JSON.parse(raw); } catch(e) { todos = []; }
  } else {
    todos = [];
  }
}
```

**Why:** `localStorage` helps show persistence — tasks remain after refresh.

---

## Step 5 — Core actions: add, toggle, delete, clear, reset

Add functions that change the app state. Place this after the helpers.

```js
function addTodo(title) {
  title = title && title.trim();
  if (!title) return;
  const todo = { id: generateId(), title, completed: false, createdAt: Date.now() };
  todos.push(todo);
  saveTodos();
  render();
}

function toggleTodo(id) {
  todos = todos.map(t => t.id === id ? {...t, completed: !t.completed} : t);
  saveTodos();
  render();
}

function deleteTodo(id) {
  todos = todos.filter(t => t.id !== id);
  saveTodos();
  render();
}

function clearCompleted() {
  todos = todos.filter(t => !t.completed);
  saveTodos();
  render();
}

function resetAll() {
  todos = [];
  saveTodos();
  render();
}
```

**Google It:** See how arrays and objects are used together (objects inside an array). Explain immutability pattern in `map` and `filter`.

---

## Step 6 — Render the UI (DOM manipulation + loops)

Add the `render()` function after the actions. This function rebuilds the visible list.

```js
function render() {
  // Apply filter
  let visible = todos;
  if (currentFilter === 'active') visible = todos.filter(t => !t.completed);
  if (currentFilter === 'completed') visible = todos.filter(t => t.completed);

  // Clear list
  list.innerHTML = '';

  // Empty message
  emptyMsg.hidden = visible.length !== 0;

  // Build list items
  visible.forEach(todo => {
    const li = document.createElement('li');

    const left = document.createElement('div');
    left.style.display = 'flex';
    left.style.gap = '8px';
    left.style.alignItems = 'center';

    const checkbox = document.createElement('input');
    checkbox.type = 'checkbox';
    checkbox.checked = todo.completed;
    checkbox.addEventListener('change', () => toggleTodo(todo.id));

    const title = document.createElement('div');
    title.innerText = todo.title;
    if (todo.completed) title.style.textDecoration = 'line-through';

    left.appendChild(checkbox);
    left.appendChild(title);

    const del = document.createElement('button');
    del.innerText = 'Delete';
    del.addEventListener('click', () => deleteTodo(todo.id));

    li.appendChild(left);
    li.appendChild(del);
    list.appendChild(li);
  });

  // Update count
  const activeCount = todos.filter(t => !t.completed).length;
  countEl.innerText = `${activeCount} task${activeCount !== 1 ? 's' : ''} remaining`;
}
```

**Why:** This demonstrates DOM creation (`createElement`), loops (`forEach`), and class/text updates.

---

## Step 7 — Wire events (form submit, filters, clear/reset)

Add the event listeners that connect the UI to the functions above.

```js
// form submit
form.addEventListener('submit', e => {
  e.preventDefault();
  addTodo(input.value);
  input.value = '';
  input.focus();
});

// filters
filterButtons.forEach(btn => btn.addEventListener('click', function() {
  currentFilter = this.getAttribute('data-filter');
  filterButtons.forEach(b => b.style.opacity = '1');
  this.style.opacity = '0.6';
  render();
}));

// clear + reset
clearCompletedBtn.addEventListener('click', clearCompleted);
resetBtn.addEventListener('click', () => { if (confirm('Reset all tasks?')) resetAll(); });
```

**Google It:** Explain `preventDefault()` — why submitting a form normally reloads the page.

---

## Step 8 — Bootstrap: load and render

Finally, at the end of the script add the bootstrapping lines that load saved todos and render the first view:

```js
loadTodos();
render();
```

Open `index.html` in the browser. You should be able to add tasks, toggle them, delete them, filter and persist between refreshes.

---

## Mini exercises (practice)

1. **Edit a task:** add an "Edit" button that replaces the title with an input so students can modify and save a title. (teaches DOM updates + events)
2. **Priority:** add `priority: 'low'|'med'|'high'` to each object and show a colored dot. (objects + conditional styling)
3. **Sort:** add a button to sort tasks by created time or priority. (array sorting)
4. **Due date:** let students add a date and highlight overdue tasks in red. (Date and time handling)
5. **Save to server (optional advanced):** fetch API to save and load tasks from a mock server (teaches async + fetch + promises).

---

## Troubleshooting checklist

* If tasks don’t show: open DevTools Console (F12) and look for errors.
* If form refreshes on submit: ensure `e.preventDefault()` is called in the submit handler.
* If localStorage seems empty: check the key name and JSON.parse errors.

---

**Happy Learning!**
