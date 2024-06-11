<script lang="ts">
  export let name: string
  export let tally: number
</script>

<div>
  <p>{name}</p>
  <p>{tally}</p>
</div>

<style>
  div {
    display: flex;
    gap: 12px;
  }
</style>
