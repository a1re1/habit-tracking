<script xmlns:C="http://www.w3.org/1999/html">
  import Days from './lib/daytracker.svelte'
  import Totals from './lib/histogram.svelte'

  const currentDate = new Date();
  const year = currentDate.getFullYear();
  const month = String(currentDate.getMonth() + 1).padStart(2, '0');
  const monthName = currentDate.toLocaleString('en-US', { month: 'long' });

  let habits = ["glutes", "hips", "core", "calves"]
  let days = []
  let progressMap = {};
  let showDays = true;

  habits.forEach(habit => progressMap[habit] = {});
  for (let i = 1; i <= 31; i++) {
    days.push(i);
    habits.forEach(habit => progressMap[habit][i] = JSON.parse(localStorage.getItem(habit + "-" + i + "-" + month + "-" + year)));
  }
  const clear = () => {
      habits.forEach(habit => progressMap[habit] = {});
      for (let i = 1; i <= 31; i++) {
          habits.forEach(habit => localStorage.removeItem(habit + "-" + i + "-" + month + "-" + year));
      }
      progressMap = {};
      habits.forEach(habit => progressMap[habit] = {})
  }
</script>

<style>
  h1 {
    font-size: 28px;
  }
  td {
    font-family: 'Nunito sans', sans-serif;
  }
  .viewToggle {
      margin-bottom: 5px;
  }
</style>

<main>
  <button class="viewToggle" on:click={() => showDays = !showDays}>
    {showDays ? "Totals" : "Days"}
  </button>
  <h1>{monthName}</h1>
  {#if showDays}
    <Days habits={habits} days={days} progressMap={progressMap}/>
  {:else}
    <Totals habits={habits} days={days} progressMap={progressMap}/>
  {/if}
  <br>
  <button class="viewToggle" on:click={() => clear()}>
    Clear
  </button>
</main>


