<script>
	import Directory from './Directory.svelte'
	import File from './File.svelte'
	import Loading from './Loading.svelte'
	import Error from './Error.svelte'
	import { DIRECTORY, FILE } from './types.js'

	export let files = []
	export let icons
	export let expanded
	export let selected

	const loaders = {}
	const opened = {}

	const open = index => {
		if (typeof files[index].children === 'function') {
			loaders[index] = files[index].children()
		} else {
			loaders[index] = files[index].children
		}
		opened[index] = true
	}

	const close = index => {
		loaders[index] = null
		opened[index] = null
	}

	if (expanded === true) {
		files.forEach((file, index) => {
			opened[index] = true
			open(index)
		})
	}
</script>

<ul>
	{#each files as file, index}
		<li>
			{#if file.children}
				<Directory
					opened={ opened[index] }
					directory={ file.name }
					on:open={ () => open(index) }
					on:close={ () => close(index) }
				/>
			{:else}
				<!-- TODO need to make sure File knows full path -->
				<File
					{ icons }
					{ selected }
					name={ file.name }
				/>
			{/if}

			{#if file.children}
				{#if loaders[index]}
					{#await loaders[index]}
						<ul>
							<li>
								<Loading />
							</li>
						</ul>
					{:then files}
						<svelte:self
							{ expanded }
							{ files }
							{ icons }
							{ selected }
						/>
					{:catch error}
						<ul>
							<li>
								<Error
									{ error }
								/>
							</li>
						</ul>
					{/await}
				{/if}
			{/if}
		</li>
	{/each}
</ul>
