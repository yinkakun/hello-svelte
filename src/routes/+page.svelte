<script>
	import { onMount, afterUpdate, onDestroy } from 'svelte';
	import Hello from '../components/Hello.svelte';
	import { afterNavigate } from '$app/navigation';

	const name = 'Yinks';
	const markup = `<h1>Hello ${name}</h1>`;

	let count = 0;

	afterUpdate(() => {
		document.title = `You clicked ${count} times`;
	});

	onMount(() => {
		console.log('Mounted');
	});

	afterNavigate(() => {
		console.log('Navigated');
	});

	onDestroy(() => {
		console.log('Destroyed');
	});

	$: triple = count * 3;

	const increment = () => (count += 1);
	const decrement = () => (count -= 1);

	$: if (count > 20) {
		alert(`You're taking too much apples`);
	}

	const greetings = ['Hello', 'Hi', 'Hey', 'Hola', 'Bonjour'];
</script>

<div>
	<Hello
		on:hello={(event) => {
			alert(event.detail.message);
		}}
		{name}
	/>
	<div>Apple x3: {triple}</div>
	<div>{@html markup}</div>
	<p>{count} {count <= 1 ? 'apple' : 'apples'}</p>

	<button on:click={decrement}>Decrease</button>
	<button on:click={increment}>Increase</button>
</div>

{#if count >= 20}
	<span>You be thief</span>
{/if}

{#each greetings as greeting, index (greeting)}
	<p>{index} {greeting}</p>
{/each}
