<script>
	import Tree from './Tree.svelte'
	export let files = []
	export let icons
	export let expanded
	export let selected
</script>

<style>
	main :global(ul) {
		list-style: none;
		margin: 0;
	}
	main :global(ul) {
		padding-left: 1rem;
	}
	main :global(> ul) {
		padding: 0;
	}
	main :global(*) {
		font-size: 1rem;
		font-family: monospace;
	}
	main :global(svg) {
		opacity: 50%;
	}
	main :global(button) {
		padding: 0.2rem 0;
		background-color: transparent;
		border: none;
		width: 100%;
		display: flex;
		align-items: center;
	}
	main :global(svg) {
		padding: 0.2rem 0.3rem 0.2rem 0.2rem;
	}
</style>

<main>
	<Tree
		{ files }
		{ icons }
		{ expanded }
		{ selected }
	/>
</main>
