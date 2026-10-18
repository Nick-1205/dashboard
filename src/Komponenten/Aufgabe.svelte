<script>
  import { createEventDispatcher } from "svelte";
  export let id, titel, inhalt, erledigt;
  let dispatch = createEventDispatcher();

  function update() {
    dispatch("update", { id, titel, inhalt, erledigt });
  }
</script>

<div class="aufgabe" class:erledigt>
  <h1 class="text-input">{titel}: {inhalt}</h1>
  <input
    class="checkbos-erledigt"
    type="checkbox"
    bind:checked={erledigt}
    on:change={() => update()}
  />
</div>

<style>
  .aufgabe {
    display: flex;
    align-items: center;
    padding: 5px;
  }
  .aufgabe.erledigt {
    background: lightgreen;
    text-decoration: line-through;
    transition: background-color 2s;
  }
  .text-input {
    flex-grow: 1;
    font-size: 1em;
  }
  .checkbos-erledigt {
    margin-left: 50px;
  }
</style>
