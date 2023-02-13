<script>
  import { createEventDispatcher } from "svelte";
  export let folder;
  const dispatch = createEventDispatcher();
  function setActiveFolder() {
    dispatch("setActiveFolder", {
      folder,
    });
  }
</script>

<div class="todo-item" on:click={setActiveFolder}>
  {folder.name}
</div>
