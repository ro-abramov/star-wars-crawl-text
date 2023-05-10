<script lang="ts">
	import { onMount } from 'svelte';

	export let backgroundAudio: HTMLAudioElement;
	export let shouldBePlayed: boolean;

	interface Star {
		x: number;
		y: number;
		size: 'small' | 'large';
		opacity: number;
	}

	function randomUpto(top: number): number {
		return Math.round(Math.random() * top);
	}

	function makeStars(): Star[] {
		return Array.from({ length: 1000 }, () => {
			return {
				x: randomUpto(4000),
				y: randomUpto(2200),
				size: Math.random() > 0.5 ? 'large' : 'small',
				opacity: Math.random()
			};
		});
	}

	const stars = makeStars();

	onMount(() => {
		if (shouldBePlayed) {
			setTimeout(() => {
				backgroundAudio.play();
			}, 7000);
		}
	});
</script>

{#each stars as star}
	<div
		class="star"
		class:star_large={star.size === 'large'}
		style="opacity: {star.opacity}; top: {star.y}px; left: {star.x}px"
	/>
{/each}

<section class="intro-text">Давным-давно в далёкой галактике....</section>

<section class="logo">
	<img src="sw-logo.svg" alt="Star wars logo" />
</section>

<div class="main-text-wrapper">
	<div class="main-text">
		<p class="main-text-title">Эпизод VII</p>
		<p class="main-text-subtitle">Рождение джедая</p>
		<br />
		<p>
			7 лет назад в далекой далекой галактике был рождён мальчик. Совет выбрал ему имя - Тимур.
			Теперь юный джедай приглашает вас на пикник чтобы отметить его седьмой день рождения и
			испытать джедайские навыки. Приходите голодными в субботу 27 мая в 12 часов дня на Аду
			Циганлию.
		</p>
		<br />
		<p>Мы очень надеемся увидеть вас!</p>
		<br />
		<p>И да пребудет с вами сила!</p>
	</div>
</div>

<style>
	.star {
		position: fixed;
		width: 2px;
		height: 2px;
		border-radius: 2px;
		background-color: #fff;
	}

	.star_large {
		width: 3px;
		height: 3px;
		box-shadow: 0px 0px 2px 2px rgba(255, 255, 255, 0.3);
	}

	.intro-text {
		color: var(--color-intro);
		font-size: var(--font-size-600);
		padding: var(--gap-300);
		max-width: 900px;
		min-width: 340px;
		animation: intro var(--intro-duration) ease-out var(--intro-delay);
		opacity: 0;
	}

	@keyframes intro {
		0% {
			opacity: 0;
			display: block;
		}
		20% {
			opacity: 1;
		}
		90% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}

	.logo {
		position: absolute;
		inset: 0;
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		overflow: hidden;
	}

	.logo img {
		opacity: 0;
		transform: scale(1.8);
		width: 80%;
		animation: logo var(--logo-duration) ease-out var(--logo-delay);
	}

	@keyframes logo {
		0% {
			opacity: 0;
			transform: scale(1.8);
		}
		20% {
			opacity: 1;
			transform: scale(1);
		}
		80% {
			opacity: 1;
		}
		90% {
			opacity: 0.7;
		}
		100% {
			opacity: 0;
			transform: scale(0.1);
		}
	}

	.main-text-wrapper {
		padding: var(--gap-300);
		transform: perspective(300px) rotateX(25deg);
		transform-origin: 50% 100%;
		position: absolute;
		font-weight: bold;
		overflow: hidden;
		font-size: 350%;
		height: 50em;
		width: min(18em, 90vw);
		bottom: 20%;
	}

	.main-text {
		font-size: var(--font-size-600);
		text-align: justify;
		animation: scroll var(--text-duration) linear var(--text-delay);
		position: absolute;
		top: 100%;
	}

	.main-text-title {
		text-align: center;
		padding: var(--gap-400);
	}

	.main-text-subtitle {
		text-align: center;
		font-size: var(--font-size-700);
		padding: var(--gap-400);
	}

	@keyframes scroll {
		0% {
			top: 100%;
			display: block;
		}
		100% {
			top: -80%;
		}
	}

	@media screen and (min-width: 640px) {
		.main-text {
			font-size: var(--font-size-xl);
		}

		.main-text-subtitle {
			font-size: var(--font-size-xxl);
		}

		.intro-text {
			font-size: var(--font-size-900);
		}
	}
</style>
