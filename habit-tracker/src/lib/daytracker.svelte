<script>
    import Checkbox from './checkbox.svelte'
    export let habits;
    export let days;
    export let progressMap;

    const currentDate = new Date();
    const year = currentDate.getFullYear();
    const month = String(currentDate.getMonth() + 1).padStart(2, '0');
    const day = currentDate.getDate();
</script>

<table>
    <thead>
    <td></td>

    </thead>
    {#each habits as habit}
        <tr>
            <td>{habit}</td>
        <td>
            <Checkbox checked={progressMap[habit][day]} toggle={() => {
                        const value = progressMap[habit][day];
                        localStorage.setItem(habit + "-" + day + "-" + month + "-" + year, JSON.stringify(!value))
                        progressMap[habit][day] = !value
                    }}/>
        </td>
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