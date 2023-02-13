<script>
  import Todo from "./Todo.svelte";
  import FolderItem from "./FolderItem.svelte";
  let activeFolder;
  let newFolderName = "";
  let folders = [
    {
      id: 1,
      name: "folder1",
      todoList: [],
    },
  ];
  function handleSetActiveFolder(event) {
    activeFolder = event.detail.folder;
  }
  function addNewFolder() {
    if (event.key === "Enter") {
      folders.push({
        name: newFolderName,
        id: Math.max(...folders.map((folder) => folder.id)) + 1,
        todoList: [],
      });
      folders = folders;
    }
  }
  function handleUpdateActiveFolderTodoList(event) {
    folders.find((folder) => folder.id === activeFolder.id).todoList =
      event.detail.todoList;
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
    <FolderItem {folder} on:setActiveFolder={handleSetActiveFolder} />
  {/each}
</div>
<div class="folder-todolist">
  {#if activeFolder}
    <Todo
      folderName={activeFolder.name}
      bind:todoList={activeFolder.todoList}
    />
  {/if}
</div>
