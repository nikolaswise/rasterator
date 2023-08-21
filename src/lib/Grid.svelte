<script type="text/javascript">
  export let height = 16
  export let width = 16
  export let dot = 8
  export let color = 'white'

  let rows
  let cols
  $: {
    rows = Array(height)
    cols = Array(width)
  }
</script>

<div
  style:--w={width}
  style:--h={height}
  style:--d={dot}
  style:--c={color}
  class="grid">
  {#each rows as row}
    {#each cols as col}
      <div class="cell"></div>
    {/each}
  {/each}
</div>

<details>
  <summary>Settings</summary>
  <div class="controls">
    <h2>Grid Settings</h2>
    <form>
      <label>
        Width
        <input bind:value={width} type="number" name="width">
      </label>

      <label>
        Height
        <input bind:value={height} type="number" name="height">
      </label>

      <label>
        Cell
        <input bind:value={dot} type="number" name="dot">
      </label>

      <label>
        Grid
        <input bind:value={color} type="color" name="color">
      </label>

    </form>
  </div>
</details>



<style type="text/css">
  .grid {
    pointer-events: none;
    width: fit-content;
    display: grid;
    grid-template-columns: repeat(var(--w), 1fr);
    grid-template-rows: repeat(var(--h), 1fr);
    z-index: 100;
    position: absolute;
    margin: auto;
    left: 50%;
    top: 50%;
    transform: translate3d(-50%, -50%, 0);
  }
  .cell {
    border: 0.5px dashed var(--c);
    height: calc(1mm * var(--d));
    width: calc(1mm * var(--d));
  }

  .controls {
    position: absolute;
    z-index: 200;
    background-color: white;
    border: 2px solid black;
    padding: 1rem;
  }

  label, input {
    display: block;
  }

  h2 {
    margin-top: 0;
  }
  label {
    margin-bottom: 0.5rem;
  }
</style>