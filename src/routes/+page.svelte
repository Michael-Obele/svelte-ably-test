<script>
	import { onMount } from 'svelte';
	import * as Ably from 'ably';

	let time = 'Sometime';

	const apiKey = import.meta.env.VITE_ABLY_API_KEY;
	let channel;
	let sub;

	function handleClick() {
		channel.publish('update', { Time: Date.now().toString() });
	}


		const ably = new Ably.Realtime(apiKey);
		channel = ably.channels.get('time');

		sub = channel.subscribe((msg) => {
			time = JSON.stringify(msg.data);
		});
</script>

<svelte:head>
	<title>Hello Ably!</title>
	<meta name="description" content="This is where the description goes for SEO" />
</svelte:head>

<div class=" flex justify-center text-center items-center flex-col">
	<h1 class="text-center text-3xl py-6 border-2 border-b-green-300 w-full">
		Ably JS and Svelte Test
	</h1>

	<p class=" text-lg">This Works</p>

	<h3 class=" text-2xl">{time}</h3>

	<button
		on:click={handleClick}
		class="mx-auto rounded-md border bg-gray-950 p-2 text-white hover:bg-gray-400"
		>Publish update</button
	>
</div>

<style>
	.mx-auto {
		margin-left: auto;
		margin-right: auto;
	}

	.flex {
		display: flex;
	}

	.w-full {
		width: 100%;
	}

	.flex-col {
		flex-direction: column;
	}

	.items-center {
		align-items: center;
	}

	.justify-center {
		justify-content: center;
	}

	.rounded-md {
		border-radius: 0.375rem;
	}

	.border {
		border-width: 1px;
	}

	.border-2 {
		border-width: 2px;
	}

	.border-b-green-300 {
		--tw-border-opacity: 1;
		border-bottom-color: rgb(134 239 172 / var(--tw-border-opacity));
	}

	.bg-gray-950 {
		--tw-bg-opacity: 1;
		background-color: rgb(3 7 18 / var(--tw-bg-opacity));
	}

	.p-2 {
		padding: 0.5rem;
	}

	.py-6 {
		padding-top: 1.5rem;
		padding-bottom: 1.5rem;
	}

	.text-center {
		text-align: center;
	}

	.text-2xl {
		font-size: 1.5rem;
		line-height: 2rem;
	}

	.text-3xl {
		font-size: 1.875rem;
		line-height: 2.25rem;
	}

	.text-lg {
		font-size: 1.125rem;
		line-height: 1.75rem;
	}

	.text-white {
		--tw-text-opacity: 1;
		color: rgb(255 255 255 / var(--tw-text-opacity));
	}

	.hover\:bg-gray-400:hover {
		--tw-bg-opacity: 1;
		background-color: rgb(156 163 175 / var(--tw-bg-opacity));
	}
</style>
