<script lang="ts">
	import Main from '../lib/components/Main.svelte';
	import BackGround from '../lib/components/BackGround.svelte';

	let audio: HTMLAudioElement;
	let started: boolean = false;
	let shouldAudioBePlayed = true;

	function start() {
		audio.play();
		audio.pause();
		audio.volume = 0.1;
		audio.currentTime = 0;
		started = true;
	}
</script>

<BackGround>
	{#if !started}
		<div>
			<div class="btn-wrapper"><button on:click={start} class="btn"> Take the tour </button></div>
			<label>
				<input type="checkbox" bind:checked={shouldAudioBePlayed} />
				With audio
			</label>
		</div>
	{/if}

	{#if started}
		<Main backgroundAudio={audio} shouldBePlayed={shouldAudioBePlayed} />
	{/if}
	<audio bind:this={audio}>
		<source src="ring.mp3" type="audio/mpeg">
	</audio>
</BackGround>


<style>
	.btn-wrapper {
		margin: 1rem 0;
	}

	.btn {
		min-width: 210px;
		text-align: center;
		height: 48px;
		background-color: var(--color-primary);
		color: #000;
		border: 1px solid var(--color-primary);
		border-radius: 24px;
	}

	.btn:hover,
	.btn:focus {
		outline: none;
		background-color: #f2d24e;
	}
</style>