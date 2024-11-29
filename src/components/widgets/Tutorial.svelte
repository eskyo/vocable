<script lang="ts">
	import { COLS, ROWS } from "../../utils";

	import { Tile } from "../board";
	export let visible: boolean;
</script>

<h3>Com jugar</h3>
<div>Endevina el <strong>VOCABLE</strong> en {ROWS} intents.</div>
<div>Cada intent ha de ser una paraula válida de {COLS} lletres. Apreta el botó intro per confirmar.</div>
<div>
	Després de cada intent, el color de les caselles canviarà per mostrar quant t'has apropat a la paraula que has d'endevinar.
</div>
<div class:complete={visible} class="examples">
	<div><strong>Exemples</strong></div>
	<div class="row">
		<Tile value="a" state="🟩" />
		<Tile value="m" state="🔳" />
		<Tile value="i" state="🔳" />
		<Tile value="g" state="🔳" />
		<Tile value="a" state="🔳" />
	</div>
	<div>La lletra <strong>A</strong> està en la posició correcta de la paraula que has d'endevinar.</div>
	<div class="row">
		<Tile value="p" state="🔳" />
		<Tile value="l" state="🟨" />
		<Tile value="u" state="🔳" />
		<Tile value="j" state="🔳" />
		<Tile value="a" state="🔳" />
	</div>
	<div>La lletra <strong>L</strong> forma part de la paraula que has d'endevinar, però no es troba en la posició correcta.</div>
	<div class="row">
		<Tile value="b" state="🔳" />
		<Tile value="a" state="🔳" />
		<Tile value="r" state="🔳" />
		<Tile value="c" state="⬛" />
		<Tile value="a" state="🔳" />
	</div>
	<div>La lletra <strong>C</strong> no forma part de la paraula que has d'endevinar.</div>
</div>
<div>
	Aquesta es una recreació del joc original <a
		href="https://www.nytimes.com/games/wordle/"
		target="_blank"
		rel="noreferrer">Wordle</a
	>
	creat per Josh Wardle. Canvia al Mode Infinit per a jugar sense límits.
	<br /><br />
	Obre el menú de configuració per a veure més opcions i modes de joc.
	<br />
	Programat amb Svelte, en Typescript per
	<a href="https://github.com/MikhaD" target="_blank" rel="noreferrer">MikhaD</a> i adaptat al català per
	<a href="https://github.com/eskyo" target="_blank" rel="noreferrer">eskyo</a>.
</div>

<style lang="scss">
	div {
		margin: 14px 0;
	}
	.examples {
		border-top: 1px solid var(--border-primary);
		border-bottom: 1px solid var(--border-primary);
		:global(.row > *) {
			height: 100%;
			aspect-ratio: 1;
		}
		&:not(.complete) :global(.row .back) {
			transition-delay: 0.3s;
		}
	}
	.row {
		height: 40px;
		display: flex;
		gap: 4px;
	}
</style>
