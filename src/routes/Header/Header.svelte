<script lang="ts">
	import { onMount } from "svelte";
	import { createEventDispatcher } from "svelte";

    export let text;
	const dispatch = createEventDispatcher();

	type Star = {
		top: string;
		left: string;
		animationDuration: number;
		scale: number;
	};

	let stars: Star[] = [];
	let sparkleScale: number = 0.8; // Giá trị mặc định

	onMount(() => {
		const starCount = 50;

		for (let i = 0; i < starCount; i++) {
			stars = [
				...stars,
				{
					top: getRandomPosition(),
					left: getRandomPosition(),
					animationDuration: getRandomDuration(),
					scale: sparkleScale,
				},
			];
		}
	});

	function getRandomPosition() {
		return Math.random() * 100 + "%";
	}

	function getRandomDuration() {
		return Math.random() * 1 + 0.5; // Random duration between 0.5s and 1.5s
	}

	function updateSparkleScale(e) {
		sparkleScale = parseFloat(e.target.value);

		// Cập nhật giá trị scale cho tất cả các ngôi sao
		stars = stars.map((star) => ({
			...star,
			scale: sparkleScale,
		}));

		// Gửi sự kiện để thông báo về sự thay đổi giá trị scale
		dispatch("scaleChange", sparkleScale);
	}
</script>

<!-- phần còn lại không thay đổi -->


<main>
	<div class="starry-night">
		{#each stars as { top, left, animationDuration, scale }, i}
			<div
				class="star"
				style="top: {top}; left: {left}; animation-duration: {animationDuration}s; transform: scale({scale})"
			/>
		{/each}
		<div class="center-text">
			<h1>{text}</h1>
		</div>
	</div>

	<!-- <div class="settings">
		<label for="sparkle-scale">Sparkle Scale:</label>
		<input
			type="range"
			id="sparkle-scale"
			min="0.1"
			max="2"
			step="0.1"
			bind:value={sparkleScale}
			on:input={updateSparkleScale}
		/>
	</div> -->
</main>

<style lang="scss">
	.starry-night {
		background: linear-gradient(
			to bottom,
			#001f3f,
			#003366,
			#004080,
			#00509e
		);
		height: 100vh;
		overflow: hidden;
		position: relative;
		perspective: 1000px;
	}

	.star {
		width: 30px;
		height: 30px;
		background: url("https://static.vecteezy.com/system/resources/thumbnails/011/024/332/small/digital-glowing-light-effect-free-png.png")
			no-repeat center center;
		background-size: cover;
		position: absolute;
		animation: sparkle 1s infinite;
	}

	@keyframes sparkle {
		0%,
		100% {
			transform: scale(0.8);
		}
		50% {
			transform: scale(0.4);
		}
	}

	$star-count: 100;

	@for $i from 1 through $star-count {
		.star:nth-child(#{$i}) {
			$top: random(100%);
			$left: random(100%);
			top: $top;
			left: $left;
		}
	}

	.center-text {
		text-align: center;
		color: white;
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%) rotateX(30deg);
	}

	h1 {
		font-size: 4em;
		margin: 0;
		padding: 20px;
		text-shadow: 4px 4px 6px rgba(0, 0, 0, 0.8);
		border: 10px solid white;
		border-radius: 15px;
	}

	.settings {
		position: fixed;
		top: 10px;
		left: 10px;
		background-color: rgba(255, 255, 255, 0.8);
		padding: 10px;
		border-radius: 5px;
	}

	label {
		margin-right: 5px;
	}
</style>
