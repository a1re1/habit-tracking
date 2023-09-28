<script>
    import Checkbox from './checkbox.svelte'
    export let habits;
    export let days;
    export let progressMap;

    const currentDate = new Date();
    const year = currentDate.getFullYear();
    const month = String(currentDate.getMonth() + 1).padStart(2, '0');
</script>

<table>
    <thead>
    <td></td>
    {#each habits as habit}
        <td class="header">{habit}</td>
    {/each}
    </thead>
    {#each days as day}
        <tr>
            <td>{day}</td>
            {#each habits as habit}
                <td>
                    <Checkbox checked={progressMap[habit][day]} toggle={() => {
                        const value = progressMap[habit][day];
                        localStorage.setItem(habit + "-" + day + "-" + month + "-" + year, JSON.stringify(!value))
                        progressMap[habit][day] = !value
                    }}/>
                </td>
            {/each}
        </tr>
    {/each}
</table>

<style>
    h1 {
        font-size: 28px;
    }
    td {
        font-family: 'Nunito sans', sans-serif;
    }
    .header {
        transform: rotate(-45deg);
        padding-bottom: 14px;
    }
</style>