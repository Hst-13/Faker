<script>
  import { storeFE, fieldTypes } from "./store.js";

  export let id;

  function removeComponent() {
    $storeFE = $storeFE.filter(function (value, index, arr) {
      if (value.id != $storeFE[id].id) {
        if (value.id > id) value.id -= 1;
        return value;
      }
    });
    console.log($storeFE);
  }
</script>

<div class="field">
  <input class="newField" type="text" bind:value={$storeFE[id].name} />
  <select class="newType" name="fieldTypes" bind:value={$storeFE[id].type}>
    {#each fieldTypes as type}
      <option value={type}>{type}</option>
    {/each}
  </select>
  <button class="delete" on:click|preventDefault={removeComponent}>
    <svg xmlns="http://www.w3.org/2000/svg" height="48" width="48"
      ><path
        d="M13.05 42q-1.25 0-2.125-.875T10.05 39V10.5H8v-3h9.4V6h13.2v1.5H40v3h-2.05V39q0 1.2-.9 2.1-.9.9-2.1.9Zm21.9-31.5h-21.9V39h21.9Zm-16.6 24.2h3V14.75h-3Zm8.3 0h3V14.75h-3Zm-13.6-24.2V39Z"
      /></svg
    >
  </button>
</div>

<style>
  .newField {
    grid-area: newField;
  }

  .newType {
    grid-area: newType;
  }

  .delete {
    grid-area: newDel;
  }
</style>
