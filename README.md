# To-Do List (JavaScript)

A simple to-do list application built using HTML, CSS, and vanilla JavaScript. The application allows you to add, delete, and mark tasks as completed. Tasks are saved to `localStorage` so they persist even after the page is refreshed.

## Features

- **Add Task**: Add new tasks to the list.
- **Delete Task**: Remove tasks from the list.
- **Mark as Completed**: Mark tasks as completed by checking the checkbox.
- **Persistent Storage**: Tasks are saved to `localStorage`.

## File Structure
├── task/
│   ├── src/
│       ├── index.html
│       ├── css/
│           └── style.css
│       ├── fonts/
│           ├── Caveat-Regular.ttf
│           └── tangerine-regular.ttf
├── README.md

## Getting Started

### Prerequisites

- Modern web browser (like Chrome, Firefox)

### Running the Project

1. **Clone the repository**:
    ```sh
    git clone https://github.com/your-username/to-do-list-js.git
    cd to-do-list-js
    ```

2. **Open `index.html` in your browser**:
    ```sh
    open task/src/index.html
    ```
    OR simply double-click on `index.html`.

3. **Using the Application**:
    - Enter a task in the input box and click "Add Task" to add a task.
    - Check the checkbox next to a task to mark it as completed.
    - Click the delete button (trash icon) to remove a task.
    - Tasks will be saved automatically to `localStorage`.

## Customization

### Styles

- You can customize the styles in `css/style.css`.
- Fonts can be changed by replacing the font files in `fonts/`.

## Contributing

Feel free to make a pull request or open an issue to contribute to the project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## Acknowledgments

- Icons from [icons8](https://icons8.com)
- Fonts sourced locally
