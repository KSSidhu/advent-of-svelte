<script lang="ts">
  import type { Child } from "../types/types"

  export let newChild: Child
  export let addChild = () => {}

  function handleTallyInput(e: { currentTarget: HTMLInputElement }) {
    newChild = {
      ...newChild,
      tally: Number(e.currentTarget.value),
    }
  }

  function handleNameInput(e: { currentTarget: HTMLInputElement }) {
    newChild = {
      ...newChild,
      name: e.currentTarget.value,
    }
  }
</script>

<form on:submit|stopPropagation|preventDefault={addChild}>
  <input title="Name" on:input={handleNameInput} />
  <input type="number" on:input={handleTallyInput} />

  <button type="submit">Save</button>
</form>

<style>
  form {
    display: flex;
    flex-direction: row;
    gap: 15px;
  }
</style>
