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
			<button on:click={start}> Take the tour </button>
			<br />

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
		<source src="/ring.mp3" type="audio/mpeg">
	</audio>
</BackGround>
