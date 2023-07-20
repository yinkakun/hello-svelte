<script>
	import { createEventDispatcher } from 'svelte';
	import { count } from '../store/count';

	export let name = 'Mystery Man';

	const disaptch = createEventDispatcher();

	const sayHello = () => {
		disaptch('hello', {
			message: `Hello from ${name}`
		});
	};
</script>

<div>{$count}</div>
<button on:click={count.increment}>increase store count</button>
<button on:click={count.decrement}>decrease store count</button>
<h1>Hello {name}</h1>
<button on:click={sayHello}>Say Hello</button>

<style>
	h1 {
		color: #ff3e00;
	}
</style>
