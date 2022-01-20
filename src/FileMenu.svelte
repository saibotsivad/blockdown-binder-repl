<script>
	import FileExplorer from './file-explorer/FileExplorer.svelte'

	export let files
</script>

<style>
	div.main {
		display: flex;
		min-height: 100vh;
	}
	div.menu {
		min-height: 100%;
		min-width: 20%;
		white-space: nowrap;
		/* TODO REMOVE */
		background-color: yellow;
	}
	div.content {
		width: 100%;
		min-height: 100%;
		/* TODO REMOVE */
		background-color: red;
	}
</style>

<div class="main">
	<div class="menu">
		<FileExplorer
			{ files }
		/>
	</div>
	<div class="content">
		<p>yolo</p>
	</div>
</div>
