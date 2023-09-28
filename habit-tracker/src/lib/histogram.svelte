<script>
    export let habits;
    export let days;
    export let progressMap;

    const countProgress = (habit) => {
        let count = 0;
        for (const day in progressMap[habit]) {
            if (progressMap[habit][day] === true) count++
        }
        return count;
    }
</script>

<table>
  <thead>
  {#each habits as habit}
    <td class="header">{habit} ({countProgress(habit)})</td>
  {/each}
  </thead>
  {#each days as day}
    <tr>
      {#each habits as habit}
        {#if countProgress(habit) >= day}
          <td>●</td>
        {:else}
          <td></td>
        {/if}
      {/each}
    </tr>
  {/each}
</table>

<style>
    h1 {
        font-size: 28px;
    }
    td {
        font-size: 18px;
        font-family: 'Nunito sans', sans-serif;
    }
    .header {
        transform: rotate(-45deg);
        padding-bottom: 14px;
    }
</style>