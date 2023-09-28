<script>
  export let checked;
  export let toggle;
</script>

<button on:click={toggle}>
  {checked ? "●" : "○"}
</button>

<style>
  button {
    padding: 0 20px;
    font-size: 40px;
    font-family: "Andale Mono", monospace;
  }
</style>
