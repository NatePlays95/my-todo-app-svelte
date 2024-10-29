<script>
import { onMount } from "svelte";
import TaskCard from "$lib/components/TaskCard.svelte"

let currentTask = $state("");
let taskList = $state([]);

// $inspect("currentTask:",currentTask);
// $inspect("taskList:",taskList);

onMount(() => {
    loadTaskList();
});

function addTask() {
    if (currentTask.trim()) {
        taskList.push(currentTask);
        currentTask = "";
        saveTaskList();
    }
};

function deleteTask(index) {
    taskList = taskList.filter((_, i) => i !== index);
    saveTaskList();
};

function saveTaskList() {
    localStorage.setItem("taskList", JSON.stringify(taskList));
    // console.log("saved list: ", taskList);
};

function loadTaskList() {
    let savedTasksString = localStorage.getItem("taskList");
    if (savedTasksString) {
        // let newTasks = JSON.parse(savedTasksString); // TODO: lets try better security
        let savedData = JSON.parse(savedTasksString);
        taskList = savedData;
        // console.log("loaded list: ", savedData);
    }
};

</script>


<div class="app-container">
    <div class="task-column">
        <h2>To-Do List</h2>

        {#each taskList as task, index}
            <TaskCard
            {task} {index} onDelete={deleteTask}
            />
        {/each}

        <input
            class="add-task-input"
            type="text"
            bind:value={currentTask}
        >
        
        <button
            class="add-task-button"
            onclick={addTask}
        >Add Task</button>
    </div>
</div>