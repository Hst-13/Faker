<script>
  import Field from "./Field.svelte";
  import { generateData } from "./generate";
  import { storeFE, idIncrement, dataFormats } from "./store.js";

  $storeFE = [{ id: 0, name: "Field 0", type: "Word" }];
  $idIncrement = 1;
  let dataFormat = "JSON";
  let noOfRows = 1;

  function addField() {
    var l = $storeFE.length; // get our current items list count
    $storeFE[l] = {
      id: l,
      name: `Field ${$idIncrement}`,
      type: "Word",
    };
    console.log($storeFE);
    $idIncrement++;
  }

  let schema = [];
  $: schema = $storeFE;
  function handleSubmit() {
    generateData(schema, dataFormat, noOfRows);
  }
</script>

<main>
  <div class="pageTitle">
    <p id="faker">Faker</p>
    <p id="subtitle">Fake Data Generator</p>
  </div>

  <div class="jumbotron">
    <div class="bar">
      <p id="fieldHead">Field</p>
      <p id="typeHead">Type</p>
      <p id="delHead">Delete</p>
    </div>

    <form id="inputForm" on:submit|preventDefault={handleSubmit}>
      {#each $storeFE as field}
        <svelte:component this={Field} id={field.id} />
      {/each}

      <button class="add" on:click|preventDefault={addField}>
        <svg xmlns="http://www.w3.org/2000/svg" height="24" width="24"
          ><path d="M10.85 19.15v-6h-6v-2.3h6v-6h2.3v6h6v2.3h-6v6Z" /></svg
        > <span>Add Field</span>
      </button>

      <div class="submission">
        <div class="data">
          <div>
            <label for="format">Data Format :</label>
            <select
              name="dataFormat"
              class="dataFormat"
              bind:value={dataFormat}
            >
              {#each dataFormats as format}
                <option value={format}>{format}</option>
              {/each}
            </select>
          </div>
          <div>
            <label for="rows">No. of Rows :</label>
            <input
              type="number"
              class="rows"
              min="1"
              max="5000"
              bind:value={noOfRows}
            />
          </div>
        </div>
        <input id="submit" type="submit" value="Generate Data" />
      </div>
    </form>
  </div>
</main>

<style>
  #fieldHead {
    grid-area: fieldHead;
  }

  #typeHead {
    grid-area: typeHead;
  }

  #delHead {
    grid-area: delHead;
  }
</style>
