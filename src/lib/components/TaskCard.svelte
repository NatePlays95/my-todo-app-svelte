<script>
    import { fly } from 'svelte/transition';

    let { task, index, onDelete } = $props();

    function handleDelete() {
        if (onDelete) {
            onDelete(index);
        } else {
            console.log("no delete function bound! task of index: ", index);
        }
    }
</script>

<style>
    @import './TaskCard.css';
</style>

<div class="task-card" transition:fly={{ y: '-5rem', duration: 200 }}>
    {task}
    <button 
    class="task-card-delete-btn"
    onclick={handleDelete}
    >Delete</button>
</div>

