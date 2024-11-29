<script context="module" lang="ts">
	const tips = [
		"Pots canviar el mode de joc tocant VOCABLE o lliscant el taulell de esquerra a dreta.",
		"Mode Expert és independent per a cada mode de joc. Habilitant-li en un mode (p.e. 'Modo Diari' no l'habilitarà en la resta de modes.",
		"Toca dos vegades sobre la paraula per veure la seva definició.",
		"El Mode Expert es pot habilitar en qualsevol moment si no s'han incomplert les normes del Mode Expert.",
		"Toca dos vegades sobre la següent filera buida per veure quantes possibles paraules es poden introduïr basant-se en el intents que s'han fet fins al moment.",
		"És possible que les paraules es repeteixin ja que es generen aleatoriament a partir d'una llista.",
		"Quan vegis el botó d'actualitzar en la banda superior esquerra significa que ja pots jugar una nova paraula.",
		"Tothom té el mateix vocable al mateix temps. La teva paraula #73 és la mateixa que la paraula #73 de tothom.",
		"Hi ha més solucions valides que possibles paraules a endivinar, per tant no totes les paraules de 5 lletres poden ser la paraula a endevinar.",
		"Les partides desades no compten per les teves estadístiques. Les partides desades son les que accedeix amb un enllaç a una paraula en concret.",
		"Només es desen les dades de la última partida per cada mode de joc.",
			];
</script>

<script lang="ts">
	export let change: boolean;
	let index = Math.floor(tips.length * Math.random());
	$: if (change) index = Math.floor(tips.length * Math.random());

	function nextTip() {
		index = (index + 1) % tips.length;
	}
	function previousTip() {
		index = (index - 1 + tips.length) % tips.length;
	}
</script>

<div class="outer">
	<div class="number">Tip {index + 1}/{tips.length}</div>
	<div class="tip">{tips[index]}</div>
	<svg
		class="left"
		on:click={previousTip}
		on:keydown={previousTip}
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 0 100 100"
	>
		<path d="M75,0L25,50L75,100z" />
	</svg>
	<svg
		on:click={nextTip}
		on:keypress={nextTip}
		class="right"
		xmlns="http://www.w3.org/2000/svg"
		viewBox="0 0 100 100"
	>
		<path d="M25,0L75,50L25,100z" />
	</svg>
</div>

<style lang="scss">
	.outer {
		margin: 15px auto;
		padding: 10px 20px;
		max-width: calc(0.6 * var(--game-width));
		border: solid 1px var(--border-secondary);
		background: var(--bg-secondary);
		border-radius: 4px;
		position: relative;
	}
	.number {
		text-align: center;
		font-weight: bold;
		font-size: 1.2em;
		margin-bottom: 10px;
	}
	.left,
	.right {
		cursor: pointer;
		position: absolute;
		border-radius: 4px;
		background: var(--fg-primary);
		fill: var(--bg-primary);
		height: 45px;
		padding: 10px 0;
		top: 50%;
	}
	.left {
		left: 0;
		transform: translate(-50%, -50%);
	}
	.right {
		right: 0;
		transform: translate(50%, -50%);
	}
	.tip {
		text-align: center;
		min-height: 70px;
	}
</style>
