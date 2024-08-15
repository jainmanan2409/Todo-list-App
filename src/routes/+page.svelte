<script lang="ts">

    type Todo = {
        done: boolean,
        task: string
    }
    let todos: Todo[] = [];
    let newTodo = '';
    
    function addTodos() {
        if(newTodo !== ''){
            todos = [...todos, { done: false, task: newTodo }];
            newTodo = '';
        }
    }

    function clearTodos() {
        todos = todos.filter((completed) => !completed.done);
    }

    function clearAllTodos() {
        todos = [];
    }

    $: remaining = todos.filter((completed) => !completed.done).length;
    
</script>

<div id="todo-app">
    <h1>Todo List</h1>
    <div class="board">
        <input
        type="text"
        placeholder="add todos to be completed!"
        bind:value={newTodo}
        on:keydown={(e) => e.key === 'Enter' && addTodos()}
        />
        <button on:click={addTodos}>Add</button>
    </div>

    <ul class="todolists">
        {#each todos as todo}
            <li class:done={todo.done}>
                <input
                type="checkbox"
                bind:checked={todo.done}
                />

                <input
                type="text"
                bind:value={todo.task}
                />
            </li>
        {/each}
    </ul>

    <p>{remaining} are pending!!</p>
    <button on:click={clearTodos}>Clear the completed Tasks</button>
    <button on:click={clearAllTodos}>Clear All Tasks</button>
</div>

<style>

#todo-app {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh; /* Full viewport height */
    width: 100vw;  /* Full viewport width */
    box-sizing: border-box;
    padding: 20px;
    background: #1b263b; /* Darker blue background for the app */
    border-radius: 10px; /* Rounded corners */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5); /* Stronger shadow for 3D effect */
    max-width: 500px; /* Optional max width for large screens */
    margin: auto;
}

h1 {
    color: #ffffff; /* White text color for the heading */
    margin-bottom: 20px;
    font-size: 24px; /* Larger font size for the heading */
}

.board {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
}

input[type="text"] {
    width: 100%;
    max-width: 400px; /* Optional max width for the input field */
    padding: 12px;
    font-size: 16px;
    border: 2px solid #3a4b5b; /* Dark blue border color */
    border-radius: 8px;
    background: #23395b; /* Darker blue background for input field */
    color: #e0e0e0; /* Light text color */
    box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.3); /* Inner shadow for input */
    outline: none;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

input[type="text"]:focus {
    border-color: #4b6a9b; /* Light blue border on focus */
    box-shadow: 0 0 8px rgba(75, 106, 155, 0.3); /* Glow effect on focus */
}

button {
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    border-radius: 8px;
    background-color: #4b6a9b; /* Light blue background */
    color: #ffffff; /* White text */
    cursor: pointer;
    transition: background-color 0.3s ease, transform 0.2s ease;
    margin: 10px;
}

button:hover {
    background-color: #3a4b5b; /* Darker blue on hover */
}

button:active {
    transform: scale(0.98); /* Slightly shrink button on click */
}

.todolists {
    list-style: none;
    padding: 0;
    width: 100%;
    max-width: 400px; /* Optional max width for the list */
}

li {
    display: flex;
    align-items: center;
    margin-bottom: 15px;
    justify-content: space-between;
    padding: 10px;
    border-radius: 8px;
    background-color: #1b263b; /* Dark blue background for list items */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.4); /* Subtle shadow for list items */
    transition: background-color 0.3s ease;
}

li:hover {
    background-color: #23395b; /* Slightly lighter blue on hover */
}

li.done input[type="text"] {
    text-decoration: none;
    color: #888; /* Gray text for completed tasks */
}

input[type="text"] {
    flex: 1;
    margin-left: 15px;
    padding: 10px;
    font-size: 16px;
    border: none;
    background: transparent; /* Transparent background */
    color: #e0e0e0; /* Light text color */
    outline: none;
}

input[type="checkbox"] {
    width: 20px;
    height: 20px;
    cursor: pointer;
    margin-right: 15px; /* Space between checkbox and text */
}

</style>