**1. addTask()**
  
    function addTask() {
            console.log("Adding a task"); // Debug Logging Statement

            // Get task input and task list elements
            const taskInput = document.getElementById("input-task");
            const taskList = document.getElementById("task-list");

            // Check if taskInput is empty
            if (taskInput.value === "") {
                console.log("Task input is empty"); // Debug Logging

                alert("Please enter a task!"); // User Dialog
                return;
            } else {
                // When task input is not empty

                // Create new task list item
                const newTask = document.createElement("li");

                // Create checkbox for new task
                const checkbox = document.createElement("input");
                checkbox.type = "checkbox";

                // Add event listener to the checkbox to save tasks when it's checked
                checkbox.addEventListener("change", function () {
                    console.log("Task status changed"); // Debug Logging Statement
                    localStorage.setItem("tasks", JSON.stringify(getTasksAsArray()));
                });

                // Create text span for new task
                const taskText = document.createElement("span");
                taskText.className = "task";
                taskText.textContent = taskInput.value;

                // Create delete button for new task
                const deleteBtn = document.createElement("button");
                deleteBtn.className = "delete-btn";

                // Add event listener to the delete button
                deleteBtn.addEventListener("click", deleteTask);

                // Create image for delete button
                const img = document.createElement("img");
                img.src = "https://img.icons8.com/?size=100&id=102550&format=png&color=000000";
                img.alt = "Delete";
                deleteBtn.appendChild(img);

                // Assemble new task list item
                newTask.appendChild(checkbox);
                newTask.appendChild(taskText);
                newTask.appendChild(deleteBtn);
                taskList.appendChild(newTask);

                //Log the new task added
                console.log("New task added: " + taskInput.value);

                //Clear the input after adding a task
                taskInput.value = "";

                //save the tasks to local storage
                localStorage.setItem("tasks", JSON.stringify(getTasksAsArray()));
            }
        }
      


* **Purpose:** Adds a new task to the to-do list.
* **Process:**
    1. Retrieves the task's text from the input field (`input-task`).
    2. Validates if the task input is empty. If so, displays an alert and returns.
    3. Creates a new list item (`<li>`) element.
    4. Creates a checkbox (`<input type="checkbox">`) element within the new list item.
        - Adds an event listener to the checkbox to save tasks to local storage upon status change.
    5. Creates a text span (`<span>`) element to display the task's text.
    6. Creates a delete button (`<button>`) element.
        - Adds an event listener to the delete button to trigger the `deleteTask` function.
    7. Assembles the list item by appending the checkbox, text span, and delete button.
    8. Appends the new list item to the task list (`task-list`).
    9. Clears the input field.
    10. Saves the updated task list to local storage.
* **Logging:**
    - Logs debug messages:
        - "Adding a task" (when function starts)
        - "Task input is empty" (if the input is empty)
        - "New task added: [task text]" (when a new task is successfully added)
        - "Task status changed" (when checkbox state changes)



**2. `deleteTask(event)`**

    function deleteTask(event) {
      let taskToDelete = event.target;
      while (taskToDelete.tagName !== "LI") {
          taskToDelete = taskToDelete.parentElement;
      }

    console.log("Deleting task: " + taskToDelete.innerText);

    taskToDelete.remove();
    console.log("Task deleted successfully");

    localStorage.setItem("tasks", JSON.stringify(getTasksAsArray()));
    }

* **Purpose:** Deletes the task associated with the clicked delete button.
* **Process:**
    1. Identifies the parent list item (`<li>`) element of the clicked delete button.
    2. Logs the text content of the task being deleted.
    3. Removes the list item from the task list.
    4. Saves the updated task list to local storage.
* **Logging:**
    - Logs debug messages:
        - "Deleting task: [task text]" (before deletion)
        - "Task deleted successfully" (after successful deletion)


**3. `getTasksAsArray()`**

    function getTasksAsArray() {
        const taskList = document.getElementById("task-list").children;
        const tasksArray = []; 
    
        for (let task of taskList) {
            const taskText = task.querySelector("span.task").textContent;
            const completed = task.querySelector("input[type='checkbox']").checked;
    
            tasksArray.push({
                text: taskText,
                completed: completed
            });
        }
        console.log("Tasks array:", tasksArray);
        return tasksArray;
    }

* **Purpose:** Retrieves all tasks from the to-do list and returns them as an array of objects.
* **Process:**
    1. Gets all the children (`<li>`) elements of the task list.
    2. Iterates through each list item:
        - Extracts the task text and checkbox status (completed or not).
        - Creates an object representing the task: `{ text: [task text], completed: [boolean] }`.
        - Adds the task object to the `tasksArray`.
    3. Logs the content of the `tasksArray`.
    4. Returns the `tasksArray`.
* **Logging:**
    - Logs the content of the `tasksArray`.



**4. `loadTasks()`**

    function loadTasks() {
        console.log("Loading tasks from storage");
    
        const taskList = JSON.parse(localStorage.getItem("tasks")) || [];
        taskList.forEach((taskObject) => {
            const newTask = document.createElement("li");
            const checkbox = document.createElement("input");
            checkbox.type = "checkbox";
            checkbox.checked = taskObject.completed;
            checkbox.addEventListener("change", function() {
                localStorage.setItem("tasks", JSON.stringify(getTasksAsArray()));
            });
    
            const taskText = document.createElement("span");
            taskText.className = "task";
            taskText.textContent = taskObject.text;
    
            const deleteBtn = document.createElement("button");
            deleteBtn.className = "delete-btn";
            deleteBtn.addEventListener("click", deleteTask);
            const img = document.createElement("img");
            img.src = "https://img.icons8.com/?size=100&id=102550&format=png&color=000000";
            img.alt = "Delete";
            deleteBtn.appendChild(img);
    
            newTask.appendChild(checkbox);
            newTask.appendChild(taskText);
            newTask.appendChild(deleteBtn);
            document.getElementById("task-list").appendChild(newTask);
        });
    }

* **Purpose:** Loads tasks from local storage and populates the to-do list when the page loads.
* **Process:**
    1. Retrieves tasks from local storage (or initializes an empty array if no tasks are found).
    2. Iterates through the retrieved tasks:
        - Creates a new list item (`<li>`) for each task.
        - Creates a checkbox with the correct completion status.
            - Adds an event listener to save tasks upon status change.
        - Creates a text span to display the task text.
        - Creates a delete button with an event listener to trigger `deleteTask`.
        - Assembles the list item and appends it to the task list.
* **Logging:**
    - Logs "Loading tasks from storage" when the function starts.
