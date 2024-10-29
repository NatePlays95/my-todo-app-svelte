<script>
import { onMount } from "svelte";

let currentTask = $state("");
let taskList = $state([]);

// $inspect("currentTask:",currentTask);
// $inspect("taskList:",taskList);

onMount(() => {
    loadTaskList();
});

function addTask() {
    taskList.push(currentTask);
    currentTask = "";
    saveTaskList();
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


<div>
    <h1>To-Do List</h1>
    <div>
        <input
            type="text"
            bind:value={currentTask}
        >
        
        <button
            onclick={addTask}
        >Add Task</button>

    </div>

    {#each taskList as task, index}
        <div>
            {task}
            <button
                onclick={() => {deleteTask(index)}}
            >Delete</button>
        </div>
    {/each}
</div>