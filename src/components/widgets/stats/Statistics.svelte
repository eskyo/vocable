<script lang="ts">
	import { mode } from "../../../stores";
	import { modeData, Stats } from "../../../utils";

	import Stat from "./Stat.svelte";
	export let data: Stats;

	let stats: [string, string | number][];
	$: {
		stats = [
			["Partides", data.played],
			["Èxits (%)", Math.round(((data.played - data.guesses.fail) / data.played) * 100) || 0],
			[
				"Mitjana d'intents",
				(
					Object.entries(data.guesses).reduce((a, b) => {
						if (!isNaN(+b[0])) {
							return a + +b[0] * b[1];
						}
						return a;
					}, 0) / data.played || 0
				).toFixed(1),
			],
		];
		if (data.guesses.fail > 0) {
			stats.push(["No endevinats", data.guesses.fail]);
		}
		if (data.hasStreak) {
			stats.push(["Ratxa actual", data.streak]);
			stats.push(["Ratxa màxima", data.maxStreak]);
		}
	}
</script>

<h3>Estadístiques (Mode: {modeData.modes[$mode].name})</h3>
<div>
	{#each stats as stat}
		<Stat name={stat[0]} stat={stat[1]} />
	{/each}
</div>

<style>
	div {
		display: flex;
		justify-content: center;
		gap: 8px;
	}
</style>
