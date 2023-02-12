<script>
    import Todo from "./Todo.svelte";
    let activeFolder;
    let newFolderName = "";
    let folders = [
      {
        id: 1,
        name: "folder1",
        todoList: [],
      }
    ];
    function setActiveFolder(folder) {
      activeFolder = folder;
    }
    function addNewFolder() {
      if (event.key === "Enter") {
        folders.push({
          name: newFolderName,
          id: Math.max(...folders.map(folder => folder.id)) + 1,
          todoList: [],
        });
        folders = folders;
      }
    }
    function handleUpdateActiveFolderTodoList(event) {
      folders.find(folder => folder.id === activeFolder.id).todoList = event.detail.todoList
    }
  </script>
  <div class="folders">
    <input
      type="text"
      placeholder="New folder ..."
      bind:value={newFolderName}
      on:keydown={addNewFolder}
    />
    {#each folders as folder}
      <div class="todo-item" on:click={() => setActiveFolder(folder)}>
        {folder.name}
      </div>
    {/each}
  </div>
  <div class="folder-todolist">
    {#if activeFolder}
      <Todo
        folderName={activeFolder.name}
        todoList={activeFolder.todoList}
        on:updateActiveFolderTodoList={handleUpdateActiveFolderTodoList}
      />
    {/if}
  </div>