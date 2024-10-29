<script>
import { onMount } from "svelte";

let currentTask = $state("");
let taskList = $state([]);

$inspect("currentTask:",currentTask);
$inspect("taskList:",taskList);

function addTask() {
    taskList.push(currentTask);
    currentTask = "";
};

function deleteTask(index) {
    taskList = taskList.filter((_, i) => i !== index);
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