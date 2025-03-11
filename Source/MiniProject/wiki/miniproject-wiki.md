Building a **To-Do List App** is a great way to learn React. It covers fundamental concepts like **state management**, **event handling**, **component structure**, and **conditional rendering**. Below is a **step-by-step guide** to building a simple To-Do List App in React.

---

### **Step 1: Set Up Your React Project**

1. **Install Node.js**: Make sure you have Node.js installed on your machine.
2. **Create a React App**:
   ```bash
   npx create-react-app todo-app
   cd todo-app
   ```
3. **Start the Development Server**:
   ```bash
   npm start
   ```
   This will open your app at `http://localhost:3000`.

---

### **Step 2: Project Structure**

Organize your project structure like this:

```
todo-app/
├── src/
│   ├── components/
│   │   ├── TodoList.js
│   │   ├── TodoItem.js
│   │   └── AddTodo.js
│   ├── App.js
│   ├── App.css
│   └── index.js
├── public/
└── package.json
```

---

### **Step 3: Create the `TodoList` Component**

This component will manage the list of todos and render the `TodoItem` components.

1. Create a file `src/components/TodoList.js`:

   ```jsx
   import React, { useState } from "react";
   import TodoItem from "./TodoItem";
   import AddTodo from "./AddTodo";

   const TodoList = () => {
     const [todos, setTodos] = useState([]);

     const addTodo = (text) => {
       const newTodo = { id: Date.now(), text, completed: false };
       setTodos([...todos, newTodo]);
     };

     const toggleTodo = (id) => {
       setTodos(
         todos.map((todo) =>
           todo.id === id ? { ...todo, completed: !todo.completed } : todo
         )
       );
     };

     const deleteTodo = (id) => {
       setTodos(todos.filter((todo) => todo.id !== id));
     };

     return (
       <div className="todo-list">
         <h1>To-Do List</h1>
         <AddTodo addTodo={addTodo} />
         {todos.length === 0 ? (
           <p>No tasks to display. Add a task!</p>
         ) : (
           todos.map((todo) => (
             <TodoItem
               key={todo.id}
               todo={todo}
               toggleTodo={toggleTodo}
               deleteTodo={deleteTodo}
             />
           ))
         )}
       </div>
     );
   };

   export default TodoList;
   ```

---

### **Step 4: Create the `TodoItem` Component**

This component will render a single todo item.

1. Create a file `src/components/TodoItem.js`:

   ```jsx
   import React from "react";

   const TodoItem = ({ todo, toggleTodo, deleteTodo }) => {
     return (
       <div className="todo-item">
         <input
           type="checkbox"
           checked={todo.completed}
           onChange={() => toggleTodo(todo.id)}
         />
         <span
           style={{
             textDecoration: todo.completed ? "line-through" : "none",
             marginLeft: "10px",
           }}
         >
           {todo.text}
         </span>
         <button
           onClick={() => deleteTodo(todo.id)}
           style={{ marginLeft: "10px" }}
         >
           Delete
         </button>
       </div>
     );
   };

   export default TodoItem;
   ```

---

### **Step 5: Create the `AddTodo` Component**

This component will allow users to add new todos.

1. Create a file `src/components/AddTodo.js`:

   ```jsx
   import React, { useState } from "react";

   const AddTodo = ({ addTodo }) => {
     const [text, setText] = useState("");

     const handleSubmit = (e) => {
       e.preventDefault();
       if (text.trim()) {
         addTodo(text);
         setText("");
       }
     };

     return (
       <form onSubmit={handleSubmit}>
         <input
           type="text"
           value={text}
           onChange={(e) => setText(e.target.value)}
           placeholder="Add a new task"
         />
         <button type="submit">Add</button>
       </form>
     );
   };

   export default AddTodo;
   ```

---

### **Step 6: Update `App.js`**

Replace the content of `src/App.js` with the following:

```jsx
import React from "react";
import TodoList from "./components/TodoList";
import "./App.css";

function App() {
  return (
    <div className="App">
      <TodoList />
    </div>
  );
}

export default App;
```

---

### **Step 7: Add Basic Styling**

Update `src/App.css` to style your app:

```css
.App {
  text-align: center;
  padding: 20px;
}

.todo-list {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
}

.todo-item {
  display: flex;
  align-items: center;
  margin: 10px 0;
}

input[type="text"] {
  padding: 8px;
  margin-right: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
```

---

### **Step 8: Run the App**

1. Save all files.
2. Run the app:
   ```bash
   npm start
   ```
3. Open your browser and go to `http://localhost:3000`.

---

### **Step 9: Test the App**

- Add a new task using the input field.
- Mark tasks as completed by checking the checkbox.
- Delete tasks using the delete button.
- Verify that the app displays a message when no tasks are available.

---

### **Step 10: Optional Enhancements**

1. **Persist Data**: Use `localStorage` to save todos between page reloads.
2. **Edit Todos**: Add functionality to edit existing todos.
3. **Categories**: Add categories or tags for todos.
4. **Drag and Drop**: Implement drag-and-drop functionality for reordering tasks.
5. **Animations**: Add animations using libraries like Framer Motion.

---

By following these steps, you’ll have a fully functional To-Do List App built with React! This project will help you understand core React concepts and prepare you for more advanced projects. 🚀
