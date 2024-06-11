<script lang="ts">
  import { onMount } from "svelte"
  import Card from "./lib/Card.svelte"
  import type { Child } from "./types/types"
  import AddChildForm from "./lib/AddChildForm.svelte"

  let naughty: Child[] = []
  let nice: Child[] = []
  let newChild: Child = {
    name: "",
    tally: 0,
  }

  onMount(async () => {
    const res = await fetch("https://advent.sveltesociety.dev/data/2023/day-one.json")
    let data = (await res.json()) as { name: string; tally: number }[]

    data = data.sort((a, b) => Number(a.tally > b.tally))
    const index = data.findIndex((d) => d.tally > 0)

    naughty = data.slice(0, index)
    nice = data.slice(index)
  })

  function addChild() {
    if (newChild.tally > 0) {
      nice = [...nice, newChild].sort((a, b) => Number(a.tally > b.tally))
    } else {
      naughty = [...naughty, newChild].sort((a, b) => Number(a.tally > b.tally))
    }
  }
</script>

<main>
  <AddChildForm {addChild} bind:newChild />

  <div class="child-lists">
    <div class="list">
      <h1>Nice</h1>
      {#each nice as child}
        <Card {...child} />
      {/each}
    </div>

    <div class="list">
      <h1>Naughty</h1>
      {#each naughty as child}
        <Card {...child} />
      {/each}
    </div>
  </div>
</main>

<style>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .child-lists {
    display: flex;
    gap: 100px;
  }

  .list {
    display: flex;
    flex-direction: column;
  }
</style>
