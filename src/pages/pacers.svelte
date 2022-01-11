<script>
    import axios from "axios";
    import { dataset_dev } from "svelte/internal";
    const pacersId = 1610612754;
    const url =
        "http://data.nba.net/10s/prod/v1/current/standings_all_no_sort_keys.json";

    async function fetchPacersData() {
        const dailyNbaData = await axios.get(url);
        const pacers = dailyNbaData.data.league.standard.teams.filter(
            (team) => team.teamId === pacersId.toString()
        )[0];
        return {
            win: pacers.win,
            loss: pacers.loss,
            confRank: pacers.confRank,
        };
    }

    let pacers = fetchPacersData();
</script>

<p>This is my pacers page</p>

{#await pacers}
    <p>...waiting</p>
{:then data}
    <p>The pacers have won {data.win} games and loss {data.loss} games</p>
    <p>They are in {data.confRank} place</p>
{:catch error}
    <p>something bad happened: {error}</p>
{/await}

<p>vvv TODO vvv</p>
<p>Previous Result:</p>
<p>Last Ten:</p>
<p>Next Game:</p>
<p>Chances of making playoffs:</p>
<a href="/">Home</a>
